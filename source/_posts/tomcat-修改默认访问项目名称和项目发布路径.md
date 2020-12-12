---
title: tomcat 修改默认访问项目名称和项目发布路径
date: 2020-12-12 15:39:32
tags:
---

**1、修改项目发布路径**

tomcat默认的而发布路径为 	`tomcat/webapps/`目录，打不死这个目录下有一些默认的项目，在tomcat启动的时候会跟着一起加载。如果不想删除这些项目，可以把tomcat发布的路径修改到其他地方。

找到`tomcat/conf/server.xml`文件，修改里面这一行的`appBase`为其他路径即可。


```
<Host name="localhost"  appBase="/root/webfile/webapps" unpackWARs="true" autoDeploy="true">
```
其中：

 - name是虚拟主机名，对应目录 /conf /Catalina /localhost
 -  unpackWARs 为是否自动解压war文件，如果设置为true，表示把war文件先展开再运行。如果为false则直接运行war文件
 - autoDeploy，默认为true，表示如果有新的WEB应用放入appBase并且Tomcat在运行的情况下，自动载入应用

*特地别：*
这里既可以用相对路径，也可以用绝对路径。
相对路径默认`tomcat`目录为根目录


----------

**2、修改默认访问项目**

最简单的，可以直接把项目名称修改为`ROOT`，放在	`tomcat/webapps/`目录即可。

如果不想修改。那么在第1步中的
```
<Host name="localhost"  appBase="/root/webfile/webapps" unpackWARs="true" autoDeploy="true">
```

下面加上下面这句即可，其中
```
<!-- 设置默认项目名称 -->
<Context path="" docBase="/root/webfile/web" reloadable="true"/> 
```

- `path`代表用浏览器访问的时候的的路径，如http://localhost:8080/web来访问path="/web"
- `docBase`为你的项目的路径，这里同样既可以用相对路径，也可以用绝对路径。设置好了之后就会把项目自动映射到ROOT
- reloadable，如果这个属性设为true，tomcat服务器在运行状态下会监视在WEB-INF/classes和WEB-INF/lib目录下class文件的改动，如果监测到有class文件被更新的，服务器会自动重新加载Web应用


----------