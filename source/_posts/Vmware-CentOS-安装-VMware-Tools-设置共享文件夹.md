---
title: Vmware CentOS 安装 VMware Tools 设置共享文件夹
date: 2020-12-12 15:10:29
categories: 虚拟机
tags:
 - CentOS
 - 虚拟机
---

**1、更新系统**

`yum -y update`
	

------------

**2、安装相应的依赖**
```shell
yum install -y perl
yum install -y net-tools
yum install -y gcc
yum install -y kernel-headers
```


------------

**3、安装 VMware Tools **

	在相应的系统上右键->安装 VMware Tools 

切换到`root`用户，运行以下命令

```shell
# 创建目录
mkdir /mnt/cdrom
# 挂载光驱
mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom
cp VMwareTools-9.10.5-2981885.tar.gz /tmp
cd /tmp
tar -zxvf VMwareTools-9.10.5-2981885.tar.gz
cd vmware-tools-distrib
./vmware-install.pl

#若再以下类似报错，可试试
#The path "" is not a valid path to the `3.10.0-229.el7.x86_64` kernel headers.
yum install kernel-devel
```

接着一路回车（默认yes）即可，完成后`reboot`


------------

**4、设置共享文件夹**

在相应的系统上`右键->设置`

![](/images/2020/12/12/74777000.png)

选择`选项`，设置启用`文件夹共享`，然后点击`添加`，选择需要共享的文件夹，然后就可以在共享文件夹里放置需要共享的文件。

![](/images/2020/12/12/74808000.png)

重启虚拟机，在`/mnt/hgfs`目录下可以看到共享的文件夹

**Enjoy it!**