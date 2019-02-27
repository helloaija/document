#打jar包 
cd /usr/local/qyj/qyj-store-1.0.0-SNAPSHOT  
jar -cvfM0 /usr/local/qyj/qyj-store-1.0.0-SNAPSHOT.jar ./  

#启动后台  
nohup java -jar -Dspring.profiles.active=prod /usr/local/qyj/qyj-store-1.0.0-SNAPSHOT.jar &
