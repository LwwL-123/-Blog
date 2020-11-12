# 1. 基本概念

## 1.1 前言

web开发：

- web，网页的意思

- 静态web

  - html  css
  - 提供给所有人看的数据始终不会发生变化

- 动态web

  - 几乎所有的网站
  - 提供给所有人看的，数据始终会发生变化，每个人在不同的时间，不同的地点看到的信息各不相同
  - 技术栈：Servlet/JSP、ASP、PHP

  在Java中，动态web资源开发的技术统称为JavaWeb



## 1.2 web应用程序

web应用程序，可以提供浏览器访问的程序

- a.html   b.html…….多个web资源，这些web资源可以被外界访问，对外界提供服务

- 你们能访问到的任何一个界面或者资源，都存在于这个世界上的某一个角落的计算机上

- URL：统一资源定位符

- 这个统一的web资源都会被放在一个文件夹下，web应用程序–>Tomcat服务器

- 一个web应用程序应由多部分组成（静态web，动态web）

  - html，css，js
  - jsp，servlet
  - java程序
  - jar包
  - 配置文件

  web应用程序编写完毕后，若想提供给外界访问，需要同意一个服务来管理

## 1.3 静态web

- *.html  *htm 这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取通信
- 静态web的缺点
  - web页面无法动态更新，所有用户看到的都是一个页面
  - 无法和数据库交互（数据无法持久化，用户无法交互）

## 1.4 动态web

页面会动态展示，web展示的效果`因人而异`

缺点：

- 加入服务器的动态web资源出现了错误，我们需要重新编写我们的后台程序，重新发布
  - 停机维护

优点：

- web页面可以动态更新，所有用户看到的不是同一个页面
- 可以与数据库交互（数据持久化：注册，商品信息，用户信息）



# 2. web服务器

## 2.1 技术讲解

`ASP`：

- 微软，国内最早流行的
- 在HTML中嵌入了vb的脚本     ASP+COM；
- 在ASP开发中，基本一个页面都有几千行的业务逻辑代码，业务及其混乱
- 维护成本高！
- C#

`PHP`：

- PHP开发速度很快，功能很强大，跨平台，代码很简单（70%）
- 但无法承载大访问量的情况下（局限性）

`JSP/Servlet`：

- B/S：浏览和服务器        C/S客户端和服务器
- 是一种B/S架构
- 基于Java语言的
- 可以承载三高问题（高并发，高可用，高性能.）带来的影响

## 2.2 web服务器

服务器是一种被动的操作，用来处理用户的一些请求，

### IIS：

微软的，基于ASP

# 3. Tomcat：

Tomcat简单的说就是一个运行JAVA的网络服务器，底层是Socket的一个程序，它也是JSP和Serlvet的一个容器。

如果你学过html，css，你会知道你写的页面只能自己访问，**别人不能远程访问你写的页面**，Tomcat就是**提供能够让别人访问自己写的页面的一个程序**

![img](https://gitee.com/lzw657434763/pictures/raw/master/Blog/640)





![642](https://gitee.com/lzw657434763/pictures/raw/master/Blog/642.png)



下载Tomcat：

		1. 安装 解压
  		2. 了解配置文件及目录结构
        		3. 这个东西的作用

![640](https://gitee.com/lzw657434763/pictures/raw/master/Blog/640.webp)

# 4. HTTP

## 4.1 什么是HTTP

HTTP（超文本传输）是一个简单的请求-响应协议，它通常运行在TCP上。

- 文本：html，字符串……
- 超文本：图片，音乐，地图，定位，视频
- 80

Https：安全的

- 443



## 4.2 两个时代

- http 1.0
  - HTTP/1.0：客户端可以与web服务器连接后，只能获得一个web资源
- http 2.0
  - HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源

## 4.3 Http 请求

- 客户端—发请求（Request）—服务器

```
Request URL: https://www.baidu.com/          请求地址
Request Method: GET						   get方法/post方法
Status Code: 200 OK						   状态码：200	
Remote Address: 103.235.46.39:443
```

```
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cache-Control: max-age=0
Connection: keep-alive
```

### 4.3.1 请求行

- 请求行中的请求方式：Get
- 请求方式：Get，Post，HEAD，DELETE，PUT，TRACT

- `GET`： 请求能够携带的参数比较小，大小有限制，会在浏览器的URL地址栏中显示数据内容，不安全，但高效。
- `POST`：请求能够携带的参数没有限制，大小没有限制，不会在浏览器的URL 地址栏显示数据内容，安全，但不高效。
- `PUT`： 传输文件，报文主体中包含文件内容，保存到对应URI位置。
- `HEAD`： 获得报文首部，与GET方法类似，只是不返回报文主体，一般用于验证URI是否有效。
- `DELETE`：删除文件，与PUT方法相反，删除对应URI位置的文件。
- `OPTIONS`：查询相应URI支持的HTTP方法

### 4.3.2 消息头

```
Accept  		    告诉浏览器，它所支持的数据类型
Accept-Encoding:	 支持那种编码格式 utf-8，GBK，…………
Accept-Language: 	告诉浏览器，他的语言环境	
Cache-Control: 		缓存控制
Connection: 		告诉浏览器，断开还是保持连接
```



## 4.4 Http响应

- 服务器—响应—客户端

```
Cache-Control: private					缓存控制
Connection: keep-alive					连接
Content-Encoding: gzip					编码
Content-Type: text/html;charset=utf-8	 类型	
```



### 4.4.1 响应体

```
Accept  		    告诉浏览器，它所支持的数据类型
Accept-Encoding:	 支持那种编码格式 utf-8，GBK，…………
Accept-Language: 	告诉浏览器，他的语言环境	
Cache-Control: 		缓存控制
Connection: 		告诉浏览器，断开还是保持连接
Reflush				告诉客户端，多久刷新
Location:			让网页重新定位
```

### 4.4.2 响应状态码

#### 2XX

一般是`请求成功`

200 正常处理

204 成功处理，但服务器没有新数据返回，显示页面不更新

206 对服务器进行范围请求，只返回一部分数据

#### 3XX

一般表示`重定向`

301 请求的资源已分配了新的URI中，URL地址改变了。【永久重定向】

302 请求的资源临时分配了新的URI中，URL地址没变【临时重定向】

303 与302相同的功能，但明确客户端应该采用GET方式来获取资源

304 发送了附带请求，但不符合条件【返回未过期的缓存数据】

307 与302相同，但不会把POST请求变成GET

#### 4XX

表示`客户端出错了`。

400 请求报文语法错误了

401 需要认证身份

403 没有权限访问

404 服务器没有这个资源

#### 5XX

`服务器出错了`

500 内部资源出错了

503 服务器正忙



# 5. Maven

1. 在JavaWeb中，我们需要大量的jar包，需要我们手动去导入
2. 如何能够让一个东西自动帮我导入和配置这个jar包

由此，Maven就诞生了



## 5.1 Maven项目架构管理工具

我们目前用它来，方便导入jar包

Maven的核心思想：**约定大于配置！！**

- 有约束，不要去违反
- Maven会规定如何去编写我们的java代码，必须按照这个规范来

![image-20201109145750477](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201109145750477.png)





> pom.xml

是maven的核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--maven版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
<!--刚才配置的-->
  <groupId>org.example</groupId>
  <artifactId>javaweb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
<!--Package：项目打包方式
jar：java应用
war：javaweb应用
-->  
  <packaging>war</packaging>
  
<!--配置-->
  <properties>
    <!--项目默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--编译版本-->
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

<!--项目依赖-->  
  <dependencies>
    <!--具体依赖-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
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



## 5.2 问题

maven由于他的约定大于配置，我们之后可能遇到我们写的配置文件，无法被导出或者生效的问题，解决方案

```xml
    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <excludes>
                    <exclude>**/*.properties</exclude>
                    <exclude>**/*.xml</exclude>
                </excludes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```



# 6. Servlet

## 6.1 Servlet简介

- Servlet就是sun公司开发动态web的一门技术
- Sun在这些API中提供一个接口叫Servlet，如果想开发一个Servlet程序，只需要完成两个小步骤
  - 编写一个类，实现Servlet接口
  - 把开发好的java类部署到web服务器中

把实现Servlet接口的java程序叫做，Servlet



## 6.2 HelloServlet

Sun公司有两个默认的实现类

1. 构建一个普通的maven项目，删掉src里面所有东西，以后我们的学习就在这个moudel里建立Moudel；

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
     <groupId>org.example</groupId>
     <version>1.0-SNAPSHOT</version>
   </parent>
   ```

3. Maven环境优化

   1. 修改web.xml为最新的
   2. 将maven的结构搭建完整

4. 编写一个servlet程序

   1. 编写一个普通类
   2. 实现Servlet接口，这里我们直接继承HttpServlet























