Database Internal
===

### Storage Engine

Cassandra使用類似log-structured merge-tree的儲存結構，而非傳統RMDB的Binary Tree。Cassandra 避免寫入前讀取(read-before-write)，在大型分散式系統可能造成嚴重延遲。Cassandra先將新增與修改先儲存在記憶體中，並依序地以附加模式(append)寫入硬碟，寫入硬碟後的資料不可變更(immutable)。使用HDD依序寫入會需要大量的查找(seek operation)，查找造成的效能降低十分顯著，Cassandra很適合使用消費級SSD。

### 寫入

* 資料log到commit log
* 寫入到memTable
* Flush memTable
* 寫入SSTable
所有的寫入都會先寫到memTable，並同時寫入commit log。memTable是資料分割的write-back cache，供使用鍵值查找資料。memTable達到設定上限(commitlog_total_space_in_mb)後會放到駐列(Queue)，依序寫入SSTable，然後flush。
寫入SSTable時，同時會產生分割Index寫入硬碟來映射token到物理位置。

### SSTable
SSTable不可變更(Immutable)，從memTableFlush出後就不會再次寫入，所以一個分割通常會有數個SSTable。SSTable

* Data(data.db) SStable資料
* Primary Index(Index.db) 指向資料列的位置
* Bloom filter(Filter.db) 儲存在記憶體中，讀取SSTable前，檢查資料列是否存在memTable
* Compression Information(CompressionInfo.db) 儲存資料的訊息如未壓縮長度、chuck offset、...等
* Statistics(Statistics) 關於SSTable統計的metaData
* Digest(Digest.csc32、Digest.adler32、Digest.sha1) 儲存編碼後的校驗碼(checksum)
* CRC(CRC.db) 儲存未壓縮的CRC32資料塊(chunk)
* SSTable Index Summary(SUMMARY) 分割Index的樣本
* SSTable Table of Contexts 
> TOC.txt
> Summary.db
> Index.db
> CompressionInfo.db
> Filter.db
> Data.db
> Digest.crc32
> Statistics.db
* Secondary Index(SI_.\*.db)) SSTable可能會有多個SI


SSTTable儲存在硬碟上，如：
/var/lib/cassandra/data/demo/emp-08bb65000b1f11e7b2156d2c86545d91
|--/backups
|--mc-1-big-CompressionInfo.db
|--mc-1-big-Data.db
|--mc-1-big-Digest.crc32
|--mc-1-big-Filter.db
|--mc-1-big-Index.db
|--mc-1-big-Statistics.db
|--mc-1-big-Summary.db
|--mc-1-big-TOC.txt
demo為keyspace，emp為資料表(table)，08bb65000b1f11e7b2156d2c86545d91為16進位的字串作為unique Table ID

### 資料維護
http://docs.datastax.com/en/cassandra/3.0/cassandra/dml/dmlHowDataMaintain.html

SSTable不可變動，Cassandra使用時間戳版本(timestamp version)標記SSTable的新增與更新，Cassandra不執行刪除，而是標記墓碑(tombstone)。

隨時間推移，Cassandra會寫入許多版本的SSTable，為了取得最新版本的資料列，對SSTable的存取會增加。Cassandra會週期性的合併(merge)這些SSTable並去除舊資料，這個程序稱為壓縮(compaction)

##### Compaction
從一群SSTable中取出資料列的所有版本，依據時間戳留下最新版本的資料。取出資料列由於使用partition key，所以效能穩定，也不需要random I/O。新的版本會寫入到新的SSTable，(在駐列中的存取結束後)舊的SSTable會被刪除。

由於新舊SSTable同時並存，Compaction會在成暫時的硬碟用量高峰，結束後才釋放硬碟使用。新的SSTable會提升存取效能。壓縮過程中，新的SSTable可以存取資料，不需等待Compaction完成。

##### Compaction Strategy

###### SizeTeiredCompactionStrategy(STCS)
write-intensive workflow

###### LeveledCompactionStrategy(LCS)
read-intensive workflow

###### TimeWindowCompactionStrategy(TWCS)
time series and expiring TTL workflow

###### DateTieredCompactionStrategy 


### 設定與執行
CREATE TABLE或ALTER TABLE時設定
使用nodetool compact

### 資料更新

Cassandra使用upsert處理新增，新增資料列時不檢查該主鍵的資料列是否已存在，所以可能會有一個或多版本存在。

在讀取時Cassandra也會進行Compaction，當讀取資料時也會需要取出各版本資料並比對，這時便一併進行Compaction，不會影響讀取。

### 資料刪除

Cassandra使用upsert處理刪除，被刪除的資料會標上墓碑(tombstone)，墓碑依循寫入流程並被寫入SSTable。墓碑內建失效時間(expiration date/time)，compaction程序中會將超過失效時間的墓碑資料移除。使用者可以手動標記生效時間(time-to-live)到資料列(row)或資料欄(column)，當過期時會被Cassandra標記墓碑。

##### 分散式系統的刪除

多Node的Cluster中，不同Node之中儲存了多個複本，這有助於防止資料遺失，但卻讓刪除變得複雜。一個Node收到刪除指令，並把資料標記墓碑時，會將墓碑的訊息通知其他Node，然而如果其他Node有離線的Node，這個離線Node自然不會收到墓碑的訊息，資料仍然維持未刪除(pre-delete)的版本，當其他在線Node都刪除資料後，離線Node上線時的回復程序，又會將這筆資料，從剛上線的Node散佈到其他已刪除資料的Node。這種被刪除但卻保存下來的資料稱為殭屍資料(Zombie)。

為了避免殭屍資料，Cassandra給每個刪除一個grace period，讓刪除時未回應的離線Node有時間先回復，並正常處理墓碑。在grace period時，如果客戶更新墓碑資料，Cassandra會複寫墓碑；如果客戶讀取墓碑資料，Cassandra會忽視墓碑資料，並試圖尋找其他複本。

當Node回覆後，Cassandra使用hinted handoff回放Node錯過的資料庫變更，grace period中墓碑資料不會被更新。然而當grace period之後，墓碑資料還是會被更新，而錯過刪除指令。

grace period後，Cassandra會在Compaction中刪除墓碑資料。grace period可在資料表(table)中設定gc_grace_period，預設值是864000秒(10 天)。

墓碑上標記的失效時間=墓碑的建立時間+gc_grace_period。
Cassandra支援批次資料新增及更新，但這同時會增加回復節點時回放時的危險，節點回復後的回放，批次寫入不會變更還在grace period中的墓碑資料。
單節點Cluster(single-node cluster)中可將gc_grace_period設為0。

To completely prevent the reappearance of zombie records, run nodetool repair on a node after it recovers, and on each table every gc_grace_seconds.
If all records in a table are given a TTL at creation, and all are allowed to expire and not deleted manually, it is not necessary to run nodetool repair for that table on a regular basis.
If you use the SizeTieredCompactionStrategy or DateTieredCompactionStrategy, you can delete tombstones immediately by manually starting the compaction process.
CAUTION:
If you force compaction, Cassandra may create one very large SSTable from all the data. Cassandra will not trigger another compaction for a long time. The data in the SSTable created during the forced compaction can grow very stale during this long period of non-compaction.
Cassandra allows you to set a default_time_to_live property for an entire table. Columns and rows marked with regular TTLs are processed as described above; but when a record exceeds the table-level TTL, Cassandra deletes it immediately, without tombstoning or compaction.
Cassandra supports immediate deletion through the DROP KEYSPACE and DROP TABLE statements.

### 索引的儲存與更新

由於資料是依照主鍵的分割鍵，分配到不同節點的不同分割上，所以使用一個主鍵來查詢(query)，只需要讀取一個節點。非主鍵(non-primary key)無關資料分割與分配，所以使用非主鍵查詢會需要讀取所有Node，造成不被允許的嚴重讀取延遲。

次級索引(Secondary Index)提供非主鍵的資瞭查找，可以使用資料表的欄位(coumn)建立。這些索引透過背景程序儲存在本地節點地的隱藏資料表。使用主鍵搭配次級索引可以快速查找資料，只需讀取一個節點。單獨使用次級索引查找會產生嚴重讀取延遲，使用時必須在query option中設定Allow Filtering；不建議在生產環境使用。

次級索引並不保證索引是沒問題的，所以可以直接使用，但有更好的解決方案，像是建立materialized view或使用次級索引作為主鍵新建一個資料表。

如同關聯資料庫，索引需要維持更新，欄位被更新時索引會一併被更新。 If the old column value still exists in the memtable, which typically occurs when updating a small set of rows repeatedly, Cassandra removes the corresponding obsolete index entry; otherwise, the old entry remains to be purged by compaction. If a read sees a stale index entry before compaction purges it, the reader thread invalidates it.


### 資料讀取

Cassandra透過以下步驟讀取不同狀態與位置的資料：
* 檢查memTable
* 檢查row cache(有啟用的話)
* 檢查Bloom filter
* 檢查分割鍵快取(如果有啟用的話)
** 有找到partition key，就直接到compression offset map
** 沒有找到就檢查Partition summary，再到partition index
* 透過compression offset map找到資料的位置，讀取SSTable


##### memTable
如果memTable中有資料，則會取出，並與SSTable的資料比較

##### Row Cache

-Row cache是為write-intensive指令。啟用時會將部分-

LRU(Least-recently-used)的資料會儲存在Row cache中，讓常用資料備查找時省去兩步驟的查找。

##### Bloom filter

每個SSTable都有對應的一個Bloom filter，可以判斷對應的SSTable沒有該筆資料的機率，減少不必要的查找、加速流程，然而由於bloom filter是以機率推估，有可能產生假陽性。如果bloom filter後都找不到對應的SSTable，會去尋找partition key cache。

##### Partition key cache

將partition key存在快取中，如果partition key cache找到，便會跳過partition summary直接到compression offset map中找到確定含有資料的comporessed block。

##### Partition Summary

將partition index的部分樣本儲存存在記憶體中，例如20筆index一個區段採樣，藉著先讀取partition summary可以確定區要的index在partition index的約略位置，加速partition index上的查找。

##### Partition index

將所有的parition key與其對應的comporession offet資訊紀錄在硬碟上，，一次查找可以找到compression offset map對應的comporessed block。

##### compression offset map

儲存實際的pointer，指向資料的確定位置。可經由partition kwy cache與partition index，定位compression offset來取用


# Data consistency

### 如何處理Consistent寫入與讀取

Consistency指的是如何同步且更新(up-to-date)一個資料列的所有複本。Cassandra的composition確保所有副本「終究」會達成一致(coonsistency)，但大型分散式系統中的constant data traffic可能導致資料不一致(inconsistency/stale data)。Cassandra在CAP理論()中為AP系統(availability & partition tolerance)，然而依照應用的需求，cassandra可以透過富有彈性的設定，達到CP(consistent & partition tolerant)，

##### Tunable consistency

Cassandra透過tunable consistency擴展終究一致(eventually consistent)，使用者可以針對每個讀取或寫入動作設定一致性，或是對cluster或datacenter作全域設定，讓cassandra可以依照應用程式的需求表現更為CP或AP。

要求一致性的代價便是延遲，高一致性導致嚴重的延遲、低一致性允許低延遲。可以控制一致性來控制延遲。

一致性等級(Consistenct level)表示：一次讀取或寫入需要多少複本確認後才能回傳成功。以讀取為例，讀取一致性等級表示回復客戶端前，需要認可(acknoledgement)的複本數量。如果讀取未達一致(inconsistent)，Cassandrac會進行讀取修復(read repair)來不一致的資料。以寫入為例：寫入一致性等級表示寫入時有多少複本需要認可才算寫入成功，cassandra總是會寫入所有的複本，寫入一致性等級指示表示coordinator回傳成功以及寫入視為成功。使用hinted handoff來確保複本離線時的寫入完成，否則不回應本次寫入。

原則上，使用低於keyspace複製因數(replication factor)的一致性等級，或是寫入一致性等級為QUORAM，搭配讀取一致性為QUORAM，端看應用的需求。


##### Linearizable consistenct

ACID中，可線性一致性(或序列化一致性serial consistency)指的是輕量交易(lightweight transcation)中一個序列化(立即)的隔離等級(isolation level)。Cassandra在進行並發(concurrent)更新時不使用傳統機制如鎖定(locking)或是交易依賴(transaction dependency)。

然而，某些行動必須要依照順序且不能被打斷。例如：複寫或重複的使用者帳戶可能導致嚴重後果。像說race condition(兩個客戶更新同筆資料)會導致複本不一致。提高寫入一致性等級無法減輕問題。使用者可以對unique identifier使用linearizable consistency，cassandra中可以使用Paxos consensus protocol，一個quorum-based演算法。Lightweight transactions can be implemented without the need for a master database or two-phase commit process.

Lightweight transaction write operations use the serial consistency level for Paxos consensus and the regular consistency level for the write to the table

##### 計算一致性

讀取與寫入的可靠性(reliability)仰賴驗證行動的一致性設定，高一致性可以確保：

> R + W > N

* R 是讀取一致性等級
* W 是寫入一致性等級
* N 是複本數量

例如：複製因數為3，則讀取與寫入的一致性等級總和需要大於等於4。寫入時在3個複本中驗證2個複本，搭配讀取時在3複本中驗證2個，來確保高一致性。如果需求是快速寫入但又確保一致性，則把寫入一致性設為1，將讀取一致性設為3，以讀取減速換取寫入更加速。

下面情況滿足終究一致性(eventullay consistent)

> R + W =< N

如果複製因數為3，讀取一致性為QUORUM(3個複本中的2個)，寫入一致性為ONE(3個複本中的1個)。複本終究會獲得正確資料，但可能會在複本更新完前讀取到資料。

##### 一致性範例

* 寫入一致性：ONE，複本寫入後毀損，則失去資料。
* 寫入一致性：ONE，結果寫入逾時(time out)，讀取時讀到舊資料，會難以察覺資料是錯誤的。
* 寫入一致性：ONE，其他的一個複本離線，等到該複本重新上線，這個節點仍會提供舊資料，直到被更新或是read repair。
* 寫入一致性：quorum，讀取一致性：quorum，縱然有節點離線，總能讀取到正確資料。


