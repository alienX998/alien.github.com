Hive

---

Hive-site.xml

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?> <?xml-stylesheet type="text/xsl" href="configuration.xsl"?> <configuration>
<property>
<name>javax.jdo.option.ConnectionUserName</name>
      <value>root</value>
  </property>
<property> <name>javax.jdo.option.ConnectionPassword</name> <value>123456</value>
  </property>
  <property>
<name>javax.jdo.option.ConnectionURL</name>
      <value>jdbc:mysql://node01:3306/hive?createDatabaseIfNotExist=true&amp;useSSL=false
  </property>
<property> <name>javax.jdo.option.ConnectionDriverName</name> <value>com.mysql.jdbc.Driver</value>
  </property>
  <property>
<name>hive.metastore.schema.verification</name>
      <value>false</value>
  </property>
<property> <name>datanucleus.schema.autoCreateAll</name> <value>true</value>
 </property>
 <property>
<name>hive.server2.thrift.bind.host</name> <value>node01</value>
 </property>
 <!--
<property>
<name>hive.metastore.uris</name> <value>thrift://node01:9083</value>
<description>JDBC connect string for a JDBC metastore</description>
  </property>
  <property>
<name>hive.metastore.local</name> <value>false</value>
<description>this is local store</description>
</property> -->
</configuration>
```

##### Hive 表操作

hive中外部表和内部表

区别：

- 内部表删除会删除表数据和元数据

- 外部表 只会删除表数据，不会删除元数据



```
load data local inpath ‘/export/servers/hivedatas/students.csv’ into table student
```

___

### flume

<img src="/Users/kongbaobao/Documents/markdown/markImg/1-案例1-采集网络数据.PNG" alt="1-案例1-采集网络数据" style="zoom:75%;" />

##### 实现步骤

1、写一个配置文件

​	1）配置3个组件的名字

​	2）配置channel

​	3）配置Sink

```
a1.sources = r1
a1.sinks = k1
a1.channels = c1

a1.sources.r1.type = netcat 
a1.sources.r1.bind = 192.168.1.100
a1.sources.r1.port = 44444

a1.sinks.k1.type = logger

a1.channels.c1.type = memory 
a1.channels.c1.capacity = 1000 
a1.channels.c1.transactionCapacity = 100

a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1
```

2、启动flume端Agent实例

3、运行测试

