###记录在使用Kafka遇到的错误以及解决方法

#### 1.主机名问题

~~~java
[2018-09-29 14:32:58,559] FATAL Fatal error during KafkaServerStartable startup. Prepare to shutdown (kafka.server.KafkaServerStartable)
java.net.UnknownHostException: dev: dev: No address associated with hostname
	at java.net.InetAddress.getLocalHost(InetAddress.java:1505)
	at kafka.server.KafkaHealthcheck$$anonfun$1.apply(KafkaHealthcheck.scala:55)
	at kafka.server.KafkaHealthcheck$$anonfun$1.apply(KafkaHealthcheck.scala:53)
	at scala.collection.MapLike$MappedValues.get(MapLike.scala:249)
	at scala.collection.MapLike$class.getOrElse(MapLike.scala:126)
	at scala.collection.AbstractMap.getOrElse(Map.scala:59)
	at kafka.server.KafkaHealthcheck.register(KafkaHealthcheck.scala:63)
	at kafka.server.KafkaHealthcheck.startup(KafkaHealthcheck.scala:45)
	at kafka.server.KafkaServer.startup(KafkaServer.scala:231)
	at kafka.server.KafkaServerStartable.startup(KafkaServerStartable.scala:37)
	at kafka.Kafka$.main(Kafka.scala:67)
	at kafka.Kafka.main(Kafka.scala)
Caused by: java.net.UnknownHostException: dev: No address associated with hostname
	at java.net.Inet6AddressImpl.lookupAllHostAddr(Native Method)
	at java.net.InetAddress$2.lookupAllHostAddr(InetAddress.java:928)
	at java.net.InetAddress.getAddressesFromNameService(InetAddress.java:1323)
	at java.net.InetAddress.getLocalHost(InetAddress.java:1500)
	... 11 more
~~~

使用的系统的hostname是dev

~~~bash
[root@dev kafka]# hostname
dev
~~~

Kafka通过主机名dev无法关联到IP地址，所以在/etc/hosts文件中加上下面一行，就可以解决这个问题

~~~bash
127.0.0.1    dev
~~~

