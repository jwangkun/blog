---
title: 如何在CentOS上安装phpMyAdmin
date: 2016-04-19 21:17:14
tags: phpMyAdmin
---





本文地址：[https://linux.cn/article-4526-1.html](https://linux.cn/article-4526-1.html)

> **问题**:我正在CentOS上运行一个MySQL/MariaDB服务，并且我想要通过网络接口来用phpMyAdmin来管理数据库。在CentOS上安装phpMyAdmin的最佳方法是什么？

phpMyAdmin是一款以PHP为基础，基于Web的MySQL/MariaDB数据库管理工具。虽然已经存在着一些诸如[Adminer](http://xmodulo.com/set-web-based-database-management-system-adminer.html)的轻量级数据库管理工具, 但是phpMyAdmin还是更加广泛应用于网站管理员之中来进行各种MySQL/MariaDB的管理任务。它支持几乎所有MySQL数据库／表的相关操作，比如浏览、创建、复制、删除、重命名、更改，还有MySQL用户/权限管理和数据库导入/导出。以下就是**如何在CentOS 6或7上安装phpMyAdmin**。

![](https://dn-linuxcn.qbox.me/data/attachment/album/201412/25/105616takjivihinhipzmy.jpg)

### 前提

在CentOS上安装phpMyAdmin，你第一步需要架设一台Web服务器(如Apache或nginx)，安装好MySQL/MariaDB数据库和PHP。根据你的偏好和需求，你可以从[LAMP](http://linux.cn/article-1567-1.html)和[LEMP](http://linux.cn/article-4314-1.html)中选择一种安装。

另一个要求是允许在你的CentOS上安装EPEL库。如果你还没设置过请[猛戳这里](http://linux.cn/article-2324-1.html)。

### 在CentOS6或7上安装phpMyAdmin

一旦你设置了EPEL库，你就能轻松地用以下命令安装phpMyAdmin了。

在CentOS 7上:

```
$ sudo yum install phpmyadmin
```

在CentOS 7上:

```
$ sudo yum install phpmyadmin php-mcrypt
```

### 在CentOS 7上配置phpMyAdmin

默认情况下，CentOS 7上的phpMyAdmin只允许从回环地址(127.0.0.1)访问。为了能远程连接，你需要改动它的配置。

用文本编辑器打开phpMyAdmin的配置文件(路径：/etc/httpd/conf.d/phpMyAdmin.conf)，找出并注释掉带有"Require ip XXXX"字样的代码行。会有四处这样的代码行，用"Require all granted"取而代之。重新改动过的配置文件如下所示。

```
$ sudo vi /etc/httpd/conf.d/phpMyAdmin.conf
```

------

```
. . . . .<Directory /usr/share/phpMyAdmin/>   AddDefaultCharset UTF-8    <IfModule mod_authz_core.c>     # Apache 2.4     <RequireAny>       #Require ip 127.0.0.1       #Require ip ::1       Require all granted     </RequireAny>   </IfModule>   <IfModule !mod_authz_core.c>     # Apache 2.2     Order Deny,Allow     Deny from All     Allow from 127.0.0.1     Allow from ::1   </IfModule></Directory> <Directory /usr/share/phpMyAdmin/setup/>   <IfModule mod_authz_core.c>     # Apache 2.4     <RequireAny>       #Require ip 127.0.0.1       #Require ip ::1       Require all granted     </RequireAny>   </IfModule>   <IfModule !mod_authz_core.c>     # Apache 2.2     Order Deny,Allow     Deny from All     Allow from 127.0.0.1     Allow from ::1   </IfModule></Directory>. . . . .
```

最后，重启httpd使改动生效。

```
$ sudo systemctl restart httpd
```

### 在CentOS 6上配置phpMyAdmin

默认情况下，CentOS 6上的phpMyAdmin是禁止从每个IP地址访问的。为了能远程连接，你需要改动它的配置。

用文本编辑器打开phpMyAdmin的配置文件(路径：/etc/httpd/conf.d/phpMyAdmin.conf)，找出并注释掉"Deny from all"字样的代码行。然后把"Allow from 127.0.0.1"字样的代码行改成"Allow from 0.0.0.0"。重新改动过的配置文件如下所示。

```
$ sudo vi /etc/httpd/conf.d/phpmyadmin.conf
```

------

```
<Directory "/usr/share/phpmyadmin">  Order Deny,Allow#  Deny from all  Allow from 0.0.0.0</Directory>
```

下一步是将phpMyAdmin的配置文件用blowfish加密工具加密。这一步需要加密cookie里的密码来作为基于cookie的部分认证。

用文本编辑器打开如下路径所示的文件并且用blowfish设置一个随机密码，如下所示。

```
$ sudo vi /usr/share/phpmyadmin/config.inc.php
```

------

```
$cfg['blowfish_secret'] = 'kd5G}d33aXDc50!'; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */
```

最后，重启httpd使改动生效。

```
$ sudo service httpd restart
```

### 测试phpMyAdmin

测试phpMyAdmin是否设置成功，访问这个页面：http://<web-server-ip-addresss>/phpmyadmin

![](https://dn-linuxcn.qbox.me/data/attachment/album/201412/25/105620ud2pex6zfm2mmopf.jpg)

你应该能通过Web界面来记录下任何MySQL用户(比如root)和管理MySQL/MariaDB的数据库/表。

![](https://dn-linuxcn.qbox.me/data/attachment/album/201412/25/105622slmakqel8lqm0hkl.jpg)

### 疑难解答

这里有一些在CentOS上安装phpMyAdmin的过程中遇到的一些问题解决方法。

1. 当你在浏览器里尝试连接phpMyAdmin页面的时候，你看到"403 Forbidding"错误：

   You don't have permission to access /phpMyAdmin on this server.

   发生这种错误是因为phpMyAdmin默认阻止了IP地址远程连接。要修复这种错误，你需要编辑它的配置文件来允许远程连接。具体操作见上。

2. 当你连接phpMyAdmin页面时，你看见"The configuration file now needs a secret passphrase (blowfish_secret)."信息，并且你无法登录。

   要修复这种错误，你需要编辑 /usr/share/phpmyadmin/config.inc.php 这个文件来添加一个随机的blowfish密码，然后重启httpd，如下所示。

   ```
   $cfg['blowfish_secret'] = 'kd5G}d33aXDc50!'; /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */
   ```

   ------

   ```
   $ sudo service httpd restart (CentOS 6)$ sudo systemctl restart httpd (CentOS 7)
   ```

3. 当你连接phpMyAdmin页面时，你看见"Cannot load mcrypt extension. Please check your PHP configuration"错误信息。

   要修复这种错误，要安装下面这个包：

   ```
   $ sudo yum install php-mcrypt
   ```

   然后重启httpd：

   ```
   $ sudo service httpd restart (CentOS 6)$ sudo systemctl restart httpd (CentOS 7)
   ```

------
