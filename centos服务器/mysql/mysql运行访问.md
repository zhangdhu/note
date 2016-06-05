进入
mysql -u root -p mysql

权限
grant all privileges on *.* to 'root'@'%' identified by 'mysql' with grant option;

flush privileges; # 重载系统权限
exit;

允许3306端口
iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT
# 查看规则是否生效
iptables -L -n

PS，上面iptables添加/删除规则都是临时的，如果需要重启后也生效，需要保存修改:
service iptables save # 或者: /etc/init.d/iptables save
另外，
vi /etc/sysconfig/iptables-config  # 加上下面这行规则也是可以的
-A INPUT -p tcp -m state --state NEW -m tcp --dport 3306 -j ACCEPT


