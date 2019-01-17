
#### 1、下载zookeeper
\> wget http://mirror.bit.edu.cn/apache/zookeeper/current/zookeeper-3.4.10.tar.gz

#### 2、解压
\> tar -zxvf zookeeper-3.4.10.tar.gz  
生成zookeeper-3.4.10文件夹

#### 3、创建数据、日志目录
进入zookeeper-3.4.10目录，创建数据、日志文件夹  
\> mkdir ./logs  
\> mkdir ./data

#### 4、配置zoo.conf
进入conf目录，复制zoo_sample.cfg  
\> cp zoo_sample.cfg zoo.cfg  
编辑配置文件  
\> vi ./zoo.cg  
配置如下
```
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just
# example sakes.
dataDir=/opt/zoopeeker/zookeeper-3.4.10/data
dataLogDir=/opt/zoopeeker/zookeeper-3.4.10/logs
# the port at which the clients will connect
clientPort=2181
server.1=192.168.30.22:2888:3888
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1
```
#### 5、启动
进入bin目录  
\> ./zkServer.sh start
