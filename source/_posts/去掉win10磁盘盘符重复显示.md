---
title: 去掉 win10 磁盘盘符重复显示
date: 2020-07-09 10:12:39
categories: Windows
tags: 磁盘盘符
---

**1、** 快捷键`win+R`进入运行窗口，然后输入`regedit`，在地址栏输入`计算机\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Desktop\NameSpace\DelegateFolders`，即可定位到显示磁盘盘符的位置

![](/images/2020/07/09/54861000.jpg)

------------

**2、** 然后把`{F5FB2C77-0E2F-4A16-A381-3E560C68BC83}`项重命名，在前面加了减号“-”就是改成`-{F5FB2C77-0E2F-4A16-A381-3E560C68BC83}`即可，如图所示：

![](/images/2020/07/09/54986000.jpg)

再次查看资源管理器，发现重复的盘符已经消失了

![](/images/2020/07/09/55016000.jpg)