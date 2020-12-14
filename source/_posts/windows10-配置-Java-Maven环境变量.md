---
title: windows10 配置 Java+Maven环境变量
date: 2020-12-12 15:15:30
categories: Windows
tags:
 - Windows
 - Maven
---

**1、Java 环境变量**

`不使用%JAVA_HOME%，防止出错`
```shell
名称：JAVA_HOME
值：C:\Programs\Java\jdk1.8.0_171

Path ：
C:\Programs\Java\jdk1.8.0_151\bin;C:\Programs\Java\jdk1.8.0_151\jre\bin;

CLASSPATH ： 
.;C:\Programs\Java\jdk1.8.0_151\lib\dt.jar;C:\Programs\Java\jdk1.8.0_151\lib\tools.jar;
```

`测试`
	在cmd下输入 `java -version` `java` `javac`，都有输出则成功，特别是javac，一定要有输出！

------------


**2、Maven 环境变量**

`M2_HOME和MAVEN_HOME两个都需要，有的项目会用到`
```shell
M2_HOME ： C:\Programs\Java\apache-maven-3.5.2
MAVEN_HOME ： C:\Programs\Java\apache-maven-3.5.2
Path ：C:\Programs\Java\apache-maven-3.5.2\bin
```

`测试`
	在cmd下输入`mvn -v`，有输出即可