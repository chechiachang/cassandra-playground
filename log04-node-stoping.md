Node Stop
===

### 172.17.0.6(Stoping Node)
INFO  [StorageServiceShutdownHook] 2017-03-19 02:36:23,796 HintsService.java:221 - Paused hints dispatch
INFO  [StorageServiceShutdownHook] 2017-03-19 02:36:23,801 Server.java:176 - Stop listening for CQL clients
INFO  [StorageServiceShutdownHook] 2017-03-19 02:36:23,802 Gossiper.java:1506 - Announcing shutdown
INFO  [StorageServiceShutdownHook] 2017-03-19 02:36:23,807 StorageService.java:2248 - Node /172.17.0.6 state jump to shutdown
INFO  [StorageServiceShutdownHook] 2017-03-19 02:36:25,810 MessagingService.java:964 - Waiting for messaging service to quiesce
INFO  [ACCEPT-/172.17.0.6] 2017-03-19 02:36:25,812 MessagingService.java:1314 - MessagingService has terminated the accept() thread
INFO  [StorageServiceShutdownHook] 2017-03-19 02:36:26,005 HintsService.java:221 - Paused hints dispatch

### 172.17.0.2(Other Node)

INFO  [GossipStage:1] 2017-03-19 02:36:23,809 Gossiper.java:1035 - InetAddress /172.17.0.6 is now DOWN
INFO  [HANDSHAKE-/172.17.0.6] 2017-03-19 02:36:25,343 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.6


