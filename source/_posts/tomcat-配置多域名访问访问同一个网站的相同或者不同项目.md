---
title: tomcat 配置多域名访问访问同一个网站的相同或者不同项目
date: 2020-12-12 15:40:09
tags:
---

关于证书的申请这里就不多说了，阿里云和腾讯云都可以申请免费的SSL证书，有效期为一年，到期可以再申请。网上搜一下，就可以去申请了。


----------


然后关于tomcat配置SSL证书的，网上也很多教程，这里推荐腾讯云的官方证书安装指引[点击跳转至腾讯云证书安装指引](https://cloud.tencent.com/document/product/400/4143#4.-tomcat-.E8.AF.81.E4.B9.A6.E9.83.A8.E7.BD.B2)


----------


不过现在的需求是多个域名访问同一个网站，并且多个域名绑定同一IP的。比如我，在腾讯云有一台服务器，解析了两个域名，现在我想让这两个域名能同时以https访问我的网站，可以是访问同一个项目，也可以是访问不同的项目。在参照前面的安装指引完成之后，只能用一个域名访问，而另一个显示证书不安全。

接下来言归正传。


----------


**1、**首先将申请好的证书下载解压。如下图：

![](https://www.hemingsheng.cn/imageDownload.hms?imageUrl=20180115/39403000.jpg)

在tomcat文件夹下有两个文件，一个是密码，一个是证书，后面我们都需要。

**注意：** 需要分别给两个域名申请证书！

----------

**2、** 编辑`tomcat/conf` 文件夹下的 `server.xml`文件，一共修改两处，其他地方都不变。首先修改第一个地方。这里声明了两个主机(host)


```xml
<!-- 第1处 -->
<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol" maxThreads="150" SSLEnabled="true" defaultSSLHostConfigName="www.hemingsheng.cn" >
		<SSLHostConfig hostName="www.hemingsheng.cn">
			<Certificate certificateKeystoreFile="/home/key_https/Tomcat/www.hemingsheng.cn.jks"
				certificateKeystorePassword="这里填txt文件中的密码" type="RSA" 
			/>
        </SSLHostConfig>
		
		<SSLHostConfig hostName="www.tinger.wang">
			<Certificate certificateKeystoreFile="/home/key_https/Tomcat/www.tinger.wang.jks"
				certificateKeystorePassword="这里填另一个txt文件中的密码" type="RSA" />
        </SSLHostConfig>
	</Connector>

```
----------

**3、** 如果两个域名访问同一个项目，按照如下修改

```xml
 <Host name="www.hemingsheng.cn" appBase="/root/webfile/webapps" unpackWARs="false" autoDeploy="true">
				<Alias>www.hemingsheng.cn</Alias>  
				<Alias>www.tinger.wang</Alias>
			<!-- 设置默认项目名称 -->
			<Context path="" docBase="/root/webfile/web" reloadable="true" /> 
				<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
					prefix="localhost_access_log" suffix=".txt"
					pattern="%h %l %u %t &quot;%r&quot; %s %b" />
		</Host>
```

这里的关键在于`<Alias>www.hemingsheng.cn</Alias>`，将两个域名主机指向了同一个项目


----------

**4、** 如果要配置两个域名访问不同的项目，则按照如下配置

<!-- 第2处 -->
```xml
<!-- 
   这里我两个主机配置了相同的项目，这样修改会实例化两个web项目，虽然两个域名可以访问同一个项目，但是会启动两个虚拟机，不推荐。
   这个访问推荐用来配置两个域名访问两个不同的项目
-->

<Host name="www.hemingsheng.cn"  appBase="/root/webfile/webapps" unpackWARs="false" autoDeploy="true">
		<!-- 设置默认项目名称 -->
		<Context path="" docBase="/root/webfile/web" reloadable="true" /> 
			<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />

      </Host>
	  
	  <Host name="www.tinger.wang"  appBase="/root/webfile/webapps" unpackWARs="false" autoDeploy="true">
		<!-- 设置默认项目名称 -->
		<Context path="" docBase="/root/webfile/web" reloadable="true" /> 
			<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />
```


----------

然后重启，发现两个域名都可以用https访问了。


----------