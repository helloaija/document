#### 1、安装依赖包libaio 
\> yum install libaio

#### 2、解压安装包
\> cd /usr/local  
\> tar -zxvf mysql-5.7.20-linux-glibc2.12-x86_64.tar.gz  
\> mkdir ./mysql  
\> mv ./mysql-5.7.20-linux-glibc2.12-x86_64/* /usr/local/mysql  

#### 3、创建用户
\> groupadd mysql  
\> useradd -r -g mysql mysql  
\> chown -R mysql mysql/  
\> chgrp -R mysql mysql/  

#### 4、创建配置文件
\> vi /etc/my.cnf 配置如下内容：  
```
[client]  
port = 3306  
socket = /tmp/mysql.sock  

[mysqld]  
character_set_server=utf8  
init_connect='SET NAMES utf8'  
basedir=/usr/local/mysql  
datadir=/usr/local/mysql/data  
socket=/tmp/mysql.sock  
log-error=/var/log/mysqld.log  
pid-file=/var/lib/mysqld/mysqld.pid  
\#不区分大小写  
lower_case_table_names = 1  
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION  
max_connections=5000  
default-time_zone = '+8:00'   
```

#### 5、初始化数据库
创建空日志文件  
\> vi /var/log/mysqld.log  
\> chmod 777 /var/log/mysqld.log  
\> chown mysql:mysql /var/log/mysqld.log  
\> /usr/local/mysql/bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data --lc_messages_dir=/usr/local/mysql/share --lc_messages=en_US

#### 6、启动服务
\> mkdir /var/lib/mysqld  
\> chmod 777 /var/lib/mysqld  
\> vi /var/lib/mysqld/mysqld.pid  
\> chmod 777 /var/lib/mysqld/mysqld.pid  
\> chown mysql:mysql /var/lib/mysqld/mysqld.pid  
\> /usr/local/mysql/support-files/mysql.server start  
\#获取初始化密码  
\> cat /var/log/mysqld.log
\> /usr/local/mysql/bin/mysql -uroot -p获取的密码  
\#修改密码  
\> set password = password('root')

#### 7、开机启动
\> cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld  
\#配置开机启动  
\> chkconfig --add mysqld  
\#映射mysql命令  
\> ln -s /usr/local/mysql/bin/mysql /usr/bin

#### 8、服务启停
\> service mysqld start/stop/restart

#### 9、配置远程连接
\> mysql -uroot -proot  
\#执行以下命令允许远程用户名root密码root登录  
`GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'root' WITH GRANT OPTION;`
