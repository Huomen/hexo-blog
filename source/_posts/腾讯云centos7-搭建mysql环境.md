---
title: 腾讯云centos7 搭建mysql环境
date: 2020-12-12 15:40:55
tags:
---

**1、安装mysql**

```ruby
##添加可以用于安装数据库系统的MySQL存储库 
yum localinstall -y https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm

##安装 
yum install -y mysql-community-server

##启动 
systemctl start mysqld
```


----------

**2、修改root密码**

```ruby
##查看初始密码 
grep 'temporary password' /var/log/mysqld.log

2017-10-12T02:37:57.483675Z 1 [Note] A temporary password is generated for root@localhost: **6uRg%NmxG9

mysql -u root -p 回车输入以上查询的密码登录

##关闭密码强度校验
set global validate_password_policy=0;
set global validate_password_length=1;

##修改初始密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
##刷新权限
FLUSH PRIVILEGES;
```


----------

**3、配置远程访问**

```ruby
##备份
cp /etc/my.cnf /etc/my.cnf_bk
##编辑
vi /etc/my.cnf
##在最后面加上一行
bind-address = 0.0.0.0
##重启
systemctl restart mysqld
```


----------

**4、创建远程访问用户**

```ruby
##创建用户
CREATE USER 'husen'@'%' IDENTIFIED BY '123456';
##如果创建用户提示密码强度不够，则用第2步中的方法关闭密码强度校验

##赋予远程访问权限
GRANT ALL PRIVILEGES ON *.* TO 'husen'@'%';

##刷新权限
FLUSH PRIVILEGES;
```