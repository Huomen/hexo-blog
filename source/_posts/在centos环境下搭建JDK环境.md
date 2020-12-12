---
title: 在centos环境下搭建JDK环境
date: 2020-12-12 15:06:46
tags:
---

**1、上传、解压**

`tar -zxvf jdk-8u151-linux-x64.tar.gz`


------------



**2、设置环境变量**
```shell

vi /etc/profile

# 方案1 java environment
JAVA_HOME=/home/jdk/jdk1.8.0_151
JRE_HOME=/home/jdk/jdk1.8.0_151/jre
CLASS_PATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME JRE_HOME CLASS_PATH PATH

# 方案2 jdk
export JAVA_HOME=/home/husen/jdk/jdk1.8.0_181
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

------------

**3、生效**
	
`source /etc/profile`