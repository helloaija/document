
#### 1、创建目录并解压 
\> mkdir /usr/local/java  
\#把压缩包放到创建的文件夹下并解压  
\> tar -zxvf jdk-linux-x64.tar.gz  

#### 2、编辑配置文件，配置环境变量
\> vi /etc/profile

```
export JAVA_HOME=/usr/local/java/jdk1.8.0_131
export JAVA_BIN=$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/lib/
export PATH=$PATH:$JAVA_HOME/bin
```

#### 3、执行命令是环境变量生效
\> source /etc/profile   

#### 4、查看安装情况
\> java -version
