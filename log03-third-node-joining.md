Third Node Joining
===

 $ docker run --name cassandra3 -d -e CASSANDRA_SEEDS="$(docker inspect --format='{{
.NetworkSettings.IPAddress }}' cassandra1)" cassandra$

 $ docker run --name cassandra4 -d -e CASSANDRA_SEEDS="$(docker inspect --format='{{
.NetworkSettings.IPAddress }}' cassandra1)" cassandra$

 $ docker run --name cassandra5 -d -e CASSANDRA_SEEDS="$(docker inspect --format='{{
.NetworkSettings.IPAddress }}' cassandra1)" cassandra$

### 172.17.0.2(Seeding Node)

INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:20:06,383 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:20:06,455 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [GossipStage:1] 2017-03-19 02:20:08,432 Gossiper.java:1056 - Node /172.17.0.4 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:20:08,436 Gossiper.java:1020 - InetAddress /172.17.0.4 is now UP
INFO  [STREAM-INIT-/172.17.0.4:49436] 2017-03-19 02:20:40,885 StreamResultFuture.java:116 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5 ID#0] Creating new streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.4:49436] 2017-03-19 02:20:40,887 StreamResultFuture.java:123 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.4:49438] 2017-03-19 02:20:40,889 StreamResultFuture.java:123 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-IN-/172.17.0.4:49438] 2017-03-19 02:20:40,935 StreamResultFuture.java:187 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] Session with /172.17.0.4 is complete
INFO  [STREAM-IN-/172.17.0.4:49438] 2017-03-19 02:20:40,936 StreamResultFuture.java:219 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] All sessions completed

### 172.17.0.3(Second Node)

INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:20:06,472 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:20:09,432 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [GossipStage:1] 2017-03-19 02:20:09,436 Gossiper.java:1056 - Node /172.17.0.4 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:20:09,440 Gossiper.java:1020 - InetAddress /172.17.0.4 is now UP
INFO  [STREAM-INIT-/172.17.0.4:41178] 2017-03-19 02:20:40,799 StreamResultFuture.java:116 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5 ID#0] Creating new streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.4:41178] 2017-03-19 02:20:40,802 StreamResultFuture.java:123 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.4:41180] 2017-03-19 02:20:40,804 StreamResultFuture.java:123 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-IN-/172.17.0.4:41180] 2017-03-19 02:20:40,851 StreamResultFuture.java:187 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] Session with /172.17.0.4 is complete
INFO  [STREAM-IN-/172.17.0.4:41180] 2017-03-19 02:20:40,851 StreamResultFuture.java:219 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] All sessions completed

### 172.17.0.4(Joining Node)

...Service initializeing before starting messaging service...

INFO  [main] 2017-03-19 02:20:06,329 MessagingService.java:733 - Starting Messaging Service on /172.17.0.4:7000 (eth0)
WARN  [main] 2017-03-19 02:20:06,333 SystemKeyspace.java:1082 - No host ID found, created 71e3610c-6732-4d61-9363-41665fd0f83a (Note: This should happen exactly once per node).
INFO  [HANDSHAKE-/172.17.0.2] 2017-03-19 02:20:06,362 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.2
INFO  [GossipStage:1] 2017-03-19 02:20:06,437 Gossiper.java:1056 - Node /172.17.0.3 is now part of the cluster
INFO  [GossipStage:1] 2017-03-19 02:20:06,453 Gossiper.java:1056 - Node /172.17.0.2 is now part of the cluster
INFO  [HANDSHAKE-/172.17.0.3] 2017-03-19 02:20:06,464 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.3
INFO  [RequestResponseStage-1] 2017-03-19 02:20:06,469 Gossiper.java:1020 - InetAddress /172.17.0.2 is now UP
INFO  [RequestResponseStage-1] 2017-03-19 02:20:06,481 Gossiper.java:1020 - InetAddress /172.17.0.3 is now UP
INFO  [main] 2017-03-19 02:20:07,390 StorageService.java:705 - Loading persisted ring state
INFO  [main] 2017-03-19 02:20:07,390 StorageService.java:818 - Starting up server gossip
INFO  [main] 2017-03-19 02:20:07,484 StorageService.java:1435 - JOINING: waiting for ring information
INFO  [HANDSHAKE-/172.17.0.2] 2017-03-19 02:20:08,435 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.2
INFO  [GossipStage:1] 2017-03-19 02:20:09,161 Gossiper.java:1056 - Node /172.17.0.3 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:20:09,184 Gossiper.java:1020 - InetAddress /172.17.0.3 is now UP
INFO  [GossipStage:1] 2017-03-19 02:20:09,262 TokenMetadata.java:479 - Updating topology for /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:20:09,266 TokenMetadata.java:479 - Updating topology for /172.17.0.3
INFO  [HANDSHAKE-/172.17.0.3] 2017-03-19 02:20:09,267 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:20:09,284 Gossiper.java:1056 - Node /172.17.0.2 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:20:09,298 Gossiper.java:1020 - InetAddress /172.17.0.2 is now UP
INFO  [GossipStage:1] 2017-03-19 02:20:09,358 TokenMetadata.java:479 - Updating topology for /172.17.0.2
INFO  [GossipStage:1] 2017-03-19 02:20:09,360 TokenMetadata.java:479 - Updating topology for /172.17.0.2
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,825 ViewManager.java:137 - Not submitting build tasks for views in keyspace system_traces as storage service is not initialized
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,831 ColumnFamilyStore.java:406 - Initializing system_traces.events
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,837 ColumnFamilyStore.java:406 - Initializing system_traces.sessions
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,842 ViewManager.java:137 - Not submitting build tasks for views in keyspace system_distributed as storage service is not initialized
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,846 ColumnFamilyStore.java:406 - Initializing system_distributed.parent_repair_history
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,852 ColumnFamilyStore.java:406 - Initializing system_distributed.repair_history
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,858 ColumnFamilyStore.java:406 - Initializing system_distributed.view_build_status
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,861 ViewManager.java:137 - Not submitting build tasks for views in keyspace system_auth as storage service is not initialized
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,865 ColumnFamilyStore.java:406 - Initializing system_auth.resource_role_permissons_index
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,871 ColumnFamilyStore.java:406 - Initializing system_auth.role_members
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,877 ColumnFamilyStore.java:406 - Initializing system_auth.role_permissions
INFO  [InternalResponseStage:1] 2017-03-19 02:20:09,883 ColumnFamilyStore.java:406 - Initializing system_auth.roles
INFO  [main] 2017-03-19 02:20:10,484 StorageService.java:1435 - JOINING: waiting for schema information to complete
INFO  [main] 2017-03-19 02:20:10,535 StorageService.java:1435 - JOINING: schema complete, ready to bootstrap
INFO  [main] 2017-03-19 02:20:10,535 StorageService.java:1435 - JOINING: waiting for pending range calculation
INFO  [main] 2017-03-19 02:20:10,536 StorageService.java:1435 - JOINING: calculation complete, ready to bootstrap
INFO  [main] 2017-03-19 02:20:10,536 StorageService.java:1435 - JOINING: getting bootstrap token
INFO  [main] 2017-03-19 02:20:10,610 StorageService.java:1435 - JOINING: sleeping 30000 ms for pending range setup
INFO  [main] 2017-03-19 02:20:40,611 StorageService.java:1435 - JOINING: Starting to bootstrap...
INFO  [main] 2017-03-19 02:20:40,792 StreamResultFuture.java:90 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] Executing streaming plan for Bootstrap
INFO  [StreamConnectionEstablisher:1] 2017-03-19 02:20:40,795 StreamSession.java:266 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] Starting streaming to /172.17.0.3
INFO  [StreamConnectionEstablisher:1] 2017-03-19 02:20:40,806 StreamCoordinator.java:264 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5, ID#0] Beginning stream session with /172.17.0.3
INFO  [STREAM-IN-/172.17.0.3:7000] 2017-03-19 02:20:40,850 StreamResultFuture.java:187 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] Session with /172.17.0.3 is complete
INFO  [StreamConnectionEstablisher:2] 2017-03-19 02:20:40,882 StreamSession.java:266 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] Starting streaming to /172.17.0.2
INFO  [StreamConnectionEstablisher:2] 2017-03-19 02:20:40,892 StreamCoordinator.java:264 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5, ID#0] Beginning stream session with /172.17.0.2
INFO  [STREAM-IN-/172.17.0.2:7000] 2017-03-19 02:20:40,934 StreamResultFuture.java:187 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] Session with /172.17.0.2 is complete
INFO  [STREAM-IN-/172.17.0.2:7000] 2017-03-19 02:20:40,940 StreamResultFuture.java:219 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] All sessions completed
INFO  [main] 2017-03-19 02:20:40,947 StorageService.java:1435 - JOINING: Finish joining ring

##### Bootstrap completed

INFO  [STREAM-IN-/172.17.0.2:7000] 2017-03-19 02:20:40,958 StorageService.java:1491 - Bootstrap completed! for the tokens [7750077046041942706, 8275947916307267888, -9072902505947422100, 2703933916141677023, 261275423039833571, 8101862698565466024, -9000643778586427211, 6675902450887888663, -8606522469744254320, 7547574079364415608, -8858879324692829045, -2639376406715973813, -4598749985891673758, -7937862333871472081, -3880925459810685232, -5076583757970028608, -2644098057455319657, -101857317728083249, 6871593105039665711, -8539422872572819966, -6079003618962656629, 4283564271965554006, -1091593588873242748, 5140313355886997356, 4488784778753654090, 8239340680731678386, 8183208694611027066, -3929688799371868661, 4606089215681682457, 2367275402638138160, -5775332312556908943, -4976761630620309997, 1185081238085258022, -148285919357726605, 4583575625330861209, 4709191376668268579, -719911141164200986, -6576287199492512743, 8752750671367730438, -896191886738664002, -537745992012129117, 1279142961850433571, -4680452899101419860, 6331244147183155098, 7408916195438484274, -3800050822908338450, 2387379210348987072, -4122060105216193665, -6186285207016380269, 4649338823143904270, -5282177523058019643, 5739428740081009138, 7072044680304890923, 6096106077908665862, 2543198215454725626, 4209170744959595056, 4039065874178002345, 5872172789766193854, 7099114022082999841, 6271852523636318500, -6897543374763972432, 8865922642710282252, -6976315411749874983, -3141782752856804442, -8532514845806261478, 7801677622419336409, 3069483589796845230, -4766125872533855672, 3272341869294783104, -6674427699923814519, 6582717258390101125, -938858775440927477, 749676202330707998, -1012325467017806986, -5476323202430290826, 8885170449619470581, -4888102594475164530, 5707621033225805133, -8714532444093635758, 7726531307937962875, 5597508261584492576, -7077843258068894020, 4903718826874629786, 7416143273775531965, 3781422209765369209, -4563902354997163484, 8923102560630432055, 2470358840351542859, -2215646973748028639, 6681898910482012652, 450359299025901132, -2896215320905603428, -5395675944342118749, 2413206257788846791, 5395136921580640112, -4851189332650845640, 7602379805882081836, 2112633892615863061, -1446671369580464563, -1101305310603726620, -8015262202372459897, -983937516875142675, 8469113789104283836, -63723710052067626, -2655013284404889210, -8424921767259791472, 1556700940715118786, 3434450656118213442, 4686724937470212933, -8004497625137101357, -1880723017853025625, 5819093439614202303, -3725475943017386270, 5169504855195272847, 2998248709052156798, 1431919046310299023, -8020954706650624800, 5799284062576275394, -1705227894307210684, 342256539531423236, -2796677572272205787, -603652276453666274, -1234259971755503570, -8381150929712497300, -3249754477566953740, -303216122481989380, 1220877069158937244, 3988379552268705243, -5306866043155851572, -6016892367359778558, -1481843267167832225, 2482381920282867447, -5025827042264353047, 1833587704237771680, 5277897635102417650, -3216952390026152531, 7296976789939467630, 1914136057777064075, 8141428984220465132, -2897770290064931229, 792862169121342391, 6834055771907640197, -2887351274962431567, 8879521069764709776, 6643601991886219409, 682623823829568052, 7129922007433310444, -6150089102348689737, 5399683294301342429, -8184343529153325397, 8761690019673193632, -6193386152553382652, -8858627289448134250, 2528171617040805479, 6884438911943805511, -2264050474893765679, -7509522477877021005, -1910628556611037105, -250323877408502723, -6126074403027055111, -5857279121215943227, 8549280305646768534, -592817710157240216, -7809936135880473352, 5870541650833928610, -5244998908125200177, -4707072186306170325, 2434080380594168766, 2260802196402994073, -6749498002519297030, 2211507336861226513, -5172712751157595042, 4739724530217774101, -6160162425581842057, -3136673220034537451, 8765681532179315089, 8783338347636892609, 3549829936369217526, 1799771569131085262, -2565693716822540173, 8703322838194369471, -5942753819866428596, -7059486066772172160, 6873270134788927404, 6106991671986564135, -8790151472079978377, 3409760091971854807, -6890463056980278283, 5822000205096984806, -6655372506131697871, 4731168016463419158, -8567212716811841486, -3576352614418811932, 6784498694406504714, -8053969226341081580, 4076950282108984759, -4124278822212484004, -867986625104084399, 1278335613165594421, 6234114358451311184, 3354121192807294096, -4116444272747730492, 3522956066928008708, 1522249298857250534, 2723985885919835534, -4444421033764128916, -7400314334499224967, -4436467998037958747, -1826027345184743205, -128056294656793251, -7203847403628470833, 2495434649754910022, -7617848887245334016, -5673082112117715820, -6761053589057654591, -4861209638872652572, 6579590103457336554, -3651359974612270658, 2201669766905752810, 7532140841294498460, 5648885259834168242, -3757017283535510765, -2968365990613134452, -9166244985169680523, -837679893236227752, 1025836250743507990, -6438791119512984440, -8687213646236073043, 7763137775212657454, -1091098430555852440, -8721137972130670608, 2164516567420337686, 1914453780546226828, 405249900870195788, -4587561226988811996, -7165247645297239495, 5811005540529028797, 1148518489190353780, -8722462705697946877, 6849679175345307622, -2827833233128477984, 6228761006518544100, -1177011653269590986, -1129022463774415628, -3680816623985586121, -5040868651382601287, 607126985317237795, 4951576828254145436, 5716570686232819248, 2845076169404105596, 6290007390753132735, 6002638468516536918, -8585107463368870834, 5129144523056807271, 270754998504903944, 7080909706533577451]
INFO  [main] 2017-03-19 02:20:41,074 CassandraDaemon.java:694 - Waiting for gossip to settle before accepting client requests...
INFO  [main] 2017-03-19 02:20:49,075 CassandraDaemon.java:725 - No gossip backlog; proceeding
INFO  [main] 2017-03-19 02:20:49,164 NativeTransportService.java:70 - Netty using native Epoll event loop
INFO  [main] 2017-03-19 02:20:49,233 Server.java:155 - Using Netty Version: [netty-buffer=netty-buffer-4.0.39.Final.38bdf86, netty-codec=netty-codec-4.0.39.Final.38bdf86, netty-codec-haproxy=netty-codec-haproxy-4.0.39.Final.38bdf86, netty-codec-http=netty-codec-http-4.0.39.Final.38bdf86, netty-codec-socks=netty-codec-socks-4.0.39.Final.38bdf86, netty-common=netty-common-4.0.39.Final.38bdf86, netty-handler=netty-handler-4.0.39.Final.38bdf86, netty-tcnative=netty-tcnative-1.1.33.Fork19.fe4816e, netty-transport=netty-transport-4.0.39.Final.38bdf86, netty-transport-native-epoll=netty-transport-native-epoll-4.0.39.Final.38bdf86, netty-transport-rxtx=netty-transport-rxtx-4.0.39.Final.38bdf86, netty-transport-sctp=netty-transport-sctp-4.0.39.Final.38bdf86, netty-transport-udt=netty-transport-udt-4.0.39.Final.38bdf86]
INFO  [main] 2017-03-19 02:20:49,233 Server.java:156 - Starting listening for CQL clients on /0.0.0.0:9042 (unencrypted)...
INFO  [main] 2017-03-19 02:20:49,268 CassandraDaemon.java:528 - Not starting RPC server as requested. Use JMX (StorageService->startRPCServer()) or nodetool (enablethrift) to start it


### 172.17.0.5(Fourth Node Joining)

...Service initializeing before starting messaging service...

INFO  [main] 2017-03-19 02:27:16,887 MessagingService.java:733 - Starting Messaging Service on /172.17.0.5:7000 (eth0)
WARN  [main] 2017-03-19 02:27:16,895 SystemKeyspace.java:1082 - No host ID found, created 5a705a90-84cf-424c-a242-9e19e6cdfd23 (Note: This should happen exactly once per node).
INFO  [HANDSHAKE-/172.17.0.2] 2017-03-19 02:27:16,931 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.2
INFO  [GossipStage:1] 2017-03-19 02:27:17,037 Gossiper.java:1056 - Node /172.17.0.4 is now part of the cluster
INFO  [GossipStage:1] 2017-03-19 02:27:17,043 Gossiper.java:1056 - Node /172.17.0.3 is now part of the cluster
INFO  [GossipStage:1] 2017-03-19 02:27:17,056 Gossiper.java:1056 - Node /172.17.0.2 is now part of the cluster
INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:27:17,059 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [HANDSHAKE-/172.17.0.3] 2017-03-19 02:27:17,062 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.3
INFO  [RequestResponseStage-1] 2017-03-19 02:27:17,078 Gossiper.java:1020 - InetAddress /172.17.0.2 is now UP
INFO  [RequestResponseStage-1] 2017-03-19 02:27:17,123 Gossiper.java:1020 - InetAddress /172.17.0.3 is now UP
INFO  [RequestResponseStage-1] 2017-03-19 02:27:17,160 Gossiper.java:1020 - InetAddress /172.17.0.4 is now UP
INFO  [main] 2017-03-19 02:27:17,936 StorageService.java:705 - Loading persisted ring state
INFO  [main] 2017-03-19 02:27:17,938 StorageService.java:818 - Starting up server gossip
INFO  [main] 2017-03-19 02:27:18,063 StorageService.java:1435 - JOINING: waiting for ring information
INFO  [HANDSHAKE-/172.17.0.2] 2017-03-19 02:27:19,004 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.2
INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:27:19,333 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [GossipStage:1] 2017-03-19 02:27:19,504 Gossiper.java:1056 - Node /172.17.0.4 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:27:19,507 Gossiper.java:1020 - InetAddress /172.17.0.4 is now UP
INFO  [GossipStage:1] 2017-03-19 02:27:19,583 TokenMetadata.java:479 - Updating topology for /172.17.0.4
INFO  [GossipStage:1] 2017-03-19 02:27:19,584 TokenMetadata.java:479 - Updating topology for /172.17.0.4
INFO  [GossipStage:1] 2017-03-19 02:27:19,592 Gossiper.java:1056 - Node /172.17.0.3 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:27:19,595 Gossiper.java:1020 - InetAddress /172.17.0.3 is now UP
INFO  [GossipStage:1] 2017-03-19 02:27:19,626 TokenMetadata.java:479 - Updating topology for /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:27:19,628 TokenMetadata.java:479 - Updating topology for /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:27:19,632 Gossiper.java:1056 - Node /172.17.0.2 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:27:19,635 Gossiper.java:1020 - InetAddress /172.17.0.2 is now UP
INFO  [HANDSHAKE-/172.17.0.3] 2017-03-19 02:27:19,636 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:27:19,809 TokenMetadata.java:479 - Updating topology for /172.17.0.2
INFO  [GossipStage:1] 2017-03-19 02:27:19,811 TokenMetadata.java:479 - Updating topology for /172.17.0.2
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,324 ViewManager.java:137 - Not submitting build tasks for views in keyspace system_traces as storage service is not initialized
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,328 ColumnFamilyStore.java:406 - Initializing system_traces.events
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,333 ColumnFamilyStore.java:406 - Initializing system_traces.sessions
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,337 ViewManager.java:137 - Not submitting build tasks for views in keyspace system_distributed as storage service is not initialized
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,341 ColumnFamilyStore.java:406 - Initializing system_distributed.parent_repair_history
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,345 ColumnFamilyStore.java:406 - Initializing system_distributed.repair_history
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,349 ColumnFamilyStore.java:406 - Initializing system_distributed.view_build_status
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,352 ViewManager.java:137 - Not submitting build tasks for views in keyspace system_auth as storage service is not initialized
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,355 ColumnFamilyStore.java:406 - Initializing system_auth.resource_role_permissons_index
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,359 ColumnFamilyStore.java:406 - Initializing system_auth.role_members
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,363 ColumnFamilyStore.java:406 - Initializing system_auth.role_permissions
INFO  [InternalResponseStage:1] 2017-03-19 02:27:20,369 ColumnFamilyStore.java:406 - Initializing system_auth.roles
INFO  [main] 2017-03-19 02:27:21,064 StorageService.java:1435 - JOINING: waiting for schema information to complete
INFO  [main] 2017-03-19 02:27:21,342 StorageService.java:1435 - JOINING: schema complete, ready to bootstrap
INFO  [main] 2017-03-19 02:27:21,343 StorageService.java:1435 - JOINING: waiting for pending range calculation
INFO  [main] 2017-03-19 02:27:21,343 StorageService.java:1435 - JOINING: calculation complete, ready to bootstrap
INFO  [main] 2017-03-19 02:27:21,344 StorageService.java:1435 - JOINING: getting bootstrap token
INFO  [main] 2017-03-19 02:27:21,384 StorageService.java:1435 - JOINING: sleeping 30000 ms for pending range setup

##### Sleeping before starting to bootstrap

INFO  [main] 2017-03-19 02:27:51,385 StorageService.java:1435 - JOINING: Starting to bootstrap...
INFO  [main] 2017-03-19 02:27:51,711 StreamResultFuture.java:90 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] Executing streaming plan for Bootstrap
INFO  [StreamConnectionEstablisher:1] 2017-03-19 02:27:51,715 StreamSession.java:266 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] Starting streaming to /172.17.0.3
INFO  [StreamConnectionEstablisher:1] 2017-03-19 02:27:51,724 StreamCoordinator.java:264 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7, ID#0] Beginning stream session with /172.17.0.3
INFO  [STREAM-IN-/172.17.0.3:7000] 2017-03-19 02:27:51,825 StreamResultFuture.java:187 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] Session with /172.17.0.3 is complete
INFO  [StreamConnectionEstablisher:2] 2017-03-19 02:27:51,970 StreamSession.java:266 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] Starting streaming to /172.17.0.2
INFO  [StreamConnectionEstablisher:2] 2017-03-19 02:27:51,972 StreamCoordinator.java:264 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7, ID#0] Beginning stream session with /172.17.0.2
INFO  [STREAM-IN-/172.17.0.2:7000] 2017-03-19 02:27:52,118 StreamResultFuture.java:187 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] Session with /172.17.0.2 is complete
INFO  [StreamConnectionEstablisher:1] 2017-03-19 02:27:52,139 StreamSession.java:266 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] Starting streaming to /172.17.0.4
INFO  [StreamConnectionEstablisher:1] 2017-03-19 02:27:52,152 StreamCoordinator.java:264 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7, ID#0] Beginning stream session with /172.17.0.4
INFO  [STREAM-IN-/172.17.0.4:7000] 2017-03-19 02:27:52,324 StreamResultFuture.java:187 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] Session with /172.17.0.4 is complete
INFO  [STREAM-IN-/172.17.0.4:7000] 2017-03-19 02:27:52,329 StreamResultFuture.java:219 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] All sessions completed
INFO  [main] 2017-03-19 02:27:52,337 StorageService.java:1435 - JOINING: Finish joining ring
INFO  [STREAM-IN-/172.17.0.4:7000] 2017-03-19 02:27:52,350 StorageService.java:1491 - Bootstrap completed! for the tokens [-5722919036896125793, 8502959077749951691, -4298403745219999689, 6805002453767038397, -268576207608015508, -2101638409501465953, -2513164605494880140, 2913060913160879368, -583529816506994166, 6392888426179246489, 1838036496312383241, 6213544200155227095, 808117275151857412, -5580668565525824075, -6643089334670368918, 8793723667903718747, 848239936321100007, -4011396460253484273, -2744711619049142483, -7210750791812235339, -7272186532873057690, 6410880353242561513, 7845868464939084327, 8705379598949014580, -8128999485591754512, -790222358465215544, 689556656487343601, -4505917635505690100, 3889619538887599429, 6372613524804559019, -649559324638194799, 3591176585387941452, 7040489264982132250, -6508405428573519986, 2642970594416535377, 2265477207814749248, 1549893889439828582, 9016895847678994436, 7519746162368674373, 3803673213899990532, 8056737554601684743, 5560716346687718497, -6480663294414495034, 6879418202751523081, -1911640586306805557, 5267658905303658497, 181345765627981327, -6533827232764225810, -7265021007519508585, -4779416637561471340, 4953671972730320620, 1183451061432608204, 5939576891568733102, 229493333350628112, 6222077302618552316, -1992797816556514243, -3795912145198944787, -5596473247473112478, 6415243302044939444, 5692761542251748335, -2360023610600642346, -948069775233633320, 408545182315303658, 5766610186939536310, 594119125574209641, 1771193348541779525, -4010043175210114239, 2886768583607178848, -8453278019794340152, -8857823549149019631, -5527023426508742896, -1013019470445579046, 1745568360283118158, 3591695770578565520, 1280704844138545129, 1373173662271886621, -6038885876900506659, 3514984788627357018, 133970652833442987, -9097698554352819083, 1992748235508336818, -480898179259682226, 652657608732816247, -5871872218973057833, 3561534511937982037, -3461769481946891287, 6165617495214375014, 2804551979561312437, 8896164657262747841, 4297383100772609397, -8018612391594281999, 5609594202592195268, -3978287091105722736, 3254495049313121806, 7800583623012270049, 8899737076896261704, 4863280054759696262, 6633752584628311806, -717456131370079227, 7010276419678266609, 3769486675653796172, 9007582409672192045, 820814142036623618, 7435810331484211372, -8198894722109659774, -8759086214466379672, -1144563705334722263, -4970881098917401479, -512006489167183744, -1487291002182762381, -4509530564623981636, 6717230473882811989, 1767134384385252013, 903443422107667468, 1240314838809485555, 7200523533041208525, 2137462005239177276, 1515666634119806906, 4595804955722844600, 1412223954049147172, 5209485036370197537, -5880290303905646062, 1754436422180160261, 6999470516567350620, 8629319207681330284, -6718631783129517527, -7296369467666055972, -490982332369633761, 5516338039257140058, 8369167465543452448, 3590228838309025030, 4861018907705426098, -1973041787299597727, 1851973684857976234, 5419491894382033074, 5246813412952666885, -4401183184728377840, -8779380925829792592, 16197604201377828, -8006789066588569977, -7747704795578190804, 7403374172199145787, 7633842162931211062, 3394806672735219998, -2790195848107245556, 1880737549327879821, -17980970313067694, 6135233497613260057, 2341862010228718321, 4629054828872371559, 5394777915607882728, -7764977550209649707, -8231100138285531101, 5669034822396677365, -7681474112269291151, 3754663538795544761, -4490870686486809161, -290450928535404763, 5477670322177937787, -5799121056975248040, -1825991537564091094, -8346511188197629814, 7144089439591563616, -6404036699078745034, -4010822116826901290, 8666160224061978647, -8334736044398196314, -1482169544102784423, 3071035363978083108, 6978798574433638876, 1389849384609184844, -8468084462036414604, -3968956393055890322, -3360634492922349120, -1140879220946722100, -6403010611246228446, 1841453387648861065, 2604333172939790252, -3847521464409507761, -5318015976110455831, 4267385850354772330, 935438644383879748, -4541125292243561389, 6075672283354993128, 7497991254924372198, 859135668373686920, -6237932276670090349, 2037315823213606183, 8778849188997131420, -3802931421552342645, 4303218321917477541, 4763156764043338248, 5256430021209712349, -7314517522843868315, 8951135358881063697, 7112125225282419717, -9160181305023061727, -5111133507593505293, 6067008974357309589, 2499032205471258322, -8065730107185964108, 3954831865875313201, 5564331724228780941, 8650093721274359705, -7688683136033586772, 7700133949689606741, -4342025966921975186, -136972347727425925, 4912703657732651408, -1803349373439258075, 4429750914302990421, 9016413035867108962, -2426950121324263257, -5483490734340195598, -2405619769514729513, -4976616121154167232, 560936772083217927, 534061622144027901, 6927796254391013679, -3895529919452833934, 7987383572718340291, 4170722094943052811, 9130393609793616040, -4532843201495739403, 698225772930984004, -4585638549209888368, -7713089424804703607, 7162108300618277401, 4286466075974122669, 6657535461993407805, 7168699599386684434, 115136001005898515, -299180926752024103, -6781602948158304386, -9174471045786051183, 8277239846532244363, 4568131624846989629, -9023115479113507971, 7968943282998322334, -4526640619071422209, 4796362452024763834, 1704861427142969405, 8886718567485746196, 6683348255499309503, -4687162853879743173, 3069520031307294275, 6595967414467678829, -7302012182827391198, -4281936167794886804, 4837870566862348369, -532736086967106192, -7771269785126425791, 7203331940886704113, 9107609428692547883, -9163286372020398533, -1040151532026325216]
INFO  [main] 2017-03-19 02:27:52,463 CassandraDaemon.java:694 - Waiting for gossip to settle before accepting client requests...
INFO  [main] 2017-03-19 02:28:00,465 CassandraDaemon.java:725 - No gossip backlog; proceeding
INFO  [main] 2017-03-19 02:28:00,546 NativeTransportService.java:70 - Netty using native Epoll event loop
INFO  [main] 2017-03-19 02:28:00,608 Server.java:155 - Using Netty Version: [netty-buffer=netty-buffer-4.0.39.Final.38bdf86, netty-codec=netty-codec-4.0.39.Final.38bdf86, netty-codec-haproxy=netty-codec-haproxy-4.0.39.Final.38bdf86, netty-codec-http=netty-codec-http-4.0.39.Final.38bdf86, netty-codec-socks=netty-codec-socks-4.0.39.Final.38bdf86, netty-common=netty-common-4.0.39.Final.38bdf86, netty-handler=netty-handler-4.0.39.Final.38bdf86, netty-tcnative=netty-tcnative-1.1.33.Fork19.fe4816e, netty-transport=netty-transport-4.0.39.Final.38bdf86, netty-transport-native-epoll=netty-transport-native-epoll-4.0.39.Final.38bdf86, netty-transport-rxtx=netty-transport-rxtx-4.0.39.Final.38bdf86, netty-transport-sctp=netty-transport-sctp-4.0.39.Final.38bdf86, netty-transport-udt=netty-transport-udt-4.0.39.Final.38bdf86]
INFO  [main] 2017-03-19 02:28:00,609 Server.java:156 - Starting listening for CQL clients on /0.0.0.0:9042 (unencrypted)...
INFO  [main] 2017-03-19 02:28:00,648 CassandraDaemon.java:528 - Not starting RPC server as requested. Use JMX (StorageService->startRPCServer()) or nodetool (enablethrift) to start it

### 172.17.0.2(Seeding Node)

##### 2nd Node Joining

INFO  [HANDSHAKE-/172.17.0.3] 2017-03-19 02:10:19,838 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.3
INFO  [HANDSHAKE-/172.17.0.3] 2017-03-19 02:10:19,867 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:10:21,864 Gossiper.java:1056 - Node /172.17.0.3 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:10:21,873 Gossiper.java:1020 - InetAddress /172.17.0.3 is now UP
WARN  [GossipTasks:1] 2017-03-19 02:10:21,921 FailureDetector.java:288 - Not marking nodes down due to local pause of 223309834300 > 5000000000
INFO  [STREAM-INIT-/172.17.0.3:34172] 2017-03-19 02:10:53,200 StreamResultFuture.java:116 - [Stream #47803560-0c49-11e7-afbc-f58bd8d3766a ID#0] Creating new streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.3:34172] 2017-03-19 02:10:53,213 StreamResultFuture.java:123 - [Stream #47803560-0c49-11e7-afbc-f58bd8d3766a, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.3:34174] 2017-03-19 02:10:53,214 StreamResultFuture.java:123 - [Stream #47803560-0c49-11e7-afbc-f58bd8d3766a, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-IN-/172.17.0.3:34174] 2017-03-19 02:10:53,414 StreamResultFuture.java:173 - [Stream #47803560-0c49-11e7-afbc-f58bd8d3766a ID#0] Prepare completed. Receiving 0 files(0.000KiB), sending 1 files(0.100KiB)
INFO  [STREAM-IN-/172.17.0.3:34174] 2017-03-19 02:10:53,523 StreamResultFuture.java:187 - [Stream #47803560-0c49-11e7-afbc-f58bd8d3766a] Session with /172.17.0.3 is complete
INFO  [STREAM-IN-/172.17.0.3:34174] 2017-03-19 02:10:53,527 StreamResultFuture.java:219 - [Stream #47803560-0c49-11e7-afbc-f58bd8d3766a] All sessions completed

##### 3rd Node Joining

INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:20:06,383 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:20:06,455 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [GossipStage:1] 2017-03-19 02:20:08,432 Gossiper.java:1056 - Node /172.17.0.4 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:20:08,436 Gossiper.java:1020 - InetAddress /172.17.0.4 is now UP
INFO  [STREAM-INIT-/172.17.0.4:49436] 2017-03-19 02:20:40,885 StreamResultFuture.java:116 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5 ID#0] Creating new streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.4:49436] 2017-03-19 02:20:40,887 StreamResultFuture.java:123 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.4:49438] 2017-03-19 02:20:40,889 StreamResultFuture.java:123 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-IN-/172.17.0.4:49438] 2017-03-19 02:20:40,935 StreamResultFuture.java:187 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] Session with /172.17.0.4 is complete
INFO  [STREAM-IN-/172.17.0.4:49438] 2017-03-19 02:20:40,936 StreamResultFuture.java:219 - [Stream #a5c20a80-0c4a-11e7-bc70-29ff21047bb5] All sessions completed

##### 4th Node Joining

INFO  [HANDSHAKE-/172.17.0.5] 2017-03-19 02:27:16,994 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.5
INFO  [HANDSHAKE-/172.17.0.5] 2017-03-19 02:27:17,060 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.5
INFO  [GossipStage:1] 2017-03-19 02:27:18,997 Gossiper.java:1056 - Node /172.17.0.5 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:27:19,018 Gossiper.java:1020 - InetAddress /172.17.0.5 is now UP
INFO  [STREAM-INIT-/172.17.0.5:43318] 2017-03-19 02:27:51,973 StreamResultFuture.java:116 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7 ID#0] Creating new streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.5:43318] 2017-03-19 02:27:51,995 StreamResultFuture.java:123 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.5:43320] 2017-03-19 02:27:52,003 StreamResultFuture.java:123 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-IN-/172.17.0.5:43320] 2017-03-19 02:27:52,123 StreamResultFuture.java:187 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] Session with /172.17.0.5 is complete
INFO  [STREAM-IN-/172.17.0.5:43320] 2017-03-19 02:27:52,128 StreamResultFuture.java:219 - [Stream #a685b330-0c4b-11e7-b874-fd3ad6a48af7] All sessions completed

##### 5th Node Joining

WARN  [GossipTasks:1] 2017-03-19 02:30:45,515 Gossiper.java:777 - Gossip stage has 1 pending tasks; skipping status check (no nodes will be marked down)
WARN  [GossipTasks:1] 2017-03-19 02:30:53,496 Gossiper.java:777 - Gossip stage has 4 pending tasks; skipping status check (no nodes will be marked down)
WARN  [GossipTasks:1] 2017-03-19 02:30:55,574 Gossiper.java:777 - Gossip stage has 7 pending tasks; skipping status check (no nodes will be marked down)

WARN  [GossipTasks:1] 2017-03-19 02:30:56,791 FailureDetector.java:288 - Not marking nodes down due to local pause of 12376376700 > 5000000000

WARN  [Service Thread] 2017-03-19 02:31:04,105 GCInspector.java:282 - ParNew GC in 1222ms.  CMS Old Gen: 30749664 -> 39206432; Par Eden Space: 167772160 -> 0; Par Survivor Space: 14629024 -> 9219584

INFO  [Service Thread] 2017-03-19 02:31:04,111 StatusLogger.java:47 - Pool Name                    Active   Pending      Completed   Blocked  All Time Blocked

INFO  [HANDSHAKE-/172.17.0.6] 2017-03-19 02:31:04,115 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.6
INFO  [HANDSHAKE-/172.17.0.6] 2017-03-19 02:31:04,151 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.6
INFO  [Service Thread] 2017-03-19 02:31:04,331 StatusLogger.java:51 - MutationStage                     0         0              1         0                 0
2017-03-19T02:31:04.332127400Z 
INFO  [Service Thread] 2017-03-19 02:31:04,333 StatusLogger.java:51 - ViewMutationStage                 0         0              0         0                 0
2017-03-19T02:31:04.334284400Z 
INFO  [Service Thread] 2017-03-19 02:31:04,335 StatusLogger.java:51 - ReadStage                         0         0             27         0                 0
2017-03-19T02:31:04.335334900Z 
INFO  [Service Thread] 2017-03-19 02:31:04,335 StatusLogger.java:51 - RequestResponseStage              0         0              3         0                 0
2017-03-19T02:31:04.336132800Z 
INFO  [Service Thread] 2017-03-19 02:31:04,336 StatusLogger.java:51 - ReadRepairStage                   0         0              0         0                 0
2017-03-19T02:31:04.337124300Z 
INFO  [Service Thread] 2017-03-19 02:31:04,338 StatusLogger.java:51 - CounterMutationStage              0         0              0         0                 0
2017-03-19T02:31:04.338550400Z 
INFO  [Service Thread] 2017-03-19 02:31:04,339 StatusLogger.java:51 - MiscStage                         0         0              0         0                 0
2017-03-19T02:31:04.339291500Z 
INFO  [Service Thread] 2017-03-19 02:31:04,341 StatusLogger.java:51 - CompactionExecutor                0         0            755         0                 0
2017-03-19T02:31:04.342276700Z 
INFO  [Service Thread] 2017-03-19 02:31:04,342 StatusLogger.java:51 - MemtableReclaimMemory             0         0             27         0                 0
2017-03-19T02:31:04.343253400Z 
INFO  [Service Thread] 2017-03-19 02:31:04,343 StatusLogger.java:51 - PendingRangeCalculator            0         0              7         0                 0
2017-03-19T02:31:04.344164400Z 
INFO  [Service Thread] 2017-03-19 02:31:04,351 StatusLogger.java:51 - GossipStage                       0         0           4465         0                 0
2017-03-19T02:31:04.351592200Z 
INFO  [Service Thread] 2017-03-19 02:31:04,353 StatusLogger.java:51 - SecondaryIndexManagement          0         0              0         0                 0
2017-03-19T02:31:04.353703300Z 
INFO  [Service Thread] 2017-03-19 02:31:04,381 StatusLogger.java:51 - HintsDispatcher                   0         0              0         0                 0
2017-03-19T02:31:04.382073300Z 
INFO  [Service Thread] 2017-03-19 02:31:04,434 StatusLogger.java:51 - MigrationStage                    0         0              9         0                 0
2017-03-19T02:31:04.572310100Z 
INFO  [Service Thread] 2017-03-19 02:31:05,160 StatusLogger.java:51 - MemtablePostFlush                 0         0             64         0                 0
2017-03-19T02:31:05.161010500Z 
INFO  [Service Thread] 2017-03-19 02:31:05,164 StatusLogger.java:51 - PerDiskMemtableFlushWriter_0         0         0             27         0                 0
2017-03-19T02:31:05.168923400Z 
INFO  [Service Thread] 2017-03-19 02:31:05,170 StatusLogger.java:51 - ValidationExecutor                0         0              0         0                 0
2017-03-19T02:31:05.170816700Z 
INFO  [Service Thread] 2017-03-19 02:31:05,172 StatusLogger.java:51 - Sampler                           0         0              0         0                 0
2017-03-19T02:31:05.173087500Z 
INFO  [Service Thread] 2017-03-19 02:31:05,182 StatusLogger.java:51 - MemtableFlushWriter               0         0             27         0                 0
2017-03-19T02:31:05.187447000Z 
INFO  [Service Thread] 2017-03-19 02:31:05,188 StatusLogger.java:51 - InternalResponseStage             0         0              0         0                 0
2017-03-19T02:31:05.189552500Z 
INFO  [Service Thread] 2017-03-19 02:31:05,190 StatusLogger.java:51 - AntiEntropyStage                  0         0              0         0                 0
2017-03-19T02:31:05.190828500Z 
INFO  [Service Thread] 2017-03-19 02:31:05,217 StatusLogger.java:51 - CacheCleanupExecutor              0         0              0         0                 0
2017-03-19T02:31:05.218705500Z 
INFO  [Service Thread] 2017-03-19 02:31:05,219 StatusLogger.java:51 - Native-Transport-Requests         0         0            211         0                 0
2017-03-19T02:31:05.220053700Z 
INFO  [Service Thread] 2017-03-19 02:31:05,225 StatusLogger.java:61 - CompactionManager                 0         0
INFO  [Service Thread] 2017-03-19 02:31:05,235 StatusLogger.java:73 - MessagingService                n/a       0/0
INFO  [Service Thread] 2017-03-19 02:31:05,236 StatusLogger.java:83 - Cache Type                     Size                 Capacity               KeysToSave
INFO  [Service Thread] 2017-03-19 02:31:05,237 StatusLogger.java:85 - KeyCache                        896                 76546048                      all
INFO  [Service Thread] 2017-03-19 02:31:05,244 StatusLogger.java:91 - RowCache                          0                        0                      all
INFO  [Service Thread] 2017-03-19 02:31:05,245 StatusLogger.java:98 - Table                       Memtable ops,data
INFO  [Service Thread] 2017-03-19 02:31:05,252 StatusLogger.java:101 - system_distributed.parent_repair_history                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,253 StatusLogger.java:101 - system_distributed.repair_history                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,253 StatusLogger.java:101 - system_distributed.view_build_status                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,253 StatusLogger.java:101 - system.compaction_history               3,576
INFO  [Service Thread] 2017-03-19 02:31:05,253 StatusLogger.java:101 - system.schema_aggregates                  0,0
INFO  [Service Thread] 2017-03-19 02:31:05,253 StatusLogger.java:101 - system.schema_triggers                    0,0
INFO  [Service Thread] 2017-03-19 02:31:05,253 StatusLogger.java:101 - system.size_estimates             5454,258354
INFO  [Service Thread] 2017-03-19 02:31:05,253 StatusLogger.java:101 - system.paxos                              0,0
INFO  [Service Thread] 2017-03-19 02:31:05,254 StatusLogger.java:101 - system.views_builds_in_progress                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,254 StatusLogger.java:101 - system.batches                            0,0
INFO  [Service Thread] 2017-03-19 02:31:05,254 StatusLogger.java:101 - system.schema_keyspaces                   0,0
INFO  [Service Thread] 2017-03-19 02:31:05,255 StatusLogger.java:101 - system.sstable_activity                16,181
INFO  [Service Thread] 2017-03-19 02:31:05,255 StatusLogger.java:101 - system.batchlog                           0,0
INFO  [Service Thread] 2017-03-19 02:31:05,255 StatusLogger.java:101 - system.schema_columns                     0,0
INFO  [Service Thread] 2017-03-19 02:31:05,256 StatusLogger.java:101 - system.hints                              0,0
INFO  [Service Thread] 2017-03-19 02:31:05,256 StatusLogger.java:101 - system.IndexInfo                          0,0
INFO  [Service Thread] 2017-03-19 02:31:05,257 StatusLogger.java:101 - system.schema_columnfamilies                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,257 StatusLogger.java:101 - system.schema_functions                   0,0
INFO  [Service Thread] 2017-03-19 02:31:05,257 StatusLogger.java:101 - system.built_views                        0,0
INFO  [Service Thread] 2017-03-19 02:31:05,257 StatusLogger.java:101 - system.peer_events                        0,0
INFO  [Service Thread] 2017-03-19 02:31:05,257 StatusLogger.java:101 - system.range_xfers                        0,0
INFO  [Service Thread] 2017-03-19 02:31:05,258 StatusLogger.java:101 - system.peers                         21,27724
INFO  [Service Thread] 2017-03-19 02:31:05,258 StatusLogger.java:101 - system.transferred_ranges                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,258 StatusLogger.java:101 - system.schema_usertypes                   0,0
INFO  [Service Thread] 2017-03-19 02:31:05,258 StatusLogger.java:101 - system.local                             1,61
INFO  [Service Thread] 2017-03-19 02:31:05,258 StatusLogger.java:101 - system.available_ranges                   0,0
INFO  [Service Thread] 2017-03-19 02:31:05,258 StatusLogger.java:101 - system.prepared_statements                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,259 StatusLogger.java:101 - system_schema.columns                     0,0
INFO  [Service Thread] 2017-03-19 02:31:05,260 StatusLogger.java:101 - system_schema.types                       0,0
INFO  [Service Thread] 2017-03-19 02:31:05,260 StatusLogger.java:101 - system_schema.indexes                     0,0
INFO  [Service Thread] 2017-03-19 02:31:05,264 StatusLogger.java:101 - system_schema.keyspaces                   0,0
INFO  [Service Thread] 2017-03-19 02:31:05,264 StatusLogger.java:101 - system_schema.dropped_columns                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,264 StatusLogger.java:101 - system_schema.aggregates                  0,0
INFO  [Service Thread] 2017-03-19 02:31:05,264 StatusLogger.java:101 - system_schema.triggers                    0,0
INFO  [Service Thread] 2017-03-19 02:31:05,265 StatusLogger.java:101 - system_schema.tables                      0,0
INFO  [Service Thread] 2017-03-19 02:31:05,265 StatusLogger.java:101 - system_schema.views                       0,0
INFO  [Service Thread] 2017-03-19 02:31:05,265 StatusLogger.java:101 - system_schema.functions                   0,0
INFO  [Service Thread] 2017-03-19 02:31:05,266 StatusLogger.java:101 - system_auth.roles                         0,0
INFO  [Service Thread] 2017-03-19 02:31:05,266 StatusLogger.java:101 - system_auth.role_members                  0,0
INFO  [Service Thread] 2017-03-19 02:31:05,266 StatusLogger.java:101 - system_auth.resource_role_permissons_index                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,267 StatusLogger.java:101 - system_auth.role_permissions                 0,0
INFO  [Service Thread] 2017-03-19 02:31:05,267 StatusLogger.java:101 - system_traces.sessions                    0,0
INFO  [Service Thread] 2017-03-19 02:31:05,267 StatusLogger.java:101 - system_traces.events                      0,0
INFO  [GossipStage:1] 2017-03-19 02:31:06,240 Gossiper.java:1056 - Node /172.17.0.6 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:31:06,244 Gossiper.java:1020 - InetAddress /172.17.0.6 is now UP
INFO  [STREAM-INIT-/172.17.0.6:52210] 2017-03-19 02:31:45,029 StreamResultFuture.java:116 - [Stream #317ccdc0-0c4c-11e7-82a5-a34111381c19 ID#0] Creating new streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.6:52210] 2017-03-19 02:31:45,032 StreamResultFuture.java:123 - [Stream #317ccdc0-0c4c-11e7-82a5-a34111381c19, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-INIT-/172.17.0.6:52212] 2017-03-19 02:31:45,034 StreamResultFuture.java:123 - [Stream #317ccdc0-0c4c-11e7-82a5-a34111381c19, ID#0] Received streaming plan for Bootstrap
INFO  [STREAM-IN-/172.17.0.6:52212] 2017-03-19 02:31:45,066 StreamResultFuture.java:187 - [Stream #317ccdc0-0c4c-11e7-82a5-a34111381c19] Session with /172.17.0.6 is complete
INFO  [STREAM-IN-/172.17.0.6:52212] 2017-03-19 02:31:45,067 StreamResultFuture.java:219 - [Stream #317ccdc0-0c4c-11e7-82a5-a34111381c19] All sessions completed