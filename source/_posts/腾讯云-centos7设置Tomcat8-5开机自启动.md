---
title: 腾讯云 centos7设置Tomcat8.5开机自启动
date: 2020-12-12 15:34:59
tags:
---

1.  `cd /etc/init.d`

1.  `vi tomcat8`

1. 粘贴自启动命令 注意替换自己的Java环境变量和 TOMCAT的HOME

```shell
#!/bin/bash        
#        
# tomcat startup script for the Tomcat server        
#        
# chkconfig: 345 80 20        
# description: start the tomcat deamon        
#        
# Source function library        
. /etc/rc.d/init.d/functions        
        
prog=tomcat8       
JAVA_HOME=/opt/jdk1.8.0_40      
export JAVA_HOME        
CATALANA_HOME=/opt/apache-tomcat-8.0.20/      
export CATALINA_HOME        
        
case "$1" in        
start)        
    echo "Starting Tomcat..."        
    $CATALANA_HOME/bin/startup.sh        
    ;;        
        
stop)        
    echo "Stopping Tomcat..."        
    $CATALANA_HOME/bin/shutdown.sh        
    ;;        
        
restart)        
    echo "Stopping Tomcat..."        
    $CATALANA_HOME/bin/shutdown.sh        
    sleep 2        
    echo        
    echo "Starting Tomcat..."        
    $CATALANA_HOME/bin/startup.sh        
    ;;        
        
*)        
    echo "Usage: $prog {start|stop|restart}"        
    ;;        
esac        
exit 0    
```

------------

4.保存退出
5.`chmod 755 tomcat8` 赋权限
6.`service tomcat8 start` 启动检查
7.`chkconfig tomcat8 on`