# Cassandra on Docker

https://hub.docker.com/_/cassandra/

###Starting a cassandra instance
$ docker run --name some-cassandra -d cassandra:tag

###Make a Cluster
$ docker run --name some-cassandra2 -d -e CASSANDRA_SEEDS="$(docker inspect --format='{{ .NetworkSettings.IPAddress }}' some-cassandra)" cassandra:tag

Inspect instance
$ docker inspect cassandra

[cassandra.json](cassandra.json)

Inspect instance
$ docker inspect cassandra2

[cassandra2.json](cassandra2.json)

Hostconfig.PortBindings

Config.Env."CASSANDRA_SEEDS=172.17.0.2"