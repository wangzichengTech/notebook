



1、基本概念

### 1.1、前言

web开发：

- web，网页的意思  ， www.baidu.com
- 静态web
  - html，css
  - 提供给所有人看的数据始终不会发生变化！
- 动态web
  - 淘宝，几乎是所有的网站；
  - 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同！
  - 技术栈：Servlet/JSP，ASP，PHP

在Java中，动态web资源开发的技术统称为JavaWeb；

### 1.2、web应用程序

web应用程序：可以提供浏览器访问的程序；

- a.html、b.html......多个web资源，这些web资源可以被外界访问，对外界提供服务；
- 你们能访问到的任何一个页面或者资源，都存在于这个世界的某一个角落的计算机上。
- URL 
- 这个统一的web资源会被放在同一个文件夹下，web应用程序-->Tomcat：服务器
- 一个web应用由多部分组成 （静态web，动态web）
  - html，css，js
  - jsp，servlet
  - Java程序
  - jar包
  - 配置文件 （Properties）

web应用程序编写完毕后，若想提供给外界访问：需要一个服务器来统一管理；

#### Web应用程序概述

- Web应用程序是一种可以通过Web访问的应用程序，程序的最大好处是用户很容易访问应用程序，用户只需要有浏览器即可，不需要再安装其他软件。

- 一个Web应用程序是由完成特定任务的各种Web组件（web components)构成的并通过Web将服务展示给外界。在实际应用中，Web应用程序是由多个Servlet、JSP页面、HTML文件以及图像文件等组成。所有这些组件相互协调为用户提供一组完整的服务。

#### 应用程序模式

- 应用程序有两种模式C/S、B/S。C/S是客户端/服务器端程序，也就是说这类程序一般独立运行。而B/S就是浏览器端/服务器端应用程序，这类应用程序一般借助IE、Firefox、Google等浏览器来运行。WEB应用程序一般是B/S模式。

​     <img src="JavaWeb.assets/clip_image001.jpg" alt="12" style="zoom:80%;" />

​     <img src="JavaWeb.assets/clip_image001-1583293770740.jpg" alt="11" style="zoom:67%;" />

##### 1，C/S架构

- C/S是Client/Server的缩写。
- Server即服务器，通常采用高性能的PC或工作站，
- Client即客户端，需要在客户电脑上安装专用的客户端软件。
- 例如大家比较熟悉的腾讯QQ就是个典型的C/S结构的软件，用户要安装QQ客户端程序同服务器进行通讯。

##### 2，B/S架构

- B/S架构即==浏览器和服务器==架构模式。它是随着Internet技术的兴起，对C/S架构的一种变化或者改进的架构。

- 在这种架构下，用户工作界面是通过==浏览器==来实现，极少部分事务逻辑在前端(Browser)实现，但是主要事务逻辑在服务器端(Server)实现，形成所谓三层结构。

- 例如京东、淘宝、12306等都是B/S架构。

- WEB应用程序一般是B/S模式。

- B/S优点：

  - 耦合度小，利于分工协作，提高开发效率

  - 具有良好的可扩展性和可维护性

  - 升级成本小
  - 简化了客户端电脑载荷
  - 减轻了系统维护与升级的成本和工作量
  - 降低了用户的总体成本

### 1.3、静态web

- `*.htm, *.html`,这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取。通络；

![1567822802516](JavaWeb.assets/1567822802516.png)

- 静态web存在的缺点
  - Web页面无法动态更新，所有用户看到都是同一个页面
    - 轮播图，点击特效：伪动态
    - JavaScript [实际开发中，它用的最多]
    - VBScript
  - 它无法和数据库交互（数据无法持久化，用户无法交互）



### 1.4、动态web

页面会动态展示： “Web的页面展示的效果因人而异”；

![1567823191289](JavaWeb.assets/1567823191289.png)

缺点：

- 加入服务器的动态web资源出现了错误，我们需要重新编写我们的**后台程序**,重新发布；
  - 停机维护

优点：

- Web页面可以动态更新，所有用户看到都不是同一个页面
- 它可以与数据库交互 （数据持久化：注册，商品信息，用户信息........）

![1567823350584](JavaWeb.assets/1567823350584.png)

#### 静态网页与动态网页

- 静态网页没有数据库的支持，在网站制作和维护方面工作量较大，静态网页的交互性较差，在功能方面有较大的限制。

- 动态网页是指在服务器端运行的程序或者网页，会根据不同客户、不同时间返回不同的网页。



### 1.5、访问Web资源

#### 什么是URL

- URL是UniformResource Locator的缩写，意思是统一资源定位符，也被称为网页地址，是因特网上标准的资源地址(Address)。
- 统一资源定位符(URL)适用于完整地描述Internet上网页和其他资源地址的一种标识方法。
- 简单地说，URL就是Web地址，俗称“网址”。

##### URL的组成

- URL是唯一能够识别Internet上具体的计算机、目录或文件位置的命名约定。

- 以这样一个URL:http://localhost:8080/FirstWeb/index.jsp为例来分析URL的组成。

1. ==HTTP协议==：两台计算机可能因为系统不同、运行程序所用语言不通，要进行通信必须按照一个约定的规则进行，浏览器和服务器之间必须遵循共同的协议HTTP (HyperText Transfer Protocol ==超文本传输协议==)。HTTP是互联网上应用最为广泛的一种网络协议。

2. ==服务器主机名或IP== :在这里localhost就是服务器的地址， 意思是本机上的服务器。当然也可以使用127.0.0.1或实际IP地址来代替。IP是网络之间互连的协议,是Internet Protocol的缩写,中文缩写为“==网协==”。

3. ==端口号==： 端口号是网络程序和外部进行通信的通道，当从外部访问服务器时要通过指定端口号来访问。物理端口是指物理存在的端口；逻辑端口是指逻辑意义上用于区分服务的端口，如TCP/IP协议中的服务端口，端口号的范围从0到65535。

4. ==路径==： 路径（包括请求的资源）由零个或多个 "/" 符号隔开的字符串， 一般用来表示主机上的一个目录或文件地址等。 而请求的资源指请求的文件的名称，可以是 一个HTML页面，也可以是 一个Servlet、 图片等服务器提供的资源。以FirstWeb/index.jsp为例，news代表的是Web应用对外发布的根路径名，而index.jsp代表了一个存放到FirstWeb根目录下的一个文件。

- ==URL的组成:==
  - 协议
  - 主机（包括端口号）
  - 路径

## 2、web服务器

- Web服务器一般指网站服务器，是指驻留于因特网上某种类型计算机的程序，可以向浏览器等Web客户端提供文档，也可以放置网站文件，让全世界浏览；可以放置数据文件，让全世界下载。
- 下面介绍几种常用的WEB服务器。
  - ==WebLogic==
    - BEA WebLogic Server 在使应用服务器成为企业应用架构的基础方面继续处于领先地位。
    - BEA WebLogic Server 为构建集成化的企业级应用提供了稳固的基础，
    - 它们以 Internet 的==容量==和==速度==，在连网的企业之间共享信息、提交服务，实现协作自动化。
  - ==Apache==
    - Apache仍然是世界上用的最多的Web服务器，市场占有率达60%左右。
    - 世界上很多著名的网站都是Apache的产物，
    - 它的成功之处主要在于它的==源代码开放==、有一支开放的开发队伍、支持跨平台的应用（可以运行在几乎所有的Unix、Windows、Linux系统平台上）以及它的==可移植性==等方面。
  - ==Tomcat==
    - Tomcat是一个==开放源代码==、运行Servlet和JSP Web应用软件的基于Java的Web应用软件容器。
    - 它是==Apache==软件基金会一个开源的==核心项目==，由Apache、Sun和其他一些公司及个人共同开发完成。
    - Tomcat Server是根据Servlet和JSP规范进行执行的，因此我们就可以说Tomcat Server也实行了Apache-Jakarta规范且比绝大多数商业应用软件服务器要好。
  -  ==Jboss==
    - 是一个基于==J2EE==的==开放源代码==的应用服务器。
    -  JBoss代码遵循LGPL许可，可以在任何商业应用中==免费==使用，而不用支付费用。
    - JBoss是一个管理EJB的容器和服务器，支持EJB 1.1、EJB 2.0和EJB3的规范。
    - 但JBoss核心服务==不包括支持Servlet/JSP的WEB容器==，一般与Tomcat或Jetty绑定使用。

### 2.1、技术讲解

**ASP:**

- 微软：国内最早流行的就是ASP；

- 在HTML中嵌入了VB的脚本，  ASP + COM；

- 在ASP开发中，基本一个页面都有几千行的业务代码，页面极其换乱

- 维护成本高！

- C# 

- IIS

  ```html
  <h1>
      <h1><h1>
          <h1>
              <h1>
                  <h1>
          <h1>
              <%
              System.out.println("hello")
              %>
              <h1>
                  <h1>
     <h1><h1>
  <h1>
  ```

  

**php：**

- PHP开发速度很快，功能很强大，跨平台，代码很简单 （70% , WP）
- 无法承载大访问量的情况（局限性）



**JSP/Servlet : ** 

B/S：浏览和服务器

C/S:  客户端和服务器

- sun公司主推的B/S架构
- 基于Java语言的 (所有的大公司，或者一些开源的组件，都是用Java写的)
- 可以承载三高问题带来的影响；
- 语法像ASP ， ASP-->JSP , 加强市场强度；

### 2.2、web服务器

服务器是一种被动的操作，用来处理用户的一些请求和给用户一些响应信息；

**==IIS==**

微软的； ASP...,Windows中自带的

==**Tomcat**==

![1567824446428](JavaWeb.assets/1567824446428.png)

面向百度编程；

Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现，因为Tomcat 技术先进、性能稳定，而且**免费**，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用[服务器](https://baike.baidu.com/item/服务器)，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个Java初学web的人来说，它是最佳的选择

Tomcat 实际上运行JSP 页面和Servlet。Tomcat最新版本为**9.0。**

**工作3-5年之后，可以尝试手写Tomcat服务器；**

下载tomcat：

1. 安装 or  解压
2. 了解配置文件及目录结构
3. 这个东西的作用



## 3、Tomcat

### 3.1、 安装tomcat

tomcat官网：http://tomcat.apache.org/



### 3.2、Tomcat启动和配置

#### Tomcat目录作用描述

| **目录**        | **说明**                                                  |
| --------------- | --------------------------------------------------------- |
| ==**bin**==     | 存放各平台下用于启动和停止Tomcat的脚本文件                |
| ==**conf**==    | 存放Tomcat各种配置文件，其中最重要的是server.xml和web.xml |
| ==**lib**==     | 存放tomcat服务器所需的jar文件                             |
| ==**webapps**== | Web应用的发布目录                                         |
| ==**work**==    | Jsp运行时生成的Servlet文件                                |
| ==**logs**==    | 存放tomcat的日志文件                                      |
| ==**temp**==    | Tomcat运行时存放临时文件                                  |

文件夹作用：

![image-20220126235845835](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220126235845835.png)

**启动。关闭Tomcat**

![image-20220126235909771](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220126235909771.png)

访问测试：http://localhost:8080/

可能遇到的问题：

1. Java环境变量没有配置
2. 闪退问题：需要配置兼容性
3. 乱码问题：配置文件中设置

### 3.3、配置

![image-20220126235947496](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220126235947496.png)

可以配置启动的端口号

- tomcat的默认端口号为：8080
- mysql：3306
- http：80
- https：443

```xml
<Connector port="8081" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
```
可以配置主机的名称

- 默认的主机名为：localhost->127.0.0.1
- 默认网站应用存放的位置为：webapps

```xml
  <Host name="www.qinjiang.com"  appBase="webapps"
        unpackWARs="true" autoDeploy="true">
```
#### 高难度面试题

请你谈谈网站是如何进行访问的！

1. 输入一个域名；回车

2. 检查本机的 C:\Windows\System32\drivers\etc\hosts配置文件下有没有这个域名映射；

   1. 有：直接返回对应的ip地址，这个地址中，有我们需要访问的web程序，可以直接访问

      ```java
      127.0.0.1       www.qinjiang.com
      ```

   2. 没有：去DNS服务器找，找到的话就返回，找不到就返回找不到；

   ![image-20220127000210718](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220127000210718.png)

4. 可以配置一下环境变量（可选性）

### 3.4、发布一个web网站

不会就先模仿

- 将自己写的网站，放到服务器(Tomcat)中指定的web应用的文件夹（webapps）下，就可以访问了

网站应该有的结构

```java
--webapps ：Tomcat服务器的web目录
	-ROOT
	-kuangstudy ：网站的目录名
		- WEB-INF
			-classes : java程序
			-lib：web应用所依赖的jar包
			-web.xml ：网站配置文件
		- index.html 默认的首页
		- static 
            -css
            	-style.css
            -js
            -img
         -.....
```



HTTP协议 ： 面试

Maven：构建工具

- Maven安装包

Servlet 入门

- HelloWorld！
- Servlet配置
- 原理

### 3.5、关于tomcat

tomcat和servlet在网络中的位置：

![image-20220127001422512](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220127001422512.png)

浏览器访问web的流程图：

![image-20220127001927098](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220127001927098.png)



## 4、Http

### 4.1、什么是HTTP

HTTP（超文本传输协议）是一个简单的请求-响应协议，它通常运行在TCP之上。

- 文本：html，字符串，~ ….
- 超文本：图片，音乐，视频，定位，地图…….
- 80

Https：安全的

- 443

### 4.2、两个时代

- http1.0

  - HTTP/1.0：客户端可以与web服务器连接后，**只能获得一个web资源**，短连接，获取资源后就断开连接
  - HTTP1.0定义了三种请求方法： GET, POST 和 HEAD方法。

- http2.0

  - HTTP/1.1：客户端可以与web服务器连接后，**可以获得多个web资源**，保持连接。
  
  - HTTP1.1新增了五种请求方法：OPTIONS, PUT, DELETE, TRACE 和 CONNECT 方法。
  
  

### 4.3、Http请求

#####  HTTP请求方式

- HTTP请求是指从客户端到服务器端的请求消息。
- 包括：消息首行中，对资源的请求方法、资源的标识符及使用的协议。
- 根据HTTP标准，HTTP请求可以使用多种请求方法。 

- ==客户端---发请求（Request）---服务器==

百度：

```java
Request URL:https://www.baidu.com/   请求地址
Request Method:GET    get方法/post方法
Status Code:200 OK    状态码：200
Remote（远程） Address:14.215.177.39:443
```

```java
Accept:text/html  
Accept-Encoding:gzip, deflate, br
Accept-Language:zh-CN,zh;q=0.9    语言
Cache-Control:max-age=0
Connection:keep-alive
```

#### 1、请求行

- 请求行中的请求方式：GET
- 请求方式：**Get，Post**，HEAD,DELETE,PUT,TRACT…
  - get：
  
    - 请求能够携带的参数比较少，大小==有限制==，会在浏览器的URL地址栏显示数据内容，==不安全，但高效==
    - GET是最简单的HTTP方法，
    - 其主要任务就是要求服务器获得一个资源并把资源发回来，
    - 请求参数在请求行中用？号和URL区别开，所以所带的参数有限，显示在浏览器的地址栏中。
    - GET请求网址http://localhost:8080/FirstWeb/test?userName=Jack&age=20
    - GET 请求可被缓存
    - GET 请求有长度限制
  
  - post：
  
    - 请求能够携带的参数没有限制，大小==没有限制==，不会在浏览器的URL地址栏显示数据内容，==安全，但不高效。==
    - POST是一种更强大的请求，在请求的同时向服务器发送一些==表单==数据还有==二进制==数据，
    - 请求参数放在请求体中，可以传输比较大的请求参数，例如图片、视频等，
    - 浏览器的地址栏中不显示参数信息。
    - POST请求网址 [http://localhost:8080/FirstWeb/test ](http://localhost:8080/FirstWeb/test)
    - POST 请求不会被缓存
    - POST 请求对数据长度没有要求
  
    

#### 2、消息头

```java
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
```

### 4.4、Http响应

- 服务器---响应-----客户端

百度：

```java
Cache-Control:private    缓存控制
Connection:Keep-Alive    连接
Content-Encoding:gzip    编码
Content-Type:text/html   类型
```

#### 1.响应体

```java
Accept：告诉浏览器，它所支持的数据类型
Accept-Encoding：支持哪种编码格式  GBK   UTF-8   GB2312  ISO8859-1
Accept-Language：告诉浏览器，它的语言环境
Cache-Control：缓存控制
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机..../.
Refresh：告诉客户端，多久刷新一次；
Location：让网页重新定位；
```

#### 2.响应状态码

200：请求响应成功  200

3xx：请求重定向 

- 重定向：你重新到我给你新位置去；

4xx：找不到资源   404

- 资源不存在；

5xx：服务器代码错误   500       502:网关错误

#### 常见面试题

当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么？



## 5、Maven

**我为什么要学习这个技术？**

1. 在Javaweb开发中，需要使用大量的jar包，我们手动去导入；

2. 如何能够让一个东西自动帮我导入和配置这个jar包。

   由此，Maven诞生了！



### 5.1 Maven项目架构管理工具

我们目前用来就是方便导入jar包的！

Maven的核心思想：**约定大于配置**

- 有约束，不要去违反。

Maven会规定好你该如何去编写我们的Java代码，必须要按照这个规范来；

### 5.2 下载安装Maven

官网;https://maven.apache.org/

![1567842350606](JavaWeb.assets/1567842350606.png)

下载完成后，解压即可；

小狂神友情建议：电脑上的所有环境都放在一个文件夹下，方便管理；



### 5.3 配置环境变量

在我们的系统环境变量中

配置如下配置：

- M2_HOME     maven目录下的bin目录
- MAVEN_HOME      maven的目录
- 在系统的path中配置  %MAVEN_HOME%\bin

![1567842882993](JavaWeb.assets/1567842882993.png)

测试Maven是否安装成功，保证必须配置完毕！

### 5.4 阿里云镜像

![1567844609399](JavaWeb.assets/1567844609399.png)

- 镜像：mirrors
  - 作用：加速我们的下载
- 国内建议使用阿里云的镜像

```xml
<mirror>
    <id>nexus-aliyun</id>  
    <mirrorOf>*,!jeecg,!jeecg-snapshots</mirrorOf>  
    <name>Nexus aliyun</name>  
    <url>http://maven.aliyun.com/nexus/content/groups/public</url> 
</mirror>
```

### 5.5 本地仓库

在本地的仓库，远程仓库；

**建立一个本地仓库：**localRepository

```xml
<localRepository>D:\Environment\apache-maven-3.6.2\maven-repo</localRepository>
```

### 5.6、在IDEA中使用Maven

1. 启动IDEA

2. 创建一个MavenWeb项目

   ![1567844785602](JavaWeb.assets/1567844785602.png)

   ![1567844841172](JavaWeb.assets/1567844841172.png)

   ![1567844917185](JavaWeb.assets/1567844917185.png)

   ![1567844956177](JavaWeb.assets/1567844956177.png)

   ![1567845029864](JavaWeb.assets/1567845029864.png)

3. 等待项目初始化完毕

   ![1567845105970](JavaWeb.assets/1567845105970.png)

   ![1567845137978](JavaWeb.assets/1567845137978.png)

4. 观察maven仓库中多了什么东西？

5. IDEA中的Maven设置

   注意：IDEA项目创建成功后，看一眼Maven的配置

   ![1567845341956](JavaWeb.assets/1567845341956.png)

   ![1567845413672](JavaWeb.assets/1567845413672.png)

6. 到这里，Maven在IDEA中的配置和使用就OK了!

### 5.7、创建一个普通的Maven项目

![1567845557744](JavaWeb.assets/1567845557744.png)

![1567845717377](JavaWeb.assets/1567845717377.png)

这个只有在Web应用下才会有！

![1567845782034](JavaWeb.assets/1567845782034.png)

### 5.8 标记文件夹功能

![1567845910728](JavaWeb.assets/1567845910728.png)

![1567845957139](JavaWeb.assets/1567845957139.png)

![1567846034906](JavaWeb.assets/1567846034906.png)

![1567846073511](JavaWeb.assets/1567846073511.png)

### 5.9 在 IDEA中配置Tomcat

![1567846140348](JavaWeb.assets/1567846140348.png)

![1567846179573](JavaWeb.assets/1567846179573.png)

![1567846234175](JavaWeb.assets/1567846234175.png)

![1567846369751](JavaWeb.assets/1567846369751.png)

解决警告问题

必须要的配置：**为什么会有这个问题：我们访问一个网站，需要指定一个文件夹名字；**

![1567846421963](JavaWeb.assets/1567846421963.png)

![1567846546465](JavaWeb.assets/1567846546465.png)

![1567846559111](JavaWeb.assets/1567846559111.png)

![1567846640372](JavaWeb.assets/1567846640372.png)

### 5.10 pom文件

pom.xml 是Maven的核心配置文件

![1567846784849](JavaWeb.assets/1567846784849.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--Maven版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!--这里就是我们刚才配置的GAV-->
  <groupId>com.kuang</groupId>
  <artifactId>javaweb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <!--Package：项目的打包方式
  jar：java应用
  war：JavaWeb应用
  -->
  <packaging>war</packaging>


  <!--配置-->
  <properties>
    <!--项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--编码版本-->
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <!--项目依赖-->
  <dependencies>
    <!--具体依赖的jar包配置文件-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
    </dependency>
  </dependencies>

  <!--项目构建用的东西-->
  <build>
    <finalName>javaweb-01-maven</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

![1567847410771](JavaWeb.assets/1567847410771.png)



maven由于他的约定大于配置，我们之后可以能遇到我们写的配置文件，无法被导出或者生效的问题，解决方案：

```xml
<!--在build中配置resources，来防止我们资源导出失败的问题-->
<build>
    <resources>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
    </resources>
</build>
```



### 5.12 IDEA操作

![1567847630808](JavaWeb.assets/1567847630808.png)



![1567847662429](JavaWeb.assets/1567847662429.png)



### 5.13 解决遇到的问题

1. Maven 3.6.2

   解决方法：降级为3.6.1

   ![1567904721301](JavaWeb.assets/1567904721301.png)

2. Tomcat闪退

   

3. IDEA中每次都要重复配置Maven
   在IDEA中的全局默认配置中去配置

   ![1567905247201](JavaWeb.assets/1567905247201.png)

   ![1567905291002](JavaWeb.assets/1567905291002.png)

4. Maven项目中Tomcat无法配置

5. maven默认web项目中的web.xml版本问题

   ![1567905537026](JavaWeb.assets/1567905537026.png)

6. 替换为webapp4.0版本和tomcat一致

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0"
            metadata-complete="true">
   
   
   
   </web-app>
   ```

   

7. Maven仓库的使用

   地址：https://mvnrepository.com/

   ![1567905870750](JavaWeb.assets/1567905870750.png)

   ![1567905982979](JavaWeb.assets/1567905982979.png)

   ![1567906017448](JavaWeb.assets/1567906017448.png)

   ![1567906039469](JavaWeb.assets/1567906039469.png)



## 6、Servlet

### 6.1、Servlet简介

- Servlet就是sun公司开发动态web的一门技术，为了能够实现聊天，发帖这样的一些交互功能
- Servlet由服务器调用，运行在服务器端
- Sun在这些API中提供一个接口叫做：Servlet，如果你想开发一个Servlet程序，只需要完成两个小步骤：
  - 编写一个类，实现Servlet接口
  - 把开发好的Java类部署到web服务器中。
- **把实现了Servlet接口的Java程序叫做，Servlet**

### 6.2、HelloServlet

#### 1 Servlet入门

- Servlet（Server Applet）是Java Servlet的简称，称为小服务程序或服务连接器，用Java编写的服务器端程序，具有独立于平台和协议的特性，主要功能在于交互式地浏览和生成数据，生成动态Web内容。

- 狭义的Servlet是指Java语言实现的一个接口，广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。Servlet运行于支持Java的应用服务器中。

- Servlet 的主要功能在于交互式地浏览和修改数据，生成动态 Web 内容。

- 这个==过程==为：

  1、客户端发送请求至服务器端；

  2、服务器将请求信息发送至 Servlet；

  3、Servlet 生成响应内容并将其传给服务器。响应内容动态生成，通常取决于客户端的请求；

  4、服务器将响应返回给客户端。

- Serlvet接口Sun公司有两个默认的实现类：HttpServlet，GenericServlet
- 配置web.xml

```xml
<!-- 注册一个Servlet -->
<servlet>
   <!-- Servlet标识名 -->
   <servlet-name>HelloServlet</servlet-name>
   <!-- Servlet类的全限定名 -->
   <servlet-class>com.aaa.servlet.HelloServlet</servlet-class>​
</servlet>

<!-- 配置Servlet映射信息 -->
<servlet-mapping>
   <!-- Servlet标识名和上面一致 -->
   <servlet-name>HelloServlet</servlet-name>
   <!-- 访问路径 -->
   <url-pattern>/hello</url-pattern>
</servlet-mapping>
```



1. 构建一个普通的Maven项目，删掉里面的src目录，以后我们的学习就在这个项目里面建立Moudel；这个空的工程就是Maven主工程；

2. 关于Maven父子工程的理解：

   父项目中会有

   ```xml
       <modules>
           <module>servlet-01</module>
       </modules>
   ```

   子项目会有

   ```xml
       <parent>
           <artifactId>javaweb-02-servlet</artifactId>
           <groupId>com.kuang</groupId>
           <version>1.0-SNAPSHOT</version>
       </parent>
   ```

   父项目中的java子项目可以直接使用

   ```java
   son extends father
   ```

3. Maven环境优化

   1. 修改web.xml为最新的
   2. 将maven的结构搭建完整

4. 编写一个Servlet程序

   ![1567911804700](JavaWeb.assets/1567911804700.png)

   1. 编写一个普通类

   2. 实现Servlet接口，这里我们直接继承HttpServlet

      ```java
      public class HelloServlet extends HttpServlet {
          
          //由于get或者post只是请求实现的不同的方式，可以相互调用，业务逻辑都一样；
          @Override
          protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
              //ServletOutputStream outputStream = resp.getOutputStream();
              PrintWriter writer = resp.getWriter(); //响应流
              writer.print("Hello,Serlvet");
          }
      
          @Override
          protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
              doGet(req, resp);
          }
      }
      
      ```

5. 编写Servlet的映射

   为什么需要映射：我们写的是JAVA程序，但是要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要再web服务中注册我们写的Servlet，还需给他一个浏览器能够访问的路径；

   ```xml
   
       <!--注册Servlet-->
       <servlet>
           <servlet-name>hello</servlet-name>
           <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
       </servlet>
       <!--Servlet的请求路径-->
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello</url-pattern>
       </servlet-mapping>
   
   ```

6. 配置Tomcat

   注意：配置项目发布的路径就可以了

7. 启动测试，OK！



#### 2 ServletAPI层次结构

**核心技能部分**

​     ![222](JavaWeb.assets/clip_image001.png)

​       ![Serv et  Servi  Serv IetCmf i g  -se rServIe 'Cca rex : O  HttpServ1et  service Cin EttpServletReque;t. ia  et (JavaWeb.assets/clip_image001-1583302830910.jpg) ](file:///C:/Users/YANKUN~1/AppData/Local/Temp/msohtmlclip1/01/clip_image001.jpg)  

**Servlet原理**

##### Servlet接口

- Servlet接口定义了所有 Servlet需要实现的方法， 包括==init()，service()，destroy ()==方法， 以及getServletConfig()方法（返回ServletConfig对象，通过该对象可以得到Servlet的配置信息）。

##### ServletConfig接口

- 在Servlet初始化时，Servlet容器会使用ServletConfig对象向该Servlet传递信息。

- **ServletConfig的常用方法**

| **方法**                              | **功能说明**                          |
| ------------------------------------- | ------------------------------------- |
| String  getInitParameter(String name) | 获取web.xml中名称为name的初始化参数值 |
| ServletContext  getServletContext()   | 返回Servlet上下文对象                 |

##### GenericServlet类

- 抽象类 GenericServlet实现了Servlet接口和ServletConfig接口，简单实现除 service()方法外的其它方法，它定义了通用的，不依赖于协议的Servlet规范。 GenericServlet类的常用方法如表2.2.3所示。

- **GenericServlet类的常用方法**

| **方法**                              | **功能说明**                 |
| ------------------------------------- | ---------------------------- |
| void  init(ServletConfig config)      | 初始化方法                   |
| String  getInitParameter(String name) | 返回名称为name的初始化参数值 |
| ServletContext  getServletCotext()    | 返回ServletContext对象       |

##### HttpServlet类

- 抽象类HttpServlet继承自GenericServlet类，专门用来处理HTTP请求，并提供了与HTTP相关的实现方法。根据HTTP协议的特点， HttpServlet分别提供了处理请求的相应方法，如表2.2.4所示。

- **HttpServlet类的常用方法**

| **方法**                                                     | **功能说明**                                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| void ==service==  (ServletRequest reg, ServletResponse res)  | 接收客户端请求，然后把请求分发给相应的doXX方法，如果是GET请求就分发给doGet()方法，如果是POST请求就分发给doPost()方法。 |
| void  ==doGet==(HttpServletRequest reg, HttpServletResponse res) | 处理GET请求                                                  |
| void  ==doPost==(HttpServletRequest reg, HttpServletResponse res) | 处理POST请求                                                 |

- 如果要自己要编写Servlet程序， 都是继承HttpServlet类， 然后重写其中的某些方法， 使用原则如下：

  (1) 重写doGet方法来处理GET请求。

  (2) 重写doPost方法来处理POST请求。

  (3) 如果需要在Servlet实例化中进行初始化工作，可以重写init()方法。

  (4) 如果需要在 Servlet被释放时进行资源清理的工作，可以重写destroy()方法。

- **提示：**
  
  - HTTP 请求主要就 get 和 post两种， 为了让 servlet两种请求都能处理，一般doGet ()和doPost()方法都重写，而处理代码只写在一个方法中，另外一个方法调用即可。

##### HttpServletRequest接口

- HttpServletRequest接口继承自ServletRequest接口，它代表客户的请求。
- 容器在调用Servlet的doGet()和doPost()方法时，会创建一个HttpServletRequest接口的实例，作为参数传给doGet()或doPost()方法。

- **HttpServleRequest 接口的常用方法**

| **方法**                                         | **功能说明**                                                 |
| ------------------------------------------------ | ------------------------------------------------------------ |
| String  ==getParameter==(String name)            | 根据页面表单元素名称获取页面提交数据                         |
| string[]  ==getPararneterValues== (String name)  | 获取页面有重名表单元素（比如复选框）的值                     |
| void  ==setCharacterEncoding== (String name)     | 设置请求的编码，在调用getParameter()方法  前进行设置，此方法可以解决提供中文数据乱码问题。 |
| void  ==setAttribute==(String name,Object value) | 设置请求的参数                                               |
| ==getRequestDispatcher==(String  path)           | 返回一个RequestDispatcher对象，该对象的  forward方法可以把请求转发到指定资源 |

##### HttpServletResponse接口

- HttpServletResponse接口继承自ServletResponse接口，它代表向客户端发送的响应。
- 容器在调用Servlet的doGet()和doPost()方法时，同样会创建一个 HttpServletResponse接口的实例，作为参数传给doGet()或doPost()方法。
- Servlet利用HttpServletRequest对象获取客户端的请求数据，经过处理后由 HttpServletResponse对象发送响应数据。

- **HttpServleRequest 接口的常用方法**

| **方法**                                   | **功能说明**       |
| ------------------------------------------ | ------------------ |
| setContentType("text/html;charset=utf-8"); | 设置响应的内容类型 |
| PrintWriter  response.getWriter()          | 获得响应的输出流   |
| response.sendRedirect(redirect)            | 重定向到指定的网址 |

#####  转发与重定向

**1 转发**

- 转发属于**服务器跳转**。当使用转发时，JSP容器将使用一个内部的方法来调用目标页面，新的页面继续处理同一个请求，而浏览器将不会知道这个过程。

- 整个过程都是在一个Web容器内完成，因而可以共享request范围内的数据。

- 而对应到客户端，不管服务器内部如何处理，作为浏览器都只是提交了一个请求，因而客户端的URL地址不会发生改变。

- 转发的作用：在多个页面交互过程中实现请求数据的共享。

- 实现转发分为两个步骤：

  1、 需要先获取RequestDispatcher实例

  dispatcher=request.getRequestDispatcher("servlet2");

  2、 调用forward方法

  dispatcher.forward(request, response);

 

**2 重定向**

- 重定向是**客户端跳转**。
- 重定向方式的含义是第一个页面通知浏览器发送一个新的页面请求。
- 因为，当你使用重定向时，浏览器中所显示的URL会变成新页面的URL。
- 同时，由于重定向方式产生了一个新的请求，所以经过一次重定向后，request内的对象将无法使用。

- 重定向需要使用HttpServletResponse对象的==sendRedirect==()方法实现

  

**3 转发与重定向的区别**

- 转发是继续传递、处理==同一个请求==，在==服务器端==进行；
  - 重定向在==客户端==运行，会产生==新请求==。

- 转发时浏览器地址栏中显示的是==初次发出请求的地址==；
  - 重定向时浏览器地址栏中==不再是初次==请求的地址，而是==最后响应==的那个地址。

- 转发时最终的servlet中，request对象和中转的那个request对象是==同一个==；
  - 重定向最终的servlet中，request对象和中转的那个request对象==不是同一个==。

- 转发只能转发给==当前web应用==的资源； 
  - 重定可以重定向到==任何==资源。



##### Servlet应用

**使用Servlet处理客户端请求** 

前面学习了Servlet的主要作用就是接受客户端请求并返回响应，接下来就通过一个用户登陆功能示例， 学习使用Servlet处理客户端请求,

**获得Servlet初始化参数**

通过Servlet的doGet()和doPost()，可以处理客户端请求并获得表单提交的数据。当然我们也可以对Servlet进行初始化设置，在Servlet加载时就对参数进行初始化。设置初 始化参数首先要在web.xml中的<servlet>元素中使用<init-param>元素进行设置，

**Servlet访问数据库**

进一步完善登录代码，需要连接数据库进行用户名和密码的校验，我们需要建立BaseDao(之前所学)、实体类、Dao接口和Dao实现类。

##### ==Servlet的生命周期==

Servlet部署在容器中，其生命周期由容器来管理，可以概括为以下5个阶段：

1. 加载
2. 实例化
3. 初始化
4. 服务
5. 销毁

### 6.3、Servlet原理

Servlet是由Web服务器调用，web服务器在收到浏览器请求之后，会：

![1567913793252](JavaWeb.assets/1567913793252.png)

### 6.4、Mapping问题

1. 一个Servlet可以指定一个映射路径

   ```xml
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello</url-pattern>
       </servlet-mapping>
   ```

2. 一个Servlet可以指定多个映射路径

   ```xml
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello</url-pattern>
       </servlet-mapping>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello2</url-pattern>
       </servlet-mapping>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello3</url-pattern>
       </servlet-mapping>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello4</url-pattern>
       </servlet-mapping>
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello5</url-pattern>
       </servlet-mapping>
   
   ```

3. 一个Servlet可以指定通用映射路径

   ```xml
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello/*</url-pattern>
       </servlet-mapping>
   ```

4. 默认请求路径

   ```xml
       <!--默认请求路径-->
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/*</url-pattern>
       </servlet-mapping>
   ```

5. 指定一些后缀或者前缀等等….

   ```xml
   
   <!--可以自定义后缀实现请求映射
       注意点，*前面不能加项目映射的路径
       hello/sajdlkajda.qinjiang
       -->
   <servlet-mapping>
       <servlet-name>hello</servlet-name>
       <url-pattern>*.qinjiang</url-pattern>
   </servlet-mapping>
   ```

6. 优先级问题
   指定了固有的映射路径优先级最高，如果找不到就会走默认的处理请求；

   ```xml
   <!--404-->
   <servlet>
       <servlet-name>error</servlet-name>
       <servlet-class>com.kuang.servlet.ErrorServlet</servlet-class>
   </servlet>
   <servlet-mapping>
       <servlet-name>error</servlet-name>
       <url-pattern>/*</url-pattern>
   </servlet-mapping>
   
   ```

   

### 6.5、ServletContext

web容器在启动的时候，它会为每个web程序都创建一个对应的ServletContext对象，它代表了当前的web应用；

#### 1、共享数据

我在这个Servlet中保存的数据，可以在另外一个servlet中拿到；

```java
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        
        //this.getInitParameter()   初始化参数
        //this.getServletConfig()   Servlet配置
        //this.getServletContext()  Servlet上下文
        ServletContext context = this.getServletContext();

        String username = "秦疆"; //数据
        context.setAttribute("username",username); //将一个数据保存在了ServletContext中，名字为：username 。值 username

    }

}

```

```java
public class GetServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        String username = (String) context.getAttribute("username");

        resp.setContentType("text/html");
        resp.setCharacterEncoding("utf-8");
        resp.getWriter().print("名字"+username);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

```XML
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>getc</servlet-name>
        <servlet-class>com.kuang.servlet.GetServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>getc</servlet-name>
        <url-pattern>/getc</url-pattern>
    </servlet-mapping>
```

测试访问结果；



#### 2、获取初始化参数

```xml
    <!--配置一些web应用初始化参数-->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
    </context-param>
```

```java
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    ServletContext context = this.getServletContext();
    String url = context.getInitParameter("url");
    resp.getWriter().print(url);
}
```

#### 3、请求转发

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    ServletContext context = this.getServletContext();
    System.out.println("进入了ServletDemo04");
    //RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp"); //转发的请求路径
    //requestDispatcher.forward(req,resp); //调用forward实现请求转发；
    context.getRequestDispatcher("/gp").forward(req,resp);
}
```

<img src="JavaWeb.assets/1567924457532.png" alt="1567924457532" style="zoom: 80%;" />

#### 4、读取资源文件

Properties

- 在java目录下新建properties
- 在resources目录下新建properties

发现：都被打包到了同一个路径下：classes，我们俗称这个路径为classpath:

思路：需要一个文件流；

```properties
username=root12312
password=zxczxczxc
```

```java
public class ServletDemo05 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/com/kuang/servlet/aa.properties");

        Properties prop = new Properties();
        prop.load(is);
        String user = prop.getProperty("username");
        String pwd = prop.getProperty("password");

        resp.getWriter().print(user+":"+pwd);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

访问测试即可ok；

### 6.6、HttpServletResponse

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletRequest对象，代表响应的一个HttpServletResponse；

- 如果要获取客户端请求过来的参数：找HttpServletRequest
- 如果要给客户端响应一些信息：找HttpServletResponse

#### 1、简单分类

负责向浏览器发送数据的方法

```java
ServletOutputStream getOutputStream() throws IOException;
PrintWriter getWriter() throws IOException;
```

负责向浏览器发送响应头的方法

```java
    void setCharacterEncoding(String var1);

    void setContentLength(int var1);

    void setContentLengthLong(long var1);

    void setContentType(String var1);

    void setDateHeader(String var1, long var2);

    void addDateHeader(String var1, long var2);

    void setHeader(String var1, String var2);

    void addHeader(String var1, String var2);

    void setIntHeader(String var1, int var2);

    void addIntHeader(String var1, int var2);
```

响应的状态码

```java
    int SC_CONTINUE = 100;
    int SC_SWITCHING_PROTOCOLS = 101;
    int SC_OK = 200;
    int SC_CREATED = 201;
    int SC_ACCEPTED = 202;
    int SC_NON_AUTHORITATIVE_INFORMATION = 203;
    int SC_NO_CONTENT = 204;
    int SC_RESET_CONTENT = 205;
    int SC_PARTIAL_CONTENT = 206;
    int SC_MULTIPLE_CHOICES = 300;
    int SC_MOVED_PERMANENTLY = 301;
    int SC_MOVED_TEMPORARILY = 302;
    int SC_FOUND = 302;
    int SC_SEE_OTHER = 303;
    int SC_NOT_MODIFIED = 304;
    int SC_USE_PROXY = 305;
    int SC_TEMPORARY_REDIRECT = 307;
    int SC_BAD_REQUEST = 400;
    int SC_UNAUTHORIZED = 401;
    int SC_PAYMENT_REQUIRED = 402;
    int SC_FORBIDDEN = 403;
    int SC_NOT_FOUND = 404;
    int SC_METHOD_NOT_ALLOWED = 405;
    int SC_NOT_ACCEPTABLE = 406;
    int SC_PROXY_AUTHENTICATION_REQUIRED = 407;
    int SC_REQUEST_TIMEOUT = 408;
    int SC_CONFLICT = 409;
    int SC_GONE = 410;
    int SC_LENGTH_REQUIRED = 411;
    int SC_PRECONDITION_FAILED = 412;
    int SC_REQUEST_ENTITY_TOO_LARGE = 413;
    int SC_REQUEST_URI_TOO_LONG = 414;
    int SC_UNSUPPORTED_MEDIA_TYPE = 415;
    int SC_REQUESTED_RANGE_NOT_SATISFIABLE = 416;
    int SC_EXPECTATION_FAILED = 417;
    int SC_INTERNAL_SERVER_ERROR = 500;
    int SC_NOT_IMPLEMENTED = 501;
    int SC_BAD_GATEWAY = 502;
    int SC_SERVICE_UNAVAILABLE = 503;
    int SC_GATEWAY_TIMEOUT = 504;
    int SC_HTTP_VERSION_NOT_SUPPORTED = 505;
```

#### 2、下载文件

1. 向浏览器输出消息 （一直在讲，就不说了）
2. 下载文件
   1. 要获取下载文件的路径
   2. 下载的文件名是啥？
   3. 设置想办法让浏览器能够支持下载我们需要的东西
   4. 获取下载文件的输入流
   5. 创建缓冲区
   6. 获取OutputStream对象
   7. 将FileOutputStream流写入到buffer缓冲区
   8. 使用OutputStream将缓冲区中的数据输出到客户端！

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // 1. 要获取下载文件的路径
    String realPath = "F:\\班级管理\\西开【19525】\\2、代码\\JavaWeb\\javaweb-02-servlet\\response\\target\\classes\\秦疆.png";
    System.out.println("下载文件的路径："+realPath);
    // 2. 下载的文件名是啥？
    String fileName = realPath.substring(realPath.lastIndexOf("\\") + 1);
    // 3. 设置想办法让浏览器能够支持(Content-Disposition)下载我们需要的东西,中文文件名URLEncoder.encode编码，否则有可能乱码
    resp.setHeader("Content-Disposition","attachment;filename="+URLEncoder.encode(fileName,"UTF-8"));
    // 4. 获取下载文件的输入流
    FileInputStream in = new FileInputStream(realPath);
    // 5. 创建缓冲区
    int len = 0;
    byte[] buffer = new byte[1024];
    // 6. 获取OutputStream对象
    ServletOutputStream out = resp.getOutputStream();
    // 7. 将FileOutputStream流写入到buffer缓冲区,使用OutputStream将缓冲区中的数据输出到客户端！
    while ((len=in.read(buffer))>0){
        out.write(buffer,0,len);
    }

    in.close();
    out.close();
}
```

#### 3、验证码功能

验证怎么来的？

- 前端实现
- 后端实现，需要用到 Java 的图片类，生产一个图片

```java
package com.kuang.servlet;

import javax.imageio.ImageIO;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.IOException;
import java.util.Random;

public class ImageServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //如何让浏览器3秒自动刷新一次;
        resp.setHeader("refresh","3");
        
        //在内存中创建一个图片
        BufferedImage image = new BufferedImage(80,20,BufferedImage.TYPE_INT_RGB);
        //得到图片
        Graphics2D g = (Graphics2D) image.getGraphics(); //笔
        //设置图片的背景颜色
        g.setColor(Color.white);
        g.fillRect(0,0,80,20);
        //给图片写数据
        g.setColor(Color.BLUE);
        g.setFont(new Font(null,Font.BOLD,20));
        g.drawString(makeNum(),0,20);

        //告诉浏览器，这个请求用图片的方式打开
        resp.setContentType("image/jpeg");
        //网站存在缓存，不让浏览器缓存
        resp.setDateHeader("expires",-1);
        resp.setHeader("Cache-Control","no-cache");
        resp.setHeader("Pragma","no-cache");

        //把图片写给浏览器
        ImageIO.write(image,"jpg", resp.getOutputStream());

    }

    //生成随机数
    private String makeNum(){
        Random random = new Random();
        String num = random.nextInt(9999999) + "";
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < 7-num.length() ; i++) {
            sb.append("0");
        }
        num = sb.toString() + num;
        return num;
    }


    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

```

#### 4、实现重定向

![1567931587955](JavaWeb.assets/1567931587955.png)

B一个web资源收到客户端A请求后，B他会通知A客户端去访问另外一个web资源C，这个过程叫重定向

常见场景：

- 用户登录

```java
void sendRedirect(String var1) throws IOException;
```

测试：

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    /*
        resp.setHeader("Location","/r/img");
        resp.setStatus(302);
         */
    resp.sendRedirect("/r/img");//重定向
}
```

面试题：请你聊聊重定向和转发的区别？

相同点

- 页面都会实现跳转

不同点

- 请求转发的时候，url不会产生变化
- 重定向时候，url地址栏会发生变化；

![1567932163430](JavaWeb.assets/1567932163430.png)

#### 5、简单实现登录重定向

```jsp
<%--这里提交的路径，需要寻找到项目的路径--%>
<%--${pageContext.request.contextPath}代表当前的项目--%>

<form action="${pageContext.request.contextPath}/login" method="get">
    用户名：<input type="text" name="username"> <br>
    密码：<input type="password" name="password"> <br>
    <input type="submit">
</form>

```

```JAVA

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //处理请求
        String username = req.getParameter("username");
        String password = req.getParameter("password");

        System.out.println(username+":"+password);

        //重定向时候一定要注意，路径问题，否则404；
        resp.sendRedirect("/r/success.jsp");
    }

```

```xml
  <servlet>
    <servlet-name>requset</servlet-name>
    <servlet-class>com.kuang.servlet.RequestTest</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>requset</servlet-name>
    <url-pattern>/login</url-pattern>
  </servlet-mapping>
```

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>

<h1>Success</h1>

</body>
</html>

```

### 6.7、HttpServletRequest

HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，HTTP请求中的所有信息会被封装到HttpServletRequest，通过这个HttpServletRequest的方法，获得客户端的所有信息；

![1567933996830](JavaWeb.assets/1567933996830.png)

![1567934023106](JavaWeb.assets/1567934023106.png)

#### 获取参数，请求转发

![1567934110794](JavaWeb.assets/1567934110794.png)

```java
@Override
protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    req.setCharacterEncoding("utf-8");
    resp.setCharacterEncoding("utf-8");

    String username = req.getParameter("username");
    String password = req.getParameter("password");
    String[] hobbys = req.getParameterValues("hobbys");
    System.out.println("=============================");
    //后台接收中文乱码问题
    System.out.println(username);
    System.out.println(password);
    System.out.println(Arrays.toString(hobbys));
    System.out.println("=============================");


    System.out.println(req.getContextPath());
    //通过请求转发
    //这里的 / 代表当前的web应用
    req.getRequestDispatcher("/success.jsp").forward(req,resp);

}
```

**面试题：请你聊聊重定向和转发的区别？**

相同点

- 页面都会实现跳转

不同点

- 请求转发的时候，url不会产生变化   307
- 重定向时候，url地址栏会发生变化； 302

### 6.8、处理中文乱码

```xml
注册
<form action="show.jsp" method="post">
  <input  type="text" name="name">
  <input  type="submit" value="注册">
  </form>  
   <%//脚本段
   String name = request.getParameter("name");
    %>    
    name:<%=name %>   //表达式
     This is my JSP page. <br>
//处理中文乱码
1.
   <%
   request.setCharacterEncoding("UTF-8");
   response.setContentType("text/html;charset=utf-8");
   String name = request.getParameter("name");
   %>
2.
    <%
   response.setContentType("text/html;charset=utf-8");
   String name = request.getParameter("name");   
   name = new String(name.getBytes("ISO-8859-1"),"utf-8");
    %>    
    name:<%=name %>

```



## 7、Cookie、Session

### 7.1、会话

**会话**：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话；

**有状态会话**：一个同学来过教室，下次再来教室，我们会知道这个同学，曾经来过，称之为有状态会话；

**你能怎么证明你是西开的学生？**

你              西开

1. 发票                西开给你发票
2. 学校登记        西开标记你来过了

**一个网站，怎么证明你来过？**

客户端              服务端

1. 服务端给客户端一个 信件，客户端下次访问服务端带上信件就可以了； cookie
2. 服务器登记你来过了，下次你来的时候我来匹配你； session



### 7.2、保存会话的两种技术

**cookie**

- 客户端技术   （响应，请求）

**session**

- 服务器技术，利用这个技术，可以保存用户的会话信息？ 我们可以把信息或者数据放在Session中！



常见常见：网站登录之后，你下次不用再登录了，第二次访问直接就上去了！

### 7.3、Cookie

![image-20220116000147458](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220116000147458.png)

1. 从请求中拿到cookie信息
2. 服务器响应给客户端cookie（充当数据载体）

```java
Cookie[] cookies = req.getCookies(); //获得Cookie
cookie.getName(); //获得cookie中的key
cookie.getValue(); //获得cookie中的value
new Cookie("lastLoginTime", System.currentTimeMillis()+""); //新建一个cookie
cookie.setMaxAge(24*60*60); //设置cookie的有效期
resp.addCookie(cookie); //响应给客户端一个cookie
```

**cookie：一般会保存在本地的 用户目录下 appdata；**



一个网站cookie是否存在上限！**聊聊细节问题**

- 一个Cookie只能保存一个信息；
- 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie；
- Cookie大小有限制4kb；
- 300个cookie浏览器上限



**删除Cookie；**

- 不设置有效期，关闭浏览器，自动失效；
- 设置有效期时间为 0 ；



**编码解码：**

```java
URLEncoder.encode("秦疆","utf-8")
URLDecoder.decode(cookie.getValue(),"UTF-8")
```



### 7.4、Session（重点）

![image-20220116000724750](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220116000724750.png)

这里服务器发送SessionID（在外人看来就是没有规律的字符串）利用了cookie，服务器设置cookie并且把SessionID放入到cookie中，再把会话结束时间对应设置为这个Cookie的有效期，浏览器拿到cookie以后对SessionID进行保存（相当于给用户名和密码加密了），而且服务器在发送Cookie之前是会对这个含有SessionID的Cookie进行签名，换句话说就是如果黑客拿到SessionID，SessionID就会变成服务器识别不了的字符串。

什么是Session：

- 服务器会给每一个用户（浏览器）创建一个Session对象；
- 一个Session独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
- 用户登录之后，整个网站它都可以访问！--> 保存用户的信息；保存购物车的信息…..

Session和cookie的区别：

- Cookie是把用户的数据写给用户的浏览器，浏览器保存 （可以保存多个）
- Session把用户的数据写到用户独占Session中，服务器端保存  （保存重要的信息，减少服务器资源的浪费）
- Session对象由服务创建；



使用场景：

- 保存一个登录用户的信息；
- 购物车信息；
- 在整个网站中经常会使用的数据，我们将它保存在Session中；



使用Session：

```java
package com.kuang.servlet;

import com.kuang.pojo.Person;

import javax.servlet.ServletException;
import javax.servlet.http.*;
import java.io.IOException;

public class SessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        
        //解决乱码问题
        req.setCharacterEncoding("UTF-8");
        resp.setCharacterEncoding("UTF-8");
        resp.setContentType("text/html;charset=utf-8");
        
        //得到Session
        HttpSession session = req.getSession();
        //给Session中存东西
        session.setAttribute("name",new Person("秦疆",1));
        //获取Session的ID
        String sessionId = session.getId();

        //判断Session是不是新创建
        if (session.isNew()){
            resp.getWriter().write("session创建成功,ID:"+sessionId);
        }else {
            resp.getWriter().write("session以及在服务器中存在了,ID:"+sessionId);
        }

        //Session创建的时候做了什么事情；
//        Cookie cookie = new Cookie("JSESSIONID",sessionId);
//        resp.addCookie(cookie);

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}

//得到Session
HttpSession session = req.getSession();

Person person = (Person) session.getAttribute("name");

System.out.println(person.toString());

HttpSession session = req.getSession();
session.removeAttribute("name");
//手动注销Session
session.invalidate();
```



**会话自动过期：web.xml配置**

```xml
<!--设置Session默认的失效时间-->
<session-config>
    <!--15分钟后Session自动失效，以分钟为单位-->
    <session-timeout>15</session-timeout>
</session-config>
```



![image-20220116002319147](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220116002319147.png)

### 简单介绍一下token

JSON Web Token（JWT）

用户第一次登录网络以后，服务器就会生成一个JWT，服务器不需要保存这个JWT，只需要保存JWT签名的密文，接着把JWT发送给浏览器，JWT在浏览器以Cookie或者Storage形式存储。假设以cookie的形式保存下来，用户每次发送请求都会把这个JWT发给服务器，用户就不需要重新输入账号密码了。

JWT由三部分组成：header.payload.signature 三个部分是相关联的，因此有一定安全性

![image-20220116004623493](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220116004623493.png)

![image-20220116004817972](C:\Users\10130\AppData\Roaming\Typora\typora-user-images\image-20220116004817972.png)



token是诞生于服务器，保存于浏览器这边的，有客户端主导一切，可以放在Cookie或者Storage里面，持有token就像持有“令牌”一样可以允许访问服务器。关键在于token使用的某种算法根据用户签名和其他一些信息生成的令牌信息是一致的，可以验证通过，对于用户量庞大的系统或者分布式，避免了大量session对象的存储带来的内存消耗，和各服务器之间的session的复制或者专门用于存储session的服务器gg带来的问题。

## 8、JSP

==**静态网页&动态网页**==

|          | **静态网页** | **动态网页**                |
| -------- | ------------ | --------------------------- |
| 组成     | html+js+css  | jsp+html;asp+html;php+html; |
| 交互     | 不可交互     | 可交互                      |
| 运行方式 | 客户端运行   | 服务端生成，客户端运行      |
| 数据库   | 无数据库连接 | 连接数据库                  |

### 8.1、什么是JSP

- Java Server Pages ： Java服务器端页面，也和Servlet一样，用于动态Web技术！
- http://127.0.0.1:8080/login/index.jsp

- 最大的特点：
  - 写JSP就像在写HTML
  - 区别：
    - HTML只给用户提供静态的数据
    - JSP页面中可以嵌入JAVA代码，为用户提供动态数据；

- **工作原理**

  - 客户端请求
  - 把 *.jsp 翻译成 *.java 
  - 编译为 *.class
  - 执行生成servlet
  - 反馈结果给客户端显示
              第二次访问 有改动 执行上述过程 
              无改动 直接执行

  - ​     ![123](JavaWeb.assets/clip_image001-1583305097106.png)
  - ​     <img src="JavaWeb.assets/clip_image001-1583305111348.png" alt="112" style="zoom:80%;" />
  - ​     ![44](JavaWeb.assets/clip_image001-1583305154041.png)
  - ​     ![54](JavaWeb.assets/clip_image001-1583305166669.png)

### 8.2、JSP原理

思路：JSP到底怎么执行的！

- 代码层面没有任何问题

- 服务器内部工作

  tomcat中有一个work目录；

  IDEA中使用Tomcat的会在IDEA的tomcat中生产一个work目录

  ![1568345873736](JavaWeb.assets/1568345873736.png)

  我电脑的地址：

  ```java
  C:\Users\Administrator\.IntelliJIdea2018.1\system\tomcat\Unnamed_javaweb-session-cookie\work\Catalina\localhost\ROOT\org\apache\jsp
  ```

  发现页面转变成了Java程序！

  ![1568345948307](JavaWeb.assets/1568345948307.png)



**浏览器向服务器发送请求，不管访问什么资源，其实都是在访问Servlet！**

JSP最终也会被转换成为一个Java类！

**JSP 本质上就是一个Servlet**

```java
//初始化
  public void _jspInit() {
      
  }
//销毁
  public void _jspDestroy() {
  }
//JSPService
  public void _jspService(.HttpServletRequest request,HttpServletResponse response)
      
```

1. 判断请求

2. 内置一些对象

   ```java
   final javax.servlet.jsp.PageContext pageContext;  //页面上下文
   javax.servlet.http.HttpSession session = null;    //session
   final javax.servlet.ServletContext application;   //applicationContext
   final javax.servlet.ServletConfig config;         //config
   javax.servlet.jsp.JspWriter out = null;           //out
   final java.lang.Object page = this;               //page：当前
   HttpServletRequest request                        //请求
   HttpServletResponse response                      //响应
   ```

3. 输出页面前增加的代码

   ```java
   response.setContentType("text/html");       //设置响应的页面类型
   pageContext = _jspxFactory.getPageContext(this, request, response,
                                             null, true, 8192, true);
   _jspx_page_context = pageContext;
   application = pageContext.getServletContext();
   config = pageContext.getServletConfig();
   session = pageContext.getSession();
   out = pageContext.getOut();
   _jspx_out = out;
   ```

4. 以上的这些个对象我们可以在JSP页面中直接使用！

![1568347078207](JavaWeb.assets/1568347078207.png)



在JSP页面中；

只要是 JAVA代码就会原封不动的输出；

如果是HTML代码，就会被转换为：

```java
out.write("<html>\r\n");
```

这样的格式，输出到前端！



### 8.3、JSP基础语法

任何语言都有自己的语法，JAVA中有,。 JSP 作为java技术的一种应用，它拥有一些自己扩充的语法（了解，知道即可！），Java所有语法都支持！

#### JSP 的组成 [**JSP页面的构成**](https://www.cnblogs.com/yangyquin/p/5430231.html)

​     <img src="JavaWeb.assets/clip_image001-1583305406375.png" alt="54" style="zoom:50%;" />



**==1 静态页面==**

##### ==2 指令==

```xml
<%@ %>
<!--page-->
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"  contentType="text/html; charset=UTF-8" isErrorPage="true"%>

<!--include-->
<%@ include file="foot.html" %>   静态引入/静态包含
<%@ include file="foot.jsp" %>使用jsp要删除

<% String path = request.getContextPath( );
   String basePath = request.getScheme( )+"://"+request %>
<base href="<%=basePath%>">
<jsp:include page="foot.html"></jsp:include>   动态引入/动态包含
<jsp:include page="foot.jsp"></jsp:include> (可使用html/jsp)
    
<!--taglib-->
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
    
<!--======================================================================-->
    
<%@page args.... %>
<%@include file=""%>

<%--@include会将两个页面合二为一--%>

<%@include file="common/header.jsp"%>
<h1>网页主体</h1>

<%@include file="common/footer.jsp"%>

<hr>
<%--jSP标签
    jsp:include：拼接页面，本质还是三个
    --%>
<jsp:include page="/common/header.jsp"/>
<h1>网页主体</h1>
<jsp:include page="/common/footer.jsp"/>
```

##### ==3 声明==

- JSP声明：会被编译到JSP生成Java的类中！其他的，就会被生成到_jspService方法中！在JSP，嵌入Java代码即可！

```xml
在JSP页面中定义变量,方法或类  <%!  %>
<%!  String s = "这是一个声明" ;
    public  int  add(int x,int y ){
         return x+y;
     } %>
=========================================
<%!
static {
  System.out.println("Loading Servlet!");
}

private int globalVar = 0;

public void kuang(){
  System.out.println("进入了方法Kuang！");
}
%>
```

##### ==4 表达式==

```xml
<%= 变量或表达式%> 
basePath:<%=basePath%>
<body>
    <h1>当前时间： </h1>
    <%= new Date() %>
</body>
================================
<%--JSP表达式
作用：用来将程序的输出，输出到客户端
<%= 变量或者表达式%>
--%>
<%= new java.util.Date()%>
```

##### ==5 脚本段==（小脚本/代码块）

```xml
在JSP页面中执行的Java代码 
语法： <% Java代码 %>
<%  System.out.println("这是一个代码块");%>
================================================== 
<%--jsp脚本片段--%>
<%
int sum = 0;
for (int i = 1; i <=100 ; i++) {
  sum+=i;
}
out.println("<h1>Sum="+sum+"</h1>");
%>
```

```xml
<!--脚本片段的再实现-->
<%
int x = 10;
out.println(x);
%>
<p>这是一个JSP文档</p>
<%
int y = 2;
out.println(y);
%>
<hr>
<%--在代码嵌入HTML元素--%>
<%
for (int i = 0; i < 5; i++) {
%>
<h1>Hello,World  <%=i%> </h1>
<%
}
%>
```

##### ==6 标准动作==

```xml
<jsp:include page="foot.html"></jsp:include>   动态引入/动态包含
<jsp:forward page="encoding.jsp"></jsp:forward>
```

##### ==7 注释==

- JSP的注释，不会在客户端显示，HTML就会！

​     <img src="JavaWeb.assets/clip_image001-1583306258871.png" alt="87" style="zoom:50%;" />  

```xml
<!-- This is my JSP page. <br> -->

<%--  <% 
System.out.println("这是一个代码块");
%>--%>

//System.out.println("这是一个代码块");
 
/* System.out.println("这是一个代码块1"); */
```



### 8.4、9大内置对象

- PageContext    存东西
- Request     存东西
- Response
- Session      存东西
- Application   【SerlvetContext】   存东西
- config    【SerlvetConfig】
- out
- page ，不用了解
- exception

```java
pageContext.setAttribute("name1","秦疆1号"); //保存的数据只在一个页面中有效
request.setAttribute("name2","秦疆2号"); //保存的数据只在一次请求中有效，请求转发会携带这个数据
session.setAttribute("name3","秦疆3号"); //保存的数据只在一次会话中有效，从打开浏览器到关闭浏览器
application.setAttribute("name4","秦疆4号");  //保存的数据只在服务器中有效，从打开服务器到关闭服务器
```

request：客户端向服务器发送请求，产生的数据，用户看完就没用了，比如：新闻，用户看完没用的！

session：客户端向服务器发送请求，产生的数据，用户用完一会还有用，比如：购物车；

application：客户端向服务器发送请求，产生的数据，一个用户用完了，其他用户还可能使用，比如：聊天数据；

### 8.5、JSP标签、JSTL标签、EL表达式

```xml
<!-- JSTL表达式的依赖 -->
<dependency>
    <groupId>javax.servlet.jsp.jstl</groupId>
    <artifactId>jstl-api</artifactId>
    <version>1.2</version>
</dependency>
<!-- standard标签库 -->
<dependency>
    <groupId>taglibs</groupId>
    <artifactId>standard</artifactId>
    <version>1.1.2</version>
</dependency>

```

EL表达式：  ${ }

- **获取数据**
- **执行运算**
- **获取web开发的常用对象**



**JSP标签**

```jsp
<%--jsp:include--%>

<%--
http://localhost:8080/jsptag.jsp?name=kuangshen&age=12
--%>

<jsp:forward page="/jsptag2.jsp">
    <jsp:param name="name" value="kuangshen"></jsp:param>
    <jsp:param name="age" value="12"></jsp:param>
</jsp:forward>
```



**JSTL表达式**

JSTL标签库的使用就是为了弥补HTML标签的不足；它自定义许多标签，可以供我们使用，标签的功能和Java代码一样！

**格式化标签**

**SQL标签**

**XML 标签**

**核心标签** （掌握部分）

![1568362473764](JavaWeb.assets/1568362473764.png)

**JSTL标签库使用步骤**

- 引入对应的 taglib
- 使用其中的方法
- **在Tomcat 也需要引入 jstl的包，否则会报错：JSTL解析错误**

c：if

```jsp
<head>
    <title>Title</title>
</head>
<body>


<h4>if测试</h4>

<hr>

<form action="coreif.jsp" method="get">
    <%--
    EL表达式获取表单中的数据
    ${param.参数名}
    --%>
    <input type="text" name="username" value="${param.username}">
    <input type="submit" value="登录">
</form>

<%--判断如果提交的用户名是管理员，则登录成功--%>
<c:if test="${param.username=='admin'}" var="isAdmin">
    <c:out value="管理员欢迎您！"/>
</c:if>

<%--自闭合标签--%>
<c:out value="${isAdmin}"/>

</body>
```

c:choose   c:when

```jsp
<body>

<%--定义一个变量score，值为85--%>
<c:set var="score" value="55"/>

<c:choose>
    <c:when test="${score>=90}">
        你的成绩为优秀
    </c:when>
    <c:when test="${score>=80}">
        你的成绩为一般
    </c:when>
    <c:when test="${score>=70}">
        你的成绩为良好
    </c:when>
    <c:when test="${score<=60}">
        你的成绩为不及格
    </c:when>
</c:choose>

</body>
```

c:forEach

```jsp
<%

    ArrayList<String> people = new ArrayList<>();
    people.add(0,"张三");
    people.add(1,"李四");
    people.add(2,"王五");
    people.add(3,"赵六");
    people.add(4,"田六");
    request.setAttribute("list",people);
%>


<%--
var , 每一次遍历出来的变量
items, 要遍历的对象
begin,   哪里开始
end,     到哪里
step,   步长
--%>
<c:forEach var="people" items="${list}">
    <c:out value="${people}"/> <br>
</c:forEach>

<hr>

<c:forEach var="people" items="${list}" begin="1" end="3" step="1" >
    <c:out value="${people}"/> <br>
</c:forEach>

```

## 9、JavaBean

实体类

JavaBean有特定的写法：

- 必须要有一个无参构造
- 属性必须私有化
- 必须有对应的get/set方法；

一般用来和数据库的字段做映射  ORM；

ORM ：对象关系映射

- 表--->类
- 字段-->属性
- 行记录---->对象

**people表**

| id   | name    | age  | address |
| ---- | ------- | ---- | ------- |
| 1    | 秦疆1号 | 3    | 西安    |
| 2    | 秦疆2号 | 18   | 西安    |
| 3    | 秦疆3号 | 100  | 西安    |

```java
class People{
    private int id;
    private String name;
    private int id;
    private String address;
}

class A{
    new People(1,"秦疆1号",3，"西安");
    new People(2,"秦疆2号",3，"西安");
    new People(3,"秦疆3号",3，"西安");
}
```



- 过滤器
- 文件上传
- 邮件发送
- JDBC 复习 ： 如何使用JDBC ,  JDBC crud， jdbc 事务



## 10、MVC三层架构

什么是MVC：  Model     view     Controller  模型、视图、控制器

### 10.1、早些年

![1568423664332](JavaWeb.assets/1568423664332.png)

用户直接访问控制层，控制层就可以直接操作数据库；

```java
servlet--CRUD-->数据库
弊端：程序十分臃肿，不利于维护  
servlet的代码中：处理请求、响应、视图跳转、处理JDBC、处理业务代码、处理逻辑代码

架构：没有什么是加一层解决不了的！
程序猿调用
|
JDBC
|
Mysql Oracle SqlServer ....
```

### 10.2、MVC三层架构

![1568424227281](JavaWeb.assets/1568424227281.png)



Model

- 业务处理 ：业务逻辑（Service）
- 数据持久层：CRUD   （Dao）

View

- 展示数据
- 提供链接发起Servlet请求 （a，form，img…）

Controller  （Servlet）

- 接收用户的请求 ：（req：请求参数、Session信息….）

- 交给业务层处理对应的代码 

- 控制视图的跳转  

  ```java
  登录--->接收用户的登录请求--->处理用户的请求（获取用户登录的参数，username，password）---->交给业务层处理登录业务（判断用户名密码是否正确：事务）--->Dao层查询用户名和密码是否正确-->数据库
  ```



## 11、Filter （重点）

Filter：过滤器 ，用来过滤网站的数据；

- 处理中文乱码
- 登录验证….

![1568424858708](JavaWeb.assets/1568424858708.png)

Filter开发步骤：

1. 导包

2. 编写过滤器

   1. 导包不要错

      ![1568425162525](JavaWeb.assets/1568425162525.png)

      实现Filter接口，重写对应的方法即可

      ```java
      public class CharacterEncodingFilter implements Filter {
      
          //初始化：web服务器启动，就以及初始化了，随时等待过滤对象出现！
          public void init(FilterConfig filterConfig) throws ServletException {
              System.out.println("CharacterEncodingFilter初始化");
          }
      
          //Chain : 链
          /*
          1. 过滤中的所有代码，在过滤特定请求的时候都会执行
          2. 必须要让过滤器继续同行
              chain.doFilter(request,response);
           */
          public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
              request.setCharacterEncoding("utf-8");
              response.setCharacterEncoding("utf-8");
              response.setContentType("text/html;charset=UTF-8");
      
              System.out.println("CharacterEncodingFilter执行前....");
              chain.doFilter(request,response); //让我们的请求继续走，如果不写，程序到这里就被拦截停止！
              System.out.println("CharacterEncodingFilter执行后....");
          }
      
          //销毁：web服务器关闭的时候，过滤会销毁
          public void destroy() {
              System.out.println("CharacterEncodingFilter销毁");
          }
      }
      
      ```

3. 在web.xml中配置 Filter

   ```xml
   <filter>
       <filter-name>CharacterEncodingFilter</filter-name>
       <filter-class>com.kuang.filter.CharacterEncodingFilter</filter-class>
   </filter>
   <filter-mapping>
       <filter-name>CharacterEncodingFilter</filter-name>
       <!--只要是 /servlet的任何请求，会经过这个过滤器-->
       <url-pattern>/servlet/*</url-pattern>
       <!--<url-pattern>/*</url-pattern>-->
   </filter-mapping>
   ```

   

## 12、监听器

实现一个监听器的接口；（有N种）

1. 编写一个监听器

   实现监听器的接口…

   ```java
   //统计网站在线人数 ： 统计session
   public class OnlineCountListener implements HttpSessionListener {
   
       //创建session监听： 看你的一举一动
       //一旦创建Session就会触发一次这个事件！
       public void sessionCreated(HttpSessionEvent se) {
           ServletContext ctx = se.getSession().getServletContext();
   
           System.out.println(se.getSession().getId());
   
           Integer onlineCount = (Integer) ctx.getAttribute("OnlineCount");
   
           if (onlineCount==null){
               onlineCount = new Integer(1);
           }else {
               int count = onlineCount.intValue();
               onlineCount = new Integer(count+1);
           }
   
           ctx.setAttribute("OnlineCount",onlineCount);
   
       }
   
       //销毁session监听
       //一旦销毁Session就会触发一次这个事件！
       public void sessionDestroyed(HttpSessionEvent se) {
           ServletContext ctx = se.getSession().getServletContext();
   
           Integer onlineCount = (Integer) ctx.getAttribute("OnlineCount");
   
           if (onlineCount==null){
               onlineCount = new Integer(0);
           }else {
               int count = onlineCount.intValue();
               onlineCount = new Integer(count-1);
           }
   
           ctx.setAttribute("OnlineCount",onlineCount);
   
       }
   
   
       /*
       Session销毁：
       1. 手动销毁  getSession().invalidate();
       2. 自动销毁
        */
   }
   
   ```

2. web.xml中注册监听器

   ```xml
   <!--注册监听器-->
   <listener>
       <listener-class>com.kuang.listener.OnlineCountListener</listener-class>
   </listener>
   ```

3. 看情况是否使用！



## 13、过滤器、监听器常见应用

**监听器：GUI编程中经常使用；**

```java
public class TestPanel {
    public static void main(String[] args) {
        Frame frame = new Frame("中秋节快乐");  //新建一个窗体
        Panel panel = new Panel(null); //面板
        frame.setLayout(null); //设置窗体的布局

        frame.setBounds(300,300,500,500);
        frame.setBackground(new Color(0,0,255)); //设置背景颜色

        panel.setBounds(50,50,300,300);
        panel.setBackground(new Color(0,255,0)); //设置背景颜色

        frame.add(panel);

        frame.setVisible(true);

        //监听事件，监听关闭事件
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                super.windowClosing(e);
            }
        });


    }
}
```



用户登录之后才能进入主页！用户注销后就不能进入主页了！

1. 用户登录之后，向Sesison中放入用户的数据

2. 进入主页的时候要判断用户是否已经登录；要求：在过滤器中实现！

   ```java
   HttpServletRequest request = (HttpServletRequest) req;
   HttpServletResponse response = (HttpServletResponse) resp;
   
   if (request.getSession().getAttribute(Constant.USER_SESSION)==null){
       response.sendRedirect("/error.jsp");
   }
   
   chain.doFilter(request,response);
   ```




## 14、JDBC

什么是JDBC ： Java连接数据库！

![1568439601825](JavaWeb.assets/1568439601825.png)

需要jar包的支持：

- java.sql
- javax.sql
- mysql-conneter-java…  连接驱动（必须要导入）



**实验环境搭建**

```sql

CREATE TABLE users(
    id INT PRIMARY KEY,
    `name` VARCHAR(40),
    `password` VARCHAR(40),
    email VARCHAR(60),
    birthday DATE
);

INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(1,'张三','123456','zs@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(2,'李四','123456','ls@qq.com','2000-01-01');
INSERT INTO users(id,`name`,`password`,email,birthday)
VALUES(3,'王五','123456','ww@qq.com','2000-01-01');


SELECT	* FROM users;

```



导入数据库依赖

```xml
<!--mysql的驱动-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.47</version>
</dependency>
```

IDEA中连接数据库：

![1568440926845](JavaWeb.assets/1568440926845.png)



**JDBC 固定步骤：**

1. 加载驱动
2. 连接数据库,代表数据库
3. 向数据库发送SQL的对象Statement : CRUD
4. 编写SQL （根据业务，不同的SQL）
5. 执行SQL
6. 关闭连接

```java
public class TestJdbc {
    public static void main(String[] args) throws ClassNotFoundException, SQLException {
        //配置信息
        //useUnicode=true&characterEncoding=utf-8 解决中文乱码
        String url="jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";

        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //3.向数据库发送SQL的对象Statement,PreparedStatement : CRUD
        Statement statement = connection.createStatement();

        //4.编写SQL
        String sql = "select * from users";

        //5.执行查询SQL，返回一个 ResultSet  ： 结果集
        ResultSet rs = statement.executeQuery(sql);

        while (rs.next()){
            System.out.println("id="+rs.getObject("id"));
            System.out.println("name="+rs.getObject("name"));
            System.out.println("password="+rs.getObject("password"));
            System.out.println("email="+rs.getObject("email"));
            System.out.println("birthday="+rs.getObject("birthday"));
        }

        //6.关闭连接，释放资源（一定要做） 先开后关
        rs.close();
        statement.close();
        connection.close();
    }
}

```



**预编译SQL**

```java
public class TestJDBC2 {
    public static void main(String[] args) throws Exception {
        //配置信息
        //useUnicode=true&characterEncoding=utf-8 解决中文乱码
        String url="jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";

        //1.加载驱动
        Class.forName("com.mysql.jdbc.Driver");
        //2.连接数据库,代表数据库
        Connection connection = DriverManager.getConnection(url, username, password);

        //3.编写SQL
        String sql = "insert into  users(id, name, password, email, birthday) values (?,?,?,?,?);";

        //4.预编译
        PreparedStatement preparedStatement = connection.prepareStatement(sql);

        preparedStatement.setInt(1,2);//给第一个占位符？ 的值赋值为1；
        preparedStatement.setString(2,"狂神说Java");//给第二个占位符？ 的值赋值为狂神说Java；
        preparedStatement.setString(3,"123456");//给第三个占位符？ 的值赋值为123456；
        preparedStatement.setString(4,"24736743@qq.com");//给第四个占位符？ 的值赋值为1；
        preparedStatement.setDate(5,new Date(new java.util.Date().getTime()));//给第五个占位符？ 的值赋值为new Date(new java.util.Date().getTime())；

        //5.执行SQL
        int i = preparedStatement.executeUpdate();

        if (i>0){
            System.out.println("插入成功@");
        }

        //6.关闭连接，释放资源（一定要做） 先开后关
        preparedStatement.close();
        connection.close();
    }
}

```



**事务**

要么都成功，要么都失败！

ACID原则：保证数据的安全。

```java
开启事务
事务提交  commit()
事务回滚  rollback()
关闭事务

转账：
A:1000
B:1000
    
A(900)   --100-->   B(1100) 
```



**Junit单元测试**

依赖

```xml
<!--单元测试-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
</dependency>
```

简单使用

@Test注解只有在方法上有效，只要加了这个注解的方法，就可以直接运行！

```java
@Test
public void test(){
    System.out.println("Hello");
}
```

![1568442261610](JavaWeb.assets/1568442261610.png)

失败的时候是红色：

![1568442289597](JavaWeb.assets/1568442289597.png)



**搭建一个环境**

```sql
CREATE TABLE account(
   id INT PRIMARY KEY AUTO_INCREMENT,
   `name` VARCHAR(40),
   money FLOAT
);

INSERT INTO account(`name`,money) VALUES('A',1000);
INSERT INTO account(`name`,money) VALUES('B',1000);
INSERT INTO account(`name`,money) VALUES('C',1000);
```

```java
    @Test
    public void test() {
        //配置信息
        //useUnicode=true&characterEncoding=utf-8 解决中文乱码
        String url="jdbc:mysql://localhost:3306/jdbc?useUnicode=true&characterEncoding=utf-8";
        String username = "root";
        String password = "123456";

        Connection connection = null;

        //1.加载驱动
        try {
            Class.forName("com.mysql.jdbc.Driver");
            //2.连接数据库,代表数据库
             connection = DriverManager.getConnection(url, username, password);

            //3.通知数据库开启事务,false 开启
            connection.setAutoCommit(false);

            String sql = "update account set money = money-100 where name = 'A'";
            connection.prepareStatement(sql).executeUpdate();

            //制造错误
            //int i = 1/0;

            String sql2 = "update account set money = money+100 where name = 'B'";
            connection.prepareStatement(sql2).executeUpdate();

            connection.commit();//以上两条SQL都执行成功了，就提交事务！
            System.out.println("success");
        } catch (Exception e) {
            try {
                //如果出现异常，就通知数据库回滚事务
                connection.rollback();
            } catch (SQLException e1) {
                e1.printStackTrace();
            }
            e.printStackTrace();
        }finally {
            try {
                connection.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
```

