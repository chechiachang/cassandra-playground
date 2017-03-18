架構
===

Cassandra將大量資料分散到複數Node處理，無單點故障

### Key structures

* Node
儲存資料的地方。是Cassandra的基本單元 。

* Data Center 
一個Node的集合。Data center設定Replication，將資料寫入多個Data Center。

* Cluster 
一個Cluster包含多個Data center。Cluster可以分散到不同的實體地點。

* Commit log 
所有資料都會先寫入到Commit log，然後才會flush到SSTables

* Table 
一個欄位(column) 的排序集合。一個列(row)包含有多個欄位，以及一個主鍵(Primary Key)。

* SSTable 
一個排序過的子串表(Sorted String Table)，是一個不變(Immutable)的資料檔案。Cassandra週期性地將MemTable的資料寫入SSTable。SSTable寫入時只能新增資料，在維護時才會整理。

### Key components

* Gossip
一個P2P(peer-to-peer)的溝通協定，Node會與Cluster中其他Node分享位置與狀態。
* Partitioner
一個計算partition key的hash函數，決定如何分配資料到Node中，以及哪個Node先放置第一筆資料。
* Replication factor
Cluster中的複本(replica)數量。RF為1 表示每列資料只存在一個Node中。
* 複本放置策略(Replica placement strategy)
決定複本應該放在那些Node上。建立keyspace時需要定義。
* Snitch

* cassandra.yaml
* System keyspace table properties

### Internode communications (Gossip)

Node週期性的分享所知的狀態訊息(包括自身與其他Node)，Gossip每秒執行訊息交換，最多同時與相同Cluster內的Node交換訊息。Gossip訊息有時間版本，舊的訊息會被新的訊息取代。
對一個Cluster內的所有Node使用同一份seed nodes清單，以避免Gossip造成問題。Seed nodes只用來引導新Node加入Cluster。如果Cluster中有複數Data center，最好每個Data center都有一個Node包含在seed清單內，否則引導新Node時就必須Gossip其他Data center。不建議將所有Node放在seed，因為會增加維護成本、降低Gossip效能。建議使用精簡的seed清單(每個Data center3個左右)。

### Failure Detection & recovery

Failure detection 是使用本地的Gossip狀態與紀錄判斷另一個Node是在線或斷線，盡量避免將客戶端的請求送到離線的Node。(透過Dynamic snitch也可以屏蔽在線的Node，但效能不佳)
Gossip程序追蹤狀態訊息(包含直接的一手訊息以及間接收到的第二手、第三手訊息)。 Cassandra計算帳戶網路效能、工作負擔、歷史狀態來精準的標記斷線的Node。每個Node在Gossip時會記錄Node間的回應時間。設定phi_convict_threshold來調整failure detection的敏銳度，數值越低則標記未回應的Node的機率越高，數值越高則降低被標記為斷線的機率。

硬體失效或是網路問題都可能使Node斷線，Node斷線可能都是過渡性的，而非長久性的斷線，其他的Node會嘗試重新建立連線。管理員必須使用nodetool-utility或是OpsCenter才能將Node移出cluster。

### Data distribution and replication

Cassandra中資料分配(Data distribution)與複製(Replication)為一體兩面，資料以表格組織、以主鍵(Primary Key)辨識並決定儲存資料的Node，複本(Replica)為資料列(row)的複製，第一次寫入也是一個複本。

影響複製的因子：
* Virtual Nodes：指派資料所有權給實體機器(Physical Machine)
* Partitioner：在Cluster中分割資料。
* 複製策略(Replication Strategy)：決定每個資料列的複本
* Snitch：定義複製策略的拓樸(Topology)訊息，用來放置複本
* Consistent Hashing：允許Cluster中的資料分割，以最小化新增或移除Node時的重新組織(reorganization)
* Virtual Nodes：
* Data replication：儲存複本，確保可靠性(Reliability)與故障容忍(Fault Tolerance)

### Consistent hashing

最小化新增或移除Node時的重新組織(reorganization)。Consistent hashing依照分割鍵(Partition key)分割資料。

 <table>
    <tr>
        <th>name</th>
        <th>age</th>
        <th>car</th>
        <th>gender</th>
    </tr>
    <tr>
        <td>david</td>
        <td>29</td>
        <td>yamaha</td>
        <td>M</td>
    </tr>
    <tr>
        <td>kim</td>
        <td>29</td>
        <td>sym</td>
        <td>F</td>
    </tr>
 </table>
 <table>
    <tr>
        <th>Partition key</th>
        <th>Murmur3 hash value</th>
    </tr>
    <tr>
        <td>david</td>
        <td>-2245462676723223822</td>
    </tr>
    <tr>
        <td>kim</td>
        <td>7723358927203680754</td>
    </tr>    
 </table>

Cluster中的每個Node負責一個(hash code)的區段，Cassandra將資料依照負責的區段分配資料，資料會分配給負責該區段的Node。


### Virtual nodes
又稱Vnodes，使用token更精細地分配資料，簡化許多Casandra的背景工作。

* Token自動計算並指派給Node
* 增加或減少Node時，自動完成Cluster中的再平衡(Rebalance)。Node加入時會平均分擔其他Node的資料；Node離開時會將資料分散給其他Node。
* 重建離線(dead)Node速度較快，因為其他每個Node都參與。
* Cluster中的每台機器都可以設置Vnode的比例，所以不同大小的機器可以使用這一個Cluster中。

### Cluster內部的資料分配
http://docs.datastax.com/en/cassandra/3.0/cassandra/architecture/archDataDistributeDistribute.html

1.2前的Cassandra需要計算並指派單一Token給Cluster中的每個Node，Token決定Node的位置以及資料分配。1.2後每個Node可以有多個Token，這個機制稱作Vnode，允許Node儲存大量的小段分割範圍(small partition ranges)。Vnode同時也使用consistent hashing，但不需要產生或指派token。

沒有Vnode時，每個Node依據分割鍵(Partition key)分配資料，再依據複製參數(Replication factor)另外儲存兩個複本。以一個六分割的Ring(ABCDEF)與六個Node(123456)為例：
Node1有分割A、以及兩個複本F與E。EFA的分割在環上必須連續。

使用Vnode時，Vnode是隨機選擇的，排列不連續。資料依據分割鍵hash後，放置於Node中更小的分割上。

### 資料複製(Data replication)

Cassandra儲存複本(replica)來確保可靠性(reliability)與故障容忍(fault tolerence)，複製策略決定複本該放在哪個Node上。由複本的總數可推論複製因數(Replication factor)，複製因數為1表示Cluster中一個資料列只有一份複本，儲存資料的Node故障則資料就無法取得。複製因數為2表示還有另一份資料放在另一個Node上。每一個複本都同等重要，無分主從(master & slave)。

* Simple Strategy

只使用單一datacenter與單一rack。放置第一份複本時，在下個順時針方向的Node上放置第二份複本，不考慮拓樸(Topology)(rack或datacenter地點)

* Network Topology Strategy

考量datacenter地點，避免遠距造成的延遲，也考慮了故障情境，適合擴展成多datacenter。沿著ring尋找下個rack的第一個Node，並試圖將資料放在不同的rack上(因為rack或實體機組可能因為相同原因一起故障)。提供兩個思考設定的方法：

** 每個datacenter兩份複本，複製群組中的一個Node故障時，仍能滿足本地讀取的consistent level of ONE。
** 每個datacenter三份複本，複製群組中的一個Node故障時，仍能滿足本地讀取的consistent level of LOCAL_QUORUM。複製群組中的多個Node故障時，仍能滿足本地讀取的consistent level of ONE。

也可設定不對稱的複製群組，如一個datacenter有三分複本來服務應用程式，另一個datacenter有一個複本做資料分析。


### 分割器(Partitioner)
http://docs.datastax.com/en/cassandra/3.0/cassandra/architecture/archPartitionerBOP.html

決定Cluster中資料分配到那些Node，基本上是一個將資料列的分割鍵轉為token的函數，一般使用hashing。

Murmur3Partitioner、RandomPartitionaer都使用token依照區塊平均分配資料，使用不同的分割鍵如usernames或timestamps依然有效。由於每個區塊資料量平均，連帶使得讀取與寫入附載均衡。

若使用vnode，則不需要計算token，若沒有使用vnode，則需要計算token並在cassandra.yaml中定義initial_token參數。不同分割器彼此不兼容，不同分割器產生的資料也不易轉換。

* Murmur3Partitioner有3-5倍的效能。使用MurmurHash函數，函數由token產生64位元的雜湊碼，可能範圍為-2^63到2^63-1。在新建的Cluster使用Murmur3Partitioner，不同分割器產生的資料也不易轉換。

* RandomPartitioner使用cryptographic hash(MD5 hash)，會花較多時間。範圍為0到2^127-1。可向前相容其他分割器的資料。

* ByteOrderedParittioner依照鍵值的位元碼依序排列資料，提供分割鍵的排序。例如可以使用16位元表示對照字母將A對應為41。因為鍵值有排序，類似傳統的index，可掃描資料列的特定排序部位並存取資料，可向前相容其他分割器的資料。存在幾個缺陷：

1. 附載均衡困難
2. 連續寫入造成負載集中(Hot spot)
3. 多表格的負載不均


### Snitches

Snitch判斷Node屬於哪個datacenter以及rack，告訴Cassandra網路分布(Topology)使得請求傳遞更有效率，並允許Cassandra考慮實體分布圖，將機器群組為datacenter與rack。更精確地說，Snitch提供資訊讓複製策略分配副本。 All nodes must return to the same rack and datacenter。Cassandra盡量避免相同rack上有多個複本。