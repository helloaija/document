#### 1、安装SVN服务器
\# 检查是否已安装  
\>rpm -qa subversion  
\>yum install httpd httpd-devel subversion mod_dav_svn mod_auth_mysql

#### 2、验证安装
\> cd /etc/httpd/modules  
\> ls | grep svn
```
mod_authz_svn.so
mod_dav_svn.so
```
\#查看版本  
\> svnserve --version

#### 3、建立SVN库
\> mkdir -p /usr/local/svn/repositories
\> svnadmin create /usr/local/svn/repositories

#### 4、修改svn配置
\> cd /usr/local/svn/repositories/conf  
\#添加用户密码shitl = 123456  
\> vi /usr/local/repositories/conf/passwd  

```
[users]
#harry = harryssecret
#sally = sallyssecret
shitl = 123456
shitl = hl1234
```
\#用户权限，追加repository库的根目录权限  
\> vi /usr/local/svn/repositories/conf/passwd  
```
[/]
zhoulf=rw  //给该用户访问所有库的权限
```
 或
```
[repositories:/project]
zhoulf=rw
```

\#配置svnserve.con服务  
\> vi /usr/local/svn/repositories/conf/svnserve.con
```
[general]
#匿名访问的权限，可以是read,write,none,默认为read
anon-access=none
#使授权用户有写权限
auth-access=write
#密码数据库的路径
password-db=passwd
#访问控制文件
authz-db=authz
#认证命名空间，subversion会在认证提示里显示，并且作为凭证缓存的关键字
realm=/usr/local/svn/repositories
```  

#### 5、配置防火墙端口  
\>vi /etc/sysconfig/iptables
\#打开3690端口，添加  
`-A INPUT -m state --state NEW -m tcp -p tcp --dport 3690 -j ACCEPT`  
\#重启防火墙  
\> service iptables restart

#### 6、服务启停
\#启动SVN  
\> svnserve -d -r /usr/local/svn/repositories  
\#查看SVN进程  
\> ps -ef|grep svn|grep -v grep  
\#检测SVN端口  
\> netstat -ln |grep 3690  
\#停止重启SVN：  
\> killall svnserve //停止

