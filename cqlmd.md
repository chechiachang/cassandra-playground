# 使用CQL

* Keyspace
  類似SQL的database，但不是用來映射資料結構，Keyspace是用來定義Node中資料如何備份。基本上，一個Cluster中，每個application會有一個Keyspace。備份在建立Keyspace前就設定，所以不同備份需求的資料會放在不同的Keyspace中。

$ bin/nodetool status

* Compond Primary key
  \*\* Partition key
  將資料分配到Cluster中的不同的Node
  \*\* Cluster column
  資料升冪排列

\([https://docs.datastax.com/en/cql/3.1/cql/ddl/ddl\_compound\_keys\_c.html](https://docs.datastax.com/en/cql/3.1/cql/ddl/ddl_compound_keys_c.html)\)

