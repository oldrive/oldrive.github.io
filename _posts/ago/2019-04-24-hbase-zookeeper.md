---
layout: post
title:  zookeeper&hbase
date:   2019-04-24 22:42:00 +0800
categories: 技术
tag: hadoop
---

* content
{:toc}


现象
--------------------------


-----------------------


myid自动发生修改


思路
-----------------------------


-----------------------


启动zookeeper前确认myid的正确，然后正常启动zookeeper--->hbase,看上去没有报错，但重新cat myid却发现自己改了。查看hbase/logs/hbase-root-zookeeper-master.out中的日志，发现如下的报错信息：

```
java.net.BindException: Address already in use
	at sun.nio.ch.Net.bind0(Native Method)
	at sun.nio.ch.Net.bind(Net.java:444)
	at sun.nio.ch.Net.bind(Net.java:436)
	at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:214)
	at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
	at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:67)
	at org.apache.zookeeper.server.NIOServerCnxnFactory.configure(NIOServerCnxnFactory.java:95)
	at org.apache.zookeeper.server.quorum.QuorumPeerMain.runFromConfig(QuorumPeerMain.java:130)
	at org.apache.hadoop.hbase.zookeeper.HQuorumPeer.runZKServer(HQuorumPeer.java:89)
	at org.apache.hadoop.hbase.zookeeper.HQuorumPeer.main(HQuorumPeer.java:79)
```


仔细看下hbase启动的过程就知道，start-hbase.sh后，先启动zookeeper，再启动master，也就是说**启动了两遍zookeeper**，myid发生变化就不奇怪了


解决
----------------------------


-----------------------


在./hbase/conf/hbase-env.sh中设置HBASE_MANAGES_ZK 改成false（默认是true），让hbase启动时不启动zookeeper


感想
------------------------------


-----------------------


不学会看日志瞎几把百度你只会原地踏步，还解决不了问题


