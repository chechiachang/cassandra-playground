# 架構

### Key structures

* Node
儲存資料的地方。是 Cassandra 的基本單元 。

* Data Center 
一個 Node 的集合。Data center 設定 Replication，將資料寫入多個 Data Center。

* Cluster 
一個 Cluster 包含多個 Data center。Cluster 可以分散到不同的實體地點。

* Commit log 
所有資料都會先寫入到 Commit log，然後才會 flush 到 SSTables

* Table 
一個欄位(column) 的排序集合。一個列(row)包含有多個欄位，以及一個主鍵(Primary Key)。

* SSTable 
一個排序過的子串表(Sorted String Table)，是一個不變(Immutable)的資料檔案。Cassandra 週期性地將 MemTable 的資料寫入 SSTable。SSTable 寫入時只能新增資料，在維護時才會整理。

### Key components

* Gossip
一個 P2P(peer-to-peer)的溝通協定，Node 會與 Cluster 中其他 Node 分享位置與狀態。
* Partitioner
一個計算 partition key 的 hash 函數，決定如何分配資料到 Node 中，以及哪個 Node 先放置第一筆資料。
* Replication factor
Cluster 中的 replica 數量。RF 為 1 表示每列資料只有存在一個 Node 中。
* Replica placement strategy
決定 replica 應該放在那些 Node 上。建立 keyspace 時需要定義。
* Snitch
* cassandra.yaml
* System keyspace table properties

### Internode communications (Gossip)

Node 週期性的分享所知的狀態訊息(包括自身與其他 Node)，Gossip 每秒執行訊息交換，最多同時與相同 Cluster 內的 Node 交換訊息。Gossip 訊息有時間版本，舊的訊息會被新的訊息取代。
對一個 Cluster 內的所有 Node 使用同一份 seed nodes 清單，以避免 Gossip 造成問題。 Seed nodes 只用來引導新 Node 加入 Cluster 。如果 Cluster 中有複數 Data center，最好每個 Data center 都有一個 Node 包含在 seed 清單內，否則引導新 Node 時就必須 Gossip 其他 Data center。不建議將所有 Node 放在 seed，因為會增加維護成本、降低 Gossip 效能。建議使用精簡的 seed 清單(每個 Data center 3 個左右)。

### Failure Detection & recovery

Failure detection 是使用本地的Gossip狀態與紀錄判斷另一個Node是在線或斷線，盡量避免將客戶端的請求送到離線的 Node。(透過Dynamic snitch也可以屏蔽在線的Node，但效能不佳)
Gossip程序追蹤狀態訊息(包含直接的一手訊息以及間接收到的第二手、第三手訊息)。 Cassandra計算帳戶網路效能、工作負擔、歷史狀態來精準的標記斷線的Node。每個Node在Gossip時會記錄Node間的回應時間。設定phi_convict_threshold來調整failure detection的敏銳度，數值越低則標記未回應的Node的機率越高，數值越高則降低被標記為斷線的機率。

硬體失效或是網路問題都可能使Node斷線，Node斷線可能都是過渡性的，而非長久性的斷線，其他的Node會嘗試重新建立連線。管理員必須使用nodetool-utility或是OpsCenter才能將Node移出cluster。