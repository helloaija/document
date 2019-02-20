#### 1、修改nginx配置文件   
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
```

#### 2、Nginx重启  
\> /usr/local/nginx/sbin/nginx -s reload   

