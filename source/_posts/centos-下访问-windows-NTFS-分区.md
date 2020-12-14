---
title: centos 下访问 windows NTFS 分区
date: 2020-12-12 15:29:55
categories: Linux
tags:
 - windows
 - Centos
---

**1、下载安装**

[点击下载ntfs-3g_ntfsprogs-2017.3.23.tgz](https://www.hemingsheng.cn/file/download.hms?filename=ntfs-3g_ntfsprogs-2017.3.23.tgz "点击下载")

```shell
# 解压
tar xzvf ntfs-3g-***.tar.gz

cd ntfs-3g-***

# 编译安装
./configure
make
make install 

## 如果有如下错误
configure: error: in `/home/husen/Downloads/ntfs-3g_ntfsprogs-2017.3.23':
configure: error: no acceptable C compiler found in $PATH
See `config.log' for more details

yum -y install gcc
```


------------


**2、手动挂在NTFS分区**

```shell
# 查看当前所有磁盘分区类型
 fdisk -l
 # 手动挂载
 mount -t ntfs-3g /dev/sda1 /ntfs
# 手动卸载
umount /dev/sda1
```


------------


**3、自动挂载**

```shell
# 备份
cp /etc/fstab /etc/fstab_bk

# 编辑
vi /etc/fstab #编辑

在最后添加以下信息，以读写方式挂载磁盘

/dev/sda5    /ntfs/c-winos   defaults  0  0


:wq!保存，退出

# 输入命令生效生效
mount -a
# 或者重启
```