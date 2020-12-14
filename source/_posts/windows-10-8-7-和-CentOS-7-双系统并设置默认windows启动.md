---
title: windows 10/8/7 和 CentOS 7 双系统并设置默认windows启动
date: 2020-12-12 15:26:59
categories: Windows
tags:
 - Windows
 - 双系统
---

**安装结果：**

	windows pro 64位
	centos 7 dvd 64位


​	
------------

**准备工作：**

	安装好的windows系统（最好先安装windows，因为后安装的centos会覆盖windows启动项，我们会在centos里恢复windows启动项）
	去centos官网下载最新的centos7 dvd
	U盘（最好8G以上）
	UltraISO 最新版（制作启动U盘）
	在windows上准备（压缩）30G左右空间


------------

**1、制作启动U盘**
	百度下载并安装UltraISO最新版，选择试用。Crtl+O（或者 文件-> 打开）打开下载好的centos7系统镜像。如下图：
![](/images/2020/12/12/52662000.png)
	
![](/images/2020/12/12/52671000.png)

	然后插入准备好的U盘，备份U盘里的数据（后面的操作会格式化U盘）。然后在菜单栏选择 启动 -> 写入硬盘镜像
![](/images/2020/12/12/52838000.png)

	硬盘驱动器就是U盘，映像文件默认加载，其余默认，点击`写入`就开始制作
![](/images/2020/12/12/52853000.png)

​	

------------

**2、安装centos系统**
	重启电脑，进入Bios设置使用U盘启动。此处不会的可百度。启动完成之后，选择第一项`Install centos7`
	
![](/images/2020/12/12/53040000.png)

	此处若进入选择语言界面，则说明一切正常，直接看第3步。否则进入grub界面，需要继续设置。原因是没有找到安装项。
	下方的提示信息将显示为
	vmlinuz initrd=initrd.img inst.stage2=hd:LABEL=CentOSx207x20x86_64 rd.live.check quiet
	移动光标，删除 
	LABEL=CentOSx207x20x86_64 rd.live.check 这部分，并用 linux dd 替换，最终的内容为
	vmlinuz initrd=initrd.img linux dd quiet
	稍后会出现一系列代码，依据你的优盘名称记下对应 DEVICE 列的值，一般是 sdb4 
	强制关闭计算机后再开机，按照上述步骤，按 Tab 键，修改启动参数，这次修改为 
	vmlinuz initrd=initrd.img inst.stage2=hd:/dev/sdb4 
	即可进入安装步骤


​	

------------

**3、配置centos安装（手动分区）**

	参考教程 [配置centos安装费（手动分区）](http://www.linuxidc.com/Linux/2016-06/132051p3.htm "配置centos安装费（手动分区）")


​	

------------

**4、修复windwos启动项**

	centos安装完成之后，会覆盖windows的启动项，这时候，只有一个centos启动项。我们在centos里面恢复windows的启动项，并设置6秒后默认启动windows。
```shell
在root账户下 
cp /etc/grub.d/40_custom /etc/grub.d/40_custom_bk #备份
vi /etc/grub.d/40_custom
#打开文件后，按i编辑，在文档内加入

menuentry 'Windows 10'{
	set root=(hd0,1)
	chainloader +1
}

#记住此处windows的名称Windows 10，用作后面修改默认启动项
#保存退出后
grub2-mkconfig -o /boot/grub2/grub.cfg
# 然后reboot就可以看到windows启动项了，此时默认启动项是centos
```

```shell
# 此处先不重启，接着输入。或者重启后进入root账户
cp /etc/default/grub /etc/default/grub_bk #备份
vim /etc/default/grub
#注释掉GRUB_DEFAULT=saved
#在这一行的下面插入GRUB_DEFAULT=’Windows 10’，保存并退出。
#此处的windows 10 是前面取的名字，两处只要一致即可
grub2-mkconfig --output=/boot/grub2/grub.cfg
#执行上面一步生效
#reboot可以看到电脑启动后光标默认在windows上，如果这时不做选择则自启动的是windows
```

**注意：**
	网上还有一种用EasyBCD制作启动项的，这个容易报错，进入centos会进入grub界面，我试了几次都没成功，按照网上的方法找不到启动盘，centos下的分区显示为Unknown disk.虽然这种方法在项目系统的界面比较好看，但是有一个系统会重启计算机再启动。相当于在选择的时候已经默认启动了一个系统（一般为windows）。
