Node Recovering
===

### 172.17.0.2(Cther Node)

[GossipStage:1] 2017-03-19 02:36:23,809 Gossiper.java:1035 - InetAddress /172.17.0.6 is now DOWN
INFO  [HANDSHAKE-/172.17.0.6] 2017-03-19 02:36:25,343 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.6
INFO  [HANDSHAKE-/172.17.0.6] 2017-03-19 02:38:33,449 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.6
INFO  [HANDSHAKE-/172.17.0.6] 2017-03-19 02:38:33,540 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.6
INFO  [GossipStage:1] 2017-03-19 02:38:35,639 Gossiper.java:1054 - Node /172.17.0.6 has restarted, now UP
INFO  [RequestResponseStage-1] 2017-03-19 02:38:35,643 Gossiper.java:1020 - InetAddress /172.17.0.6 is now UP
INFO  [GossipStage:1] 2017-03-19 02:38:35,648 StorageService.java:2248 - Node /172.17.0.6 state jump to NORMAL
INFO  [GossipStage:1] 2017-03-19 02:38:35,664 TokenMetadata.java:479 - Updating topology for /172.17.0.6
INFO  [GossipStage:1] 2017-03-19 02:38:35,665 TokenMetadata.java:479 - Updating topology for /172.17.0.6

### 172.17.0.6(Recovering Node)

...Service initializeing before starting messaging service...

INFO  [main] 2017-03-19 02:38:33,389 MessagingService.java:733 - Starting Messaging Service on /172.17.0.6:7000 (eth0)
INFO  [HANDSHAKE-/172.17.0.2] 2017-03-19 02:38:33,461 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.2
INFO  [GossipStage:1] 2017-03-19 02:38:33,527 Gossiper.java:1056 - Node /172.17.0.3 is now part of the cluster
INFO  [GossipStage:1] 2017-03-19 02:38:33,536 Gossiper.java:1056 - Node /172.17.0.2 is now part of the cluster
INFO  [GossipStage:1] 2017-03-19 02:38:33,538 Gossiper.java:1056 - Node /172.17.0.5 is now part of the cluster
INFO  [GossipStage:1] 2017-03-19 02:38:33,543 Gossiper.java:1056 - Node /172.17.0.4 is now part of the cluster
INFO  [HANDSHAKE-/172.17.0.3] 2017-03-19 02:38:33,546 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:38:33,551 Gossiper.java:1056 - Node /172.17.0.6 is now part of the cluster
INFO  [RequestResponseStage-1] 2017-03-19 02:38:33,557 Gossiper.java:1020 - InetAddress /172.17.0.2 is now UP
INFO  [HANDSHAKE-/172.17.0.5] 2017-03-19 02:38:33,558 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.5
INFO  [RequestResponseStage-1] 2017-03-19 02:38:33,561 Gossiper.java:1020 - InetAddress /172.17.0.3 is now UP
INFO  [GossipStage:1] 2017-03-19 02:38:33,564 Gossiper.java:1035 - InetAddress /172.17.0.6 is now DOWN
INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:38:33,568 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [HANDSHAKE-/172.17.0.6] 2017-03-19 02:38:33,576 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.6
INFO  [RequestResponseStage-1] 2017-03-19 02:38:33,577 Gossiper.java:1020 - InetAddress /172.17.0.5 is now UP
INFO  [RequestResponseStage-1] 2017-03-19 02:38:33,579 Gossiper.java:1020 - InetAddress /172.17.0.4 is now UP
INFO  [HANDSHAKE-/172.17.0.6] 2017-03-19 02:38:33,579 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.6
INFO  [RequestResponseStage-1] 2017-03-19 02:38:33,580 Gossiper.java:1020 - InetAddress /172.17.0.6 is now UP
INFO  [main] 2017-03-19 02:38:34,447 StorageService.java:705 - Loading persisted ring state
INFO  [main] 2017-03-19 02:38:34,478 StorageService.java:818 - Starting up server gossip
INFO  [main] 2017-03-19 02:38:34,540 TokenMetadata.java:479 - Updating topology for /172.17.0.6
INFO  [main] 2017-03-19 02:38:34,541 TokenMetadata.java:479 - Updating topology for /172.17.0.6
INFO  [main] 2017-03-19 02:38:34,572 StorageService.java:991 - Using saved tokens [-1003015985802709695, -1075742679806008946, -109813683696154332, -1165294533688115940, -1294931026951526242, -1359385803374741698, -1397486009055985549, -1506670834259418652, -1582709777049610893, -1617786277696369892, -1644222711963280614, -1784762645343000913, -1866274082365722240, -1933414902668436951, -1967121754473788913, -1968007768451161880, -2016517867447902537, -2037767127971128651, -2121696204901019256, -2216913552489380428, -2238863699705751395, -2347228750332406897, -239537787005787838, -2496564921887802878, -2579468518060463520, -2605459882464175675, -2670865424757155875, -2723225301194081246, -2757107071775378810, -2844707422788545471, -2896501480642728957, -2970341145667962371, -3031872774992154871, -3038122038093178468, -3043444904452639072, -3257497419535757029, -3294696830710312362, -3365994630697041249, -3392408894117899032, -3502611856513830297, -3530389398492167383, -3580066304253927050, -3745912149377987238, -3769057524712547419, -3862157726448293590, -3881486285790337056, -4055589820801818434, -4063205466668517135, -4115934265203955498, -4169438233928023548, -4194193667016207594, -4348200071222475014, -460822139987485105, -4654384014634809282, -479841537438211098, -4872464453025150223, -514955905236349553, -5198791947906320184, -5227235556101189256, -523528175627317399, -5354282288231418906, -5356262230375092063, -5403057390042234291, -5415433760612890081, -5443967212382065981, -5475658349933711317, -5482028763792798736, -5733872334997542637, -5740885848224027427, -5773412385075298111, -5941300211641579008, -5953480403554788137, -5967621347140303423, -6073143164008368475, -6166583488031330728, -621990496943092300, -6265082680146763322, -6327411289264781693, -6329661020979118876, -6335197057053788621, -6335976812350941212, -6364053191585582087, -6364385604580043430, -6428948358348702958, -6552565411539810267, -663737660363814844, -6733994888888566973, -6747362892106925414, -6876004723164768747, -6957466327921871129, -7183661650952284840, -7226379695288210281, -7490830758156246202, -7492288363471118509, -7494382088331274377, -7535650470399204150, -756100318954557929, -7688419076640327949, -7689768393292149775, -7709454635417905668, -7774437765683711113, -7822438300638419469, -8146665193302658656, -8159787643487021372, -8366385786979283104, -8374534783310328968, -8437813530579296178, -8442032607090481775, -8530221276085101446, -857881286215354031, -8606129496299936933, -864490934763185444, -8665268258826790050, -8667391246315263202, -8888910701756393223, -895632613386132809, -9001455476287747933, -9066036628919025780, -9184670761295966291, -9200843669298622572, -9220740371389683814, 1061518382839054529, 1342209434080606859, 1344359680309042381, 1383121825178267524, 1439092322890351874, 1515479642016343553, 158155310697737388, 1673137243101646254, 1796922506019651659, 1799084513172337810, 1811321716440986098, 1825496150109755415, 1829289347100464565, 1864564630176379269, 1882614753484000444, 1964944497666972282, 200567493176920685, 2079745859530909568, 2126134886468847041, 2132730338191213650, 2334527917376459298, 2402119852133855148, 2477799286274862177, 2519836076026886973, 2521931660218786494, 2824537223626774279, 2840716212835286422, 2851863154976486354, 2878519583664898648, 2937059299287392407, 2937536765207371480, 2978204757132450372, 3010033562332288023, 3016908569385769999, 3044226331918504129, 3075336988422656518, 3091276798885423247, 3115144445072054888, 3174261935637649406, 3190705236684554126, 3272427921795467256, 356303976049994721, 360653885496694900, 3628112222348245684, 3682305513909942705, 3925334180035509253, 4012622200873815874, 405463446916877032, 4171426138165697128, 4291666290173089843, 4361621967364377520, 4420535894817976315, 4504333351277690000, 4538149345617286669, 4593505631551248615, 4689235113416656981, 4787859873420798504, 4850672002141376162, 4890761377463545675, 5102655574534366062, 5125027815875610847, 5343981035989774005, 5415380555415324801, 5502220366737493330, 5606779591013461107, 5722142922176090192, 5775354262730559806, 5809067912068103071, 5848515549440889340, 5994821905396231300, 6029583806040321592, 6061861095137789002, 6088912910070950280, 6240354744849831099, 6297643594335549402, 6302431299760403035, 6317638879291806682, 6376124949833050178, 6438812231729294819, 6516227147126901897, 6572809559551694071, 6578672504863664130, 6654855897090231523, 6660443832992170949, 6662994624453238224, 6666671150710955477, 677398190025801837, 6872301607604634082, 6881832386574267014, 6956243965758329995, 6959243076835520715, 6981616019656671719, 7054958392429577389, 707318756870155982, 7097008886391816268, 7170250405370119028, 7258518415204884016, 7282230138388288982, 74084851872898324, 7409684569721792685, 7436743964517936703, 7557815752989295460, 7661624134856616333, 7697163352184944368, 7712775875130826083, 7719962793631882965, 7739646118724812433, 7951257172066486740, 7960105547365535340, 7966650488668924331, 8026487338551418100, 8033985498334410424, 8073372316873124648, 8209187892023835898, 8361613923924257048, 8362897222367517279, 836677935143327278, 8392970481381829996, 8540187731015709495, 8550557117822029711, 8582840192443497218, 8687977123749005151, 87008783579567373, 8722173758798527127, 8832446589888495588, 891021695838483107, 8915160369004421292, 892678148961780895, 8994949039916997659, 9036142777898368472, 910633091015901623, 9139191029846019241, 9214114367576957527, 92227174777238224, 978579181180752634]
INFO  [main] 2017-03-19 02:38:34,582 StorageService.java:1435 - JOINING: Finish joining ring
INFO  [main] 2017-03-19 02:38:34,692 StorageService.java:2248 - Node /172.17.0.6 state jump to NORMAL
INFO  [main] 2017-03-19 02:38:34,702 CassandraDaemon.java:694 - Waiting for gossip to settle before accepting client requests...
INFO  [GossipStage:1] 2017-03-19 02:38:35,541 Gossiper.java:1054 - Node /172.17.0.3 has restarted, now UP
INFO  [GossipStage:1] 2017-03-19 02:38:35,545 StorageService.java:2248 - Node /172.17.0.3 state jump to NORMAL
INFO  [RequestResponseStage-1] 2017-03-19 02:38:35,546 Gossiper.java:1020 - InetAddress /172.17.0.3 is now UP
INFO  [GossipStage:1] 2017-03-19 02:38:35,559 TokenMetadata.java:479 - Updating topology for /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:38:35,565 TokenMetadata.java:479 - Updating topology for /172.17.0.3
INFO  [GossipStage:1] 2017-03-19 02:38:35,568 Gossiper.java:1054 - Node /172.17.0.2 has restarted, now UP
INFO  [RequestResponseStage-1] 2017-03-19 02:38:35,573 Gossiper.java:1020 - InetAddress /172.17.0.2 is now UP
INFO  [GossipStage:1] 2017-03-19 02:38:35,577 StorageService.java:2248 - Node /172.17.0.2 state jump to NORMAL
INFO  [GossipStage:1] 2017-03-19 02:38:35,589 TokenMetadata.java:479 - Updating topology for /172.17.0.2
INFO  [GossipStage:1] 2017-03-19 02:38:35,593 TokenMetadata.java:479 - Updating topology for /172.17.0.2
INFO  [GossipStage:1] 2017-03-19 02:38:35,596 Gossiper.java:1054 - Node /172.17.0.5 has restarted, now UP
INFO  [RequestResponseStage-1] 2017-03-19 02:38:35,597 Gossiper.java:1020 - InetAddress /172.17.0.5 is now UP
INFO  [GossipStage:1] 2017-03-19 02:38:35,601 StorageService.java:2248 - Node /172.17.0.5 state jump to NORMAL
INFO  [GossipStage:1] 2017-03-19 02:38:35,613 TokenMetadata.java:479 - Updating topology for /172.17.0.5
INFO  [GossipStage:1] 2017-03-19 02:38:35,614 TokenMetadata.java:479 - Updating topology for /172.17.0.5
INFO  [GossipStage:1] 2017-03-19 02:38:35,620 Gossiper.java:1054 - Node /172.17.0.4 has restarted, now UP
INFO  [RequestResponseStage-1] 2017-03-19 02:38:35,620 Gossiper.java:1020 - InetAddress /172.17.0.4 is now UP
INFO  [GossipStage:1] 2017-03-19 02:38:35,622 StorageService.java:2248 - Node /172.17.0.4 state jump to NORMAL
INFO  [GossipStage:1] 2017-03-19 02:38:35,631 TokenMetadata.java:479 - Updating topology for /172.17.0.4
INFO  [GossipStage:1] 2017-03-19 02:38:35,632 TokenMetadata.java:479 - Updating topology for /172.17.0.4
INFO  [HANDSHAKE-/172.17.0.2] 2017-03-19 02:38:35,641 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.2
INFO  [HANDSHAKE-/172.17.0.4] 2017-03-19 02:38:41,060 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.4
INFO  [main] 2017-03-19 02:38:42,704 CassandraDaemon.java:725 - No gossip backlog; proceeding
INFO  [main] 2017-03-19 02:38:42,790 NativeTransportService.java:70 - Netty using native Epoll event loop
INFO  [main] 2017-03-19 02:38:42,861 Server.java:155 - Using Netty Version: [netty-buffer=netty-buffer-4.0.39.Final.38bdf86, netty-codec=netty-codec-4.0.39.Final.38bdf86, netty-codec-haproxy=netty-codec-haproxy-4.0.39.Final.38bdf86, netty-codec-http=netty-codec-http-4.0.39.Final.38bdf86, netty-codec-socks=netty-codec-socks-4.0.39.Final.38bdf86, netty-common=netty-common-4.0.39.Final.38bdf86, netty-handler=netty-handler-4.0.39.Final.38bdf86, netty-tcnative=netty-tcnative-1.1.33.Fork19.fe4816e, netty-transport=netty-transport-4.0.39.Final.38bdf86, netty-transport-native-epoll=netty-transport-native-epoll-4.0.39.Final.38bdf86, netty-transport-rxtx=netty-transport-rxtx-4.0.39.Final.38bdf86, netty-transport-sctp=netty-transport-sctp-4.0.39.Final.38bdf86, netty-transport-udt=netty-transport-udt-4.0.39.Final.38bdf86]
INFO  [main] 2017-03-19 02:38:42,861 Server.java:156 - Starting listening for CQL clients on /0.0.0.0:9042 (unencrypted)...
INFO  [main] 2017-03-19 02:38:42,907 CassandraDaemon.java:528 - Not starting RPC server as requested. Use JMX (StorageService->startRPCServer()) or nodetool (enablethrift) to start it
INFO  [HANDSHAKE-/172.17.0.5] 2017-03-19 02:38:46,308 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.5
INFO  [HANDSHAKE-/172.17.0.3] 2017-03-19 02:39:16,601 OutboundTcpConnection.java:510 - Handshaking version with /172.17.0.3