# Deloying-Web-on-Server-using-Tomcat  
## This work is based on [Install Java](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04), [Install Node.js](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04), and [Apache Tomcat 9](https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-8-on-ubuntu-16-04)  
creating a homepage and connecting to a dockercontainer  
`sudo apt update`  
`sudo apt install nodejs`  
`sudo apt install npm`  
`java -version`  
`sudo apt install default-jre`  
`sudo apt install default-jdk`  
`sudo update-alternatives --config java`  
`sudo groupadd tomcat`  
`sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat`  
`cd /tmp`  
`curl -O https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.54/bin/apache-tomcat-9.0.54.tar.gz`  
`sudo mkdir /opt/tomcat`  
`sudo tar xzvf apache-tomcat-8*tar.gz -C /opt/tomcat --strip-components=1`  
`cd /opt/tomcat`  
`sudo chgrp -R tomcat /opt/tomcat`  
`sudo chmod -R g+r conf`  
`sudo chmod g+x conf`  
`sudo chown -R tomcat webapps/ work/ temp/ logs/`  
`sudo nano /etc/systemd/system/tomcat.service`  
```service
[Unit]
Description=Apache Tomcat Web Application Container
After=network.target

[Service]
Type=forking

Environment=JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64/jre
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'
Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom'

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
```  
`sudo systemctl daemon-reload`  
`sudo systemctl start tomcat`  
`sudo systemctl status tomcat`  
``  
