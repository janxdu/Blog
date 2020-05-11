---
title: MySQL常见问题排查
categories: DataBase
date: 2018-04-28 00:00:00
---

之前一直使用ORACLE的数据库，最近因项目需求需要操作MySQL，遇到了若干问题，在此记录一下。使用的虚拟机环境是CentOS release 6.2，数据库版本是5.6.16。

### 重置root用户密码

在使用命令行模式进入MySQL时提示密码错误，而root用户的密码也忘记了，需要重置数据库的root用户密码。虚拟机上以root用户执行以下命令：
```
// 停止mysql
$ service mysql stop
// 以跳过权限控制的模式启动mysql
$ service mysql start --skip-grant-tables
// 此时不需要密码即可访问mysql命令行
$ mysql -u root
// 更新root密码
$ update root set password=PASSWORD('xxxxxx');
// 退出mysql命令行
$ exit;
// 以正常模式重启mysql即可
$ service mysql restart
$ mysql -u root -pxxxxxx
```

### 新建用户、数据库与赋权

需要从sql文件导入数据到某个数据库，以MySQL命令行执行以下命令：
```
// 创建用户
$ use mysql
$ insert into mysql.user(Host,User,Password) values("localhost","testUser",password("testUser"));
// 新建数据库
$ create database test
// 切换到此数据库
$ use test
// 给testUser用户赋test数据库的权限
$ GRANT ALL PRIVILEGES ON test.* TO 'testUser'@'localhost' IDENTIFIED BY 
'testUser' WITH GRANT OPTION; 
$ 
```
### 执行sql文件导入时遇到ERROR 1005 (errno: 13)报错

经搜索是因为MySQL用户无权限修改mysql数据库文件所在文件夹，赋权即可。
```
$ Chown -r mysql:mysql /var/lib/mysql
```

---------
参考：
http://www.cnblogs.com/kerrycode/p/3861719.html

https://www.cnblogs.com/MIC2016/p/8287897.html#_label3_0
https://lists.mysql.com/mysql/219672

