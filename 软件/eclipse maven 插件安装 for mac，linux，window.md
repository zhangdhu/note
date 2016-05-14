eclipse maven 插件安装 for mac，linux，window.md


1.打开eclipse，help－>install new software 

 add: 

name:maven名字随便取；

Location:http://download.eclipse.org/technology/m2e/releases ,  (参考http://www.eclipse.org/m2e/download/).

等待安装下载安装完毕。

2. 去http://maven.apache.org/download.cgi 下载，apache-maven-3.2.1-bin.tar.gz

解压，打开eclipse property  下面有一个maven，修改User settings  选择解压的maven，修改maven下的repository， 这个就是本地仓库的地址，如果不修改就用默认的地址

3.maven安装完毕，就可以使用maven了  创建maven project ，maven install project。