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