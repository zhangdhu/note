安装步骤:
1、使用putty或类似的SSH工具登陆VPS或服务器；
登陆后运行：screen -S lnmt
如果提示screen: command not found 命令不存在可以执行：yum install screen 或 apt-get install screen安装。
2、下载并安装LNMT一键安装包：
建议您选择使用下载版，两者区别在于，一个是使用已经打包的安装包（包含所有程序版本），一个是在线下载的安装包（按选择的版本进行下载）。
执行安装程序前需要您确认您的Linux发行版，可以执行：cat /etc/issue 查看是CentOS、Debian还是Ubuntu，也可以通过VPS服务商提供的控制面板上查看。确定好之后，选择下面对应系统的安装命令（目前程序仅支持CentOS，其它系统请期待以后版本，如果其它系统使用所造成数据丢失，后果自负）：
完整版安装：CentOS系统下执行：wget -c http://lnmt.org/lnmt/beta/lnmt-full-beta-0.2.tar.gz && tar zxf lnmt-full-beta-0.2.tar.gz && cd lnmt-full-beta-0.2 && ./centos.sh
下载版安装：CentOS系统下执行：wget -c http://lnmt.org/lnmt/beta/lnmt-ol-beta-0.2.tar.gz && tar zxf lnmt-ol-beta-0.2.tar.gz && cd lnmt-ol-beta-0.2 && ./centos.sh
3、安装步骤/过程
(1)、录入MySQL的root账号密码
(2)、选择是否安装InnoDB，默认不安装，不安装可直接回车。
(3)、选择数据库版本，可选择版本有：MySQL 5.5.37 和 MariaDB 5.5.37，如不懂两者区别，自行Google。
(4)、选择JRE版本，默认为JDK 1.7，建议与下面Tomcat版本保持一致，以保证最优兼容性。
(5)、选择Tomcat版本，默认为Apache Tomcat 7.0.57，建议与上面JRE版本保持一致，以保证最优兼容性。
(6)、直接回车就可以自动安装了，安装过程可能需要20-30分钟，具体看VPS的硬件配置而定。
(7)、最后，如果你看到下面信息（主要是红框中的信息），如果有，则说明成功了，如果没有，则可能失败，请看上面的安装检测，可查看安装日志（在~下的lnmt-install.log文件）。