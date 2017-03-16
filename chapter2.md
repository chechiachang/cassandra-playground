# 架構

Key structures

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