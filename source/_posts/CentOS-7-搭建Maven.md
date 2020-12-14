---
title: CentOS 7 搭建Maven
date: 2020-12-12 15:25:05
categories: Centos
tags:
 - Maven
 - Centos
---

**1、选择要放maven的位置，下载安装包**

`wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz`
	
	

------------


**2、解压在当前目录，记住当前目录路径**

`tar -zxvf apache-maven-3.5.2-bin.tar.gz`


------------


**3、配置环境变量**

`vi /etc/profile`

在文件末尾添加
```shell
M2_HOME=第2步中的路径
export PATH=${M2_HOME}/bin:${PATH}
```
重载生效

` source /etc/profile`


------------

**4、检查是否生效**

`mvn -v `