#### 1、安装编译工具及库文件   
\> yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel

#### 2、安装 PCRE，使Nginx 支持 Rewrite 功能  
\> cd /usr/local/src  
#下载 PCRE 安装包  
\> wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.42.tar.gz  
\> tar zxvf pcre-8.42.tar.gz  
\> cd pcre-8.42  
#编译安装  
\>  ./configure && make && make install  
#查看版本  
\> pcre-config --version  

#### 3、安装 Nginx  
\> cd /usr/local/src  
\> wget http://nginx.org/download/nginx-1.15.8.tar.gz  
\> tar zxvf nginx-1.15.8.tar.gz   
\> cd nginx-1.15.8    
\> ./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/usr/local/src/pcre-8.42   
\> make && make install
\> /usr/local/nginx/sbin/nginx -v


#### 4、Nginx操作  
#启动
\> /usr/local/nginx/sbin/nginx
#停止/重启
\> /usr/local/nginx/sbin/nginx -s stop(quit、reload)
#命令帮助
\> /usr/local/nginx/sbin/nginx -h
#验证配置文件
\> /usr/local/nginx/sbin/nginx -t
#配置文件
\> vim /usr/local/nginx/conf/nginx.conf
