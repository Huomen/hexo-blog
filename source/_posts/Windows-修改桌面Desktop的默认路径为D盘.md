---
title: Windows 修改桌面Desktop的默认路径为D盘
date: 2020-12-12 15:41:21
categories: Windows
tags:
 - Windows
 - 桌面路径
---

**1、**点击`开始菜单`→`运行`，输入“regedit”，打开注册表编辑器。

**2、** 依次展开注册表里的
`计算机\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders`
（不区分大小写）

**3、**找到`Desktop`，修改其值为你想要的路径，重启电脑即可。