1、下载
https://tomcat.apache.org/download-80.cgi

2、发到服务器。
scp apache-tomcat-8.0.35.tar root@121.42.204.167:/download 

3、解压
tar xvf apache-tomcat-8.0.35.tar 

4、mv
mv apache-tomcat-8.0.35 /usr/local/tomcat8

5、server.xml

#tomcat启动脚本
[root@server1 tomcat]# vi /etc/init.d/tomcat
#!/bin/sh
#chkconfig: 2345 10 90
#description: Start and Stop the Tomcat
 
JAVA_HOME=/usr/java/jdk1.8.0_40
TOMCAT_HOME=/usr/local/tomcat
 
start_tomcat=$TOMCAT_HOME/bin/startup.sh
stop_tomcat=$TOMCAT_HOME/bin/shutdown.sh
 
start() {
    echo -n "Starting tomcat: "
    ${start_tomcat}
    echo "tomcat start ok"
}
 
stop() {
    echo -n "Shutdown tomcat"
    ${stop_tomcat}
    echo "tomcat stop ok"
}
 
case "$1" in
    start)
        start
        ;;
    stop)
        stop
        ;;
    restart)
        stop
        sleep 10
        start
        ;;
    *)
        echo "Usage: $0 {start|stop|restart}"
esac
exit 0
[root@server1 tomcat]# chmod a+x /etc/init.d/tomcat
[root@server1 tomcat]# /etc/init.d/tomcat restart


第二方法，使用YUM
How To Install Apache Tomcat 7 on CentOS 7 via Yum
https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-7-on-centos-7-via-yum

    sudo yum install tomcat
    sudo yum install tomcat-webapps tomcat-admin-webapps 
    sudo yum install tomcat-docs-webapp tomcat-javadoc
    
    sudo vi /usr/share/tomcat/conf/tomcat-users.xml
    <tomcat-users>
        <user username="admin" password="password" roles="manager-gui,admin-gui"/>
    </tomcat-users>

    启动：tomcat start
    关闭：tomcat stop
    http://server_IP_address:8080




    




