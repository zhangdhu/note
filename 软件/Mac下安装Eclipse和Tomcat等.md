Mac下安装Eclipse和Tomcat等.md

Mac下做Java开发还是很方便的，不用像.NET开发一样在Parallel Desktop里面安装Windows虚拟机，Mac下面默认已经安装了JDK。



当然，你如果要安装JDK7，请先阅读：http://www.oracle.com/technetwork/java/javase/downloads/jdk-for-mac-readme-1564562.html

然后下载Eclipse，Eclipse64位在Mac下的也是用Objective C写的。Eclipse Indigo Mac 64位版本 下载地址：http://www.eclipse.org/downloads/packages/release/indigo/sr2

下载Eclipse以后解压即可。Eclispe插件（比如SVN、Maven(Install new software from:  http://download.eclipse.org/m2e-wtp/releases/)、Egit等）的安装，自己谷歌搜索。

Maven 在Eclipse Indigo的安装方法：http://stackoverflow.com/questions/9108267/error-maven-installation-in-eclipse



下载Tomcat，tar.gz即可，地址：http://tomcat.apache.org/

下面Tomcat的步骤和Linux一样：

建立Tomcat目录：打开终端命令行，cd /Library, mkdir Tomcat, sudo chmod 755 /Library/Tomcat

把Tomcat解压以后复制到新建的Tomcat目录。修改/conf/tomcat-users.xml，里面加入两行：



保存以后bin启动./startup.sh，然后在浏览器输入http://localhost:8080，点击manager，输入上面图片的用户名和密码就可以部署网站了。

配置Tomcat启动脚本：

使用文本编辑器添加以下代码：

#!/bin/bash

case $1 in
start)
sh /Library/Tomcat/bin/startup.sh
;;
stop)
sh /Library/Tomcat/bin/shutdown.sh
;;
restart)
sh /Library/Tomcat/bin/shutdown.sh
sh /Library/Tomcat/bin/startup.sh
;;
*)
echo “Usage: start|stop|restart”
;;
esac

exit 0

将文件保存为tomcat，小写并不带后缀。赋予文件执行权限：

chmod 777 tomcat

。将这个文件放置到终端包含的路径中，例如/usr/bin，而后便可以在终端中简单地输入tomcat start和tomcat stop启用tomcat了。

快捷命令如下：

1）tomcat start 

2)  tomcat stop

3)  tomcat restart 

非常的方便！此外，MyEclipse也有Mac版的，ssh也是系统自带的，jboss和tomcat一样也是直接解压就可以用了。

Netbeans也有mac版本下载，下载地址：https://netbeans.org/downloads/index.html

数据库方面，可以安装Mac版的Oracle，客户端用sqlplus++或者Razorsql。或者用PostgreSQL数据库，下载地址：http://www.postgresql.org/download/macosx/。里面已经包含pgAdmin。

 

分类: Java
标签: Java, mac
好文要顶 关注我 收藏该文  
Mainz
关注 - 19
粉丝 - 881
荣誉：推荐博客
+加关注
0 0
(请您对文章做出评价)
« 上一篇：大量微软正版电子书下载
» 下一篇：为什么研发团队不适合量化KPI的绩效考核？
posted on 2013-07-06 11:06 Mainz 阅读(6844) 评论(2) 编辑 收藏
评论

#1楼 2013-10-25 12:05 hhb19900618  
大哥 我点击 startup.sh 后 
输出
Last login: Fri Oct 25 12:04:46 on ttys003
localhost:~ huabinko$ /Users/huabinko/Library/Tomcat/apache-tomcat-6.0.37/bin/startup.sh ; exit;
Using CATALINA_BASE: /Users/huabinko/Library/Tomcat/apache-tomcat-6.0.37
Using CATALINA_HOME: /Users/huabinko/Library/Tomcat/apache-tomcat-6.0.37
Using CATALINA_TMPDIR: /Users/huabinko/Library/Tomcat/apache-tomcat-6.0.37/temp
Using JRE_HOME: /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
Using CLASSPATH: /Users/huabinko/Library/Tomcat/apache-tomcat-6.0.37/bin/bootstrap.jar
logout

[进程已完成]

但是 输入 local8080 到浏览器访问没反应呢？ 咋回事