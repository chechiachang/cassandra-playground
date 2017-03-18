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

