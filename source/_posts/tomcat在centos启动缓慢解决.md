---
title: tomcat在centos启动缓慢解决
date: 2020-12-12 15:04:46
tags:
---

 在`$TOMCAT_HOME/bin/catalina.sh`最前面加一句
	
	if [[ "$JAVA_OPTS" != *-Djava.security.egd=* ]]; then
		JAVA_OPTS="$JAVA_OPTS -Djava.security.egd=file:/dev/urandom"
	fi