---
title: windows 配置java环境变量
date: 2020-12-11 17:35:22
tags: Java
---

**变量设置参数如下：**

变量名：`JAVA_HOME` 
变量值：`C:\Programs\Java\jdk1.8.0_171`

变量名：`CLASSPATH` 
变量值：`.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`

变量名：`Path` 
变量值：`%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`