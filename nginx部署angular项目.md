#### 1、修改nginx配置文件,跨域需要设置代理
\> vim /usr/local/nginx/conf/nginx.conf  
修改以下配置  
```
location / {
            #root   html;
            #index  index.html index.htm;
            #angular项目路径
            root /usr/local/my-app;
            index index.html index.html;
            #处理angular路由问题
            try_files $uri $uri/ /index.html;
        }
        
#设置代理
location /admin/ {
          # http://myserver/ #最后一个斜杠不可少，否则接口url会带上/api/目录
          proxy_pass   http://192.168.30.19:8080;
          proxy_set_header x-forwarded-host $host;
          proxy_set_header X-Real-IP $remote_addr;
          proxy_set_header REMOTE-HOST $remote_addr;
          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_redirect  off;
          client_max_body_size    2000m;
       }
       
 #压缩文件提升性能
 gzip on;
 gzip_static on;
 gzip_comp_level 2;
 gzip_http_version 1.0;
 gzip_proxied any;
 gzip_min_length 1100;
 gzip_buffers 16 8k;
 gzip_types text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
 
 # Disable for IE < 6 because there are some known problems
 gzip_disable "MSIE [1-6].(?!.*SV1)";
 
 # Add a vary header for downstream proxies to avoid sending cached gzipped files to IE6
 gzip_vary on;

```

#### 2、Nginx重启  
\> /usr/local/nginx/sbin/nginx -s reload   

