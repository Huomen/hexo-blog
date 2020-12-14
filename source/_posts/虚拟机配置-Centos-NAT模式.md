---
title: 虚拟机配置 Centos NAT模式
date: 2020-12-12 15:17:45
categories: 虚拟机
tags:
 - Centos
 - 虚拟机
---

**1、配置vmware**

	在VMware里，依次点击”编辑“ - ”虚拟网络编辑器“

![](/images/2020/12/12/58479000.png)

	选择更改设置，然后就可以修改

![](/images/2020/12/12/58587000.png)

	修改一下几个地方
	1）选择NAT模式
	2）选择NAT模式
	3）设置子网IP和子网掩码（子网IP与宿主机的ip一定不能处在同一地址范围里，否则就算虚拟机能上网，网络既慢，还不稳定。）
	4）NAT设置（设置网关，一般默认即可）

![](/images/2020/12/12/58636000.png)

![](/images/2020/12/12/58702000.png)


------------

**2、设置虚拟机系统的模式为NAT模式**

以下两个二选一即可

![](/images/2020/12/12/62575000.jpg)

![](/images/2020/12/12/62586000.jpg)

------------


**3、配置网卡配置文件**

	修改 `/etc/sysconfig/network-scripts/ifcfg-ens××`文件，这里的××具体不一样。
	（类似ifcfg-*之类的文件）
修改和添加如下信息：
	
```shell
	BOOTPROTO=static #原始值“dhcp”，改为“static”
	IPADDR=192.168.186.11 #添加NAT上网的静态IP地址
	NETMASK=255.255.255.0 #添加子网掩码
	GATEWAY=192.168.186.2 #添加网关，根据VMware 软件‘虚拟网络编辑器’中的子网配置
	DNS1=192.168.186.2 #添加首选DNS服务器，和网关一致
	DNS2=8.8.8.8 #添加备用DNS服务器（可不填）
	ONBOOT=yes #原始值“no”，改为“yes”，意为网卡eth0随开机启动
```

修改后完整配置文件如下：

```shell
TYPE=Ethernet
BOOTPROTO=static
DEFROUTE=yes
PEERDNS=yes
PEERROUTES=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_PEERDNS=yes
IPV6_PEERROUTES=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=ens33
UUID=09423380-5f41-4ebf-8734-7297b547af10
DEVICE=ens33
ONBOOT=yes
ZONE=
GATEWAY=192.168.186.2
IPADDR=192.168.186.11
NETMASK=255.255.255.0
DNS1=192.168.186.2

```


------------


**4、重启（服务）生效**

`/etc/init.d/network restart` 或者`service network restart`或者`reboot` 即可生效


------------

**5、测试结果**

主机 ping 虚拟机 -> 在电脑cmd命令行下 ping 192.168.186.11
虚拟机 ping 主机 -> 在centos中 ping 192.168.186.1
虚拟机 ping 百度 -> 在centos中 ping www.baidu.com


------------

**6、解决虚拟机ping不通主机，但是主机可以ping通虚拟机**

打开`防火墙`->`选择高级设置`->`入站规则`->`找到配置文件类型为“公用”的“文件和打印共享（回显请求 – ICMPv4-In）”规则`，设计启用并允许。
