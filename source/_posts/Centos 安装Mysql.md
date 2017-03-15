title: Centos挂载数据盘
date: 2014-06-11
tags:  Centos，Mysql

------

Centos 6.6下安装Mysql很简单，先查看一下yum源里面的mysql以及版本
yum list mysql-server

当只有一个时候就可以直接（如果有多个的时候，安装带上版本号）
yum install mysql-server
进行安装

安装完成后，启动mysql：
先启动Mysql服务
service mysqld start

设置Mysql开机启动
chkconfig mysqld on

检查一下开启启动情况：
chkconfig --list

MYSQL默认的数据文件存储目录为/var/lib/mysql。假如要把目录移到/home/data下需要进行下面几步：

1、home目录下建立data目录

cd /homemkdir data
2、把MySQL服务进程停掉：

mysqladmin -u root -p shutdown
3、把/var/lib/mysql整个目录移到/home/data

mv /var/lib/mysql　/home/data/
这样就把MySQL的数据文件移动到了/home/data/mysql下

4、找到my.cnf配置文件

如果/etc/目录下没有my.cnf配置文件，请到/usr/share/mysql/下找到*.cnf文件，拷贝其中一个到/etc/并改名为my.cnf)中。命令如下：

[root@test1 mysql]# cp /usr/share/mysql/my-medium.cnf　/etc/my.cnf
5、编辑MySQL的配置文件/etc/my.cnf

为保证MySQL能够正常工作，需要指明mysql.sock文件的产生位置。修改socket=/var/lib/mysql/mysql.sock一行中等号右边的值为：/home/mysql/mysql.sock 。操作如下：

vi　 my.cnf　 (用vi工具编辑my.cnf文件，找到下列数据修改之)# The MySQL server[mysqld]　 port　= 3306#socket　 = /var/lib/mysql/mysql.sock（原内容，为了更稳妥用“#”注释此行）socket　 = /home/data/mysql/mysql.sock　（加上此行）
6、修改MySQL启动脚本/etc/init.d/mysql

最后，需要修改MySQL启动脚本/etc/init.d/mysql，把其中datadir=/var/lib/mysql一行中，等号右边的路径改成你现在的实际存放路径：home/data/mysql。

[root@test1 etc]# vi　/etc/init.d/mysql#datadir=/var/lib/mysql（注释此行）datadir=/home/data/mysql （加上此行）

如果是CentOS还要改 /usr/bin/mysqld_safe 相关文件位置；

最后 做一个mysql.sock 链接：
ln -s /home/data/mysql/mysql.sock /var/lib/mysql/mysql.sock

7、重新启动MySQL服务
/etc/init.d/mysqld　start


如果工作正常移动就成功了，否则对照前面的7步再检查一下。还要注意目录的属主和权限。
复制内容到剪贴板



注意事项;
1.乱码问题
找一个配置文件，复制到/etc/目录，命名为my.cnf
（有时候没有my.cnf）
cp /usr/share/doc/mysql-server-5.1.73/my-medium.cnf /etc/my.cnf

vim my.cnf
在[client]和[mysqld]下面都添加上
default-character-set=utf8
最后重新启动服务就可以了
service mysqld restart

2.设置Mysql远程访问
grant all privileges on *.* to 'root'@'%' identified by '123456' with grant option;

3.修改mysql数据存储路径
