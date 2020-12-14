---
title: 删除centos 更新后多余的启动项
date: 2020-12-12 15:14:49
categories: Linux
tags:
 - Centos
---

在CentOS更新后,并不会自动删除旧内核。所以在启动选项中会有多个内核选项,可以手动使用以下命令删除多余的内核:

------------

```shell
# 查看系统当前内核版本:
uname -a

Linux localhost.localdomain 2.6.32-696.18.7.el6.x86_64 #1 SMP Thu Jan 4 17:31:22 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

# 查看系统中全部的内核RPM包:
rpm -qa | grep kernel

dracut-kernel-004-409.el6_8.2.noarch
abrt-addon-kerneloops-2.0.8-43.el6.centos.x86_64
kernel-2.6.32-696.18.7.el6.x86_64
kernel-headers-2.6.32-696.18.7.el6.x86_64
libreport-plugin-kerneloops-2.0.9-33.el6.centos.x86_64
kernel-firmware-2.6.32-696.18.7.el6.noarch

# 删除旧内核的RPM包
yum remove kernel--2.6.32-696.el6

# 重启系统
reboot

```