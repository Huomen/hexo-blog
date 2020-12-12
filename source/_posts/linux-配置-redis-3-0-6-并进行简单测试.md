---
title: linux  配置 redis 3.0.6 并进行简单测试
date: 2020-12-12 15:36:14
tags:
---

1、下载redis GZ压缩包，[点击下载](http://download.redis.io/releases/redis-3.0.6.tar.gz "点击下载")

2、tar解压

`tar -zxf redis-3.0.6.tar.gz  ` 



3、进入解压后的redis文件夹，编译

```shell
cd redis-3.0.6  
make  
```


4、然后测试，出现以下界面，则测试通过

```shell
make test  ##这一步比较久
```

（截图忘记保存了..............反正就是都OK）
5、接着开始安装，这个时候需要切换到root用户

```shell
make install  

```



6、接着再当前目录下执行以下命令，启动redis，出现以下界面说明启动成功

```shell
src/redis-server  
```




7、重新打开另外一个终端，再次测试是否安装成功。
```shell

cd redis-3.0.6/  
src/redis-cli  
```

**出现 redis127.0.0.1:6379>， 说明配置成功**

**接着输入**
```shell
set myname husen
get myname
```
**输出结果为husen**

