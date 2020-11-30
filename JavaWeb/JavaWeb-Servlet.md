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
- Servlet其实就是一个**遵循Servlet开发的java类**。Serlvet是**由服务器调用的**，**运行在服务器端**。
- Sun在这些API中提供一个接口叫Servlet，如果想开发一个Servlet程序，只需要完成两个小步骤
  - 编写一个类，实现Servlet接口
  - 把开发好的java类部署到web服务器中

把实现Servlet接口的java程序叫做，Servlet



Servlet带给我们最大的作用就是能够**处理浏览器带来HTTP请求，并返回一个响应给浏览器，从而实现浏览器和服务器的交互**。

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

```java
public class HelloServlet extends HttpServlet {

    //由于get和post只是请求实现的不同方式，可以互相调用，业务逻辑都一样
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        PrintWriter writer = resp.getWriter();//响应流
        writer.print("Hello,Servlet");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

5. 编写Servlet的映射

   为什么需要映射：我们写的是java程序，但是要通过浏览器访问，而浏览器需要连接web服务器，所以我们需要在web服务中注册我们的Servlet，还需给他一个浏览器能够访问的路径

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                         http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0"
         metadata-complete="true">
    <!--注册servlet-->
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.Lee.servlet.HelloServlet</servlet-class>
    </servlet>
    <!--servlet请求陆青-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>hello</url-pattern>
    </servlet-mapping>
</web-app>
```

6. 配置Tomcat
7. 启动测试

## 6.3 Serlet原理

Servlet是由web服务器（Tomcat）调用，web服务器在收到浏览器请求之后，会：

![image-20201116132429389](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201116132429389.png)

## 6.4 Mapping问题

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

4. 指定后缀或者前缀

```xml
<!--可以自定义后缀实现请求映射
注意点，*前面不能加项目映射的路径
hello/sajdlkajda.qinjiang
-->
<servlet-mapping>
<servlet-name>hello</servlet-name>
<url-pattern>*.lizhiwei</url-pattern>
</servlet-mapping>
```

5. 优先级问题 指定了固有的映射路径优先级最高，如果找不到就会走默认的处理请求；

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



## 6.5 ServletContext

web容器在启动的时候，会为每个web程序都创建一个对应的ServletContext对象，他代表了当前的web应用

### 6.5.1 共享数据

我在这个Servlet中保存的数据，可以在另外一个Servlet中拿到

创建的类：

```java
public class HelloServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        
        ServletContext context = this.getServletContext();
        String username="lzw";//数据
        context.setAttribute("username",username);//将一个数据保存在了ServletContext中，名字：username，值username
    }
}
```

读取的类：

```java
public class GetServlet extends HelloServlet{
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        String username = (String) context.getAttribute("username");

        resp.setContentType("text/html");
        resp.setCharacterEncoding("utf-8");
        resp.getWriter().print("名字"+username);
    }
}
```

xml：

```xml
<servlet>
    <servlet-name>hello</servlet-name>
    <servlet-class>com.Lee.Servlet.HelloServlet</servlet-class>
</servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>

    <servlet>
        <servlet-name>getc</servlet-name>
        <servlet-class>com.Lee.Servlet.GetServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>getc</servlet-name>
        <url-pattern>/getc</url-pattern>
    </servlet-mapping>
```



### 6.5.2 获取初始化参数

首先在web.xml中配置	

```xml
    <!--配置一些初始化的参数-->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:mysql://localhost:3306/mybatis</param-value>
    </context-param>
```

获取：

```java
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        String url = context.getInitParameter("url");
        resp.getWriter().print(url);
    }
```



### 6.5.3 请求转发

```java
public class ServletDemo02 extends HelloServlet{
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        System.out.println("进入了demo02");
        //转发的请求路径
        RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp");
        //调用forward实现请求转发
        requestDispatcher.forward(req,resp);
    }
}
```

- `请求转发`：

![image-20201117105158213](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201117105158213.png)



- `重定向`:

![image-20201117105223305](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201117105223305.png)

### 6.5.4 读取资源文件

Properties

- 在java目录下新建properties
- 在resource目录下新建properties

发现：都被打包到了同一个路径下，classes，我们俗称这个路径为classpath

思路：需要一个文件流：

```properties
username=lzw
password=123456
```

```java
public class ServletDemo03 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        InputStream is = context.getResourceAsStream("/WEB-INF/classes/db.properties");
        //创建properties
        Properties prop = new Properties();
        prop.load(is);
        String username = prop.getProperty("username");
        String password = prop.getProperty("password");
        resp.getWriter().print(username+"  "+password);

    }
}
```



## 6.6 HttpServletResponse

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求，分别创建一个代表请求的HttpServletRequest对象，代表相应的一个HttpServletResponse对象；

- 如果我们需要获取客户端请求过来的参数，找HttpServletRequest
- 如果要给客户端响应一些信息，找HttpServletResponse

### 6.6.1 简单分类

> 负责向浏览器发送数据的方法

```java
public ServletOutputStream getOutputStream() throws IOException;

public PrintWriter getWriter() throws IOException;
```



> 负责向浏览器发送响应头的方法

```java
public void setCharacterEncoding(String charset);
public void setContentLength(int len);
public void setContentLengthLong(long len);
public void setContentType(String type);
public void setHeader(String name, String value);
public void setDateHeader(String name, long date);
```

### 6.6.2 下载文件

1. 要获取下载文件的路径
2. 下载的文件名是什么
3. 设置想办法让浏览器支持我们需要下载的东西
4. 获取下载文件的输入流
5. 创建缓冲区
6. 获取OutputStream对象
7. 将FileOutputStream流写入到buffer缓冲区
8. 使用OutputStream将缓冲区中的数据输出到客户端

```java
public class FileServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        1. 要获取下载文件的路径
        String realPath = "C:\\Users\\Administrator\\IdeaProjects\\javaweb-02-servlet\\response\\target\\classes\\2.jpg";
        System.out.println("下载文件的路径：" + realPath);
//        2. 下载的文件名是什么
        String fileName = realPath.substring(realPath.indexOf("\\") + 1);
//        3. 设置想办法让浏览器支持我们需要下载的东西
        resp.setHeader("Content-Disposition", "attachment;filename" + fileName);
//        4. 获取下载文件的输入流
        FileInputStream in = new FileInputStream(realPath);
//        5. 创建缓冲区
        int len = 0;
        byte[] buffer = new byte[1024];
//        6. 获取OutputStream对象
        ServletOutputStream out = resp.getOutputStream();
//        7. 将FileOutputStream流写入到buffer缓冲区,使用OutputStream将缓冲区中的数据输出到客户端
        while ((len=in.read(buffer))!=-1){
            out.write(buffer,0,len);
        }
        out.close();
        in.close();
    }
}
```



### 6.6.3 验证码功能

验证码怎么来

- 前端实现
- 后端实现，需要用Java的图片类，生成一个图片

### 6.6.4 实现重定向（重要）

![image-20201117105223305](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201117105223305.png)



一个web资源（B）收到客户端请求后，他会通知客户端（A）去访问另一个web资源（C），这个过程叫重定向

常见场景：

- 用户登录

```java
public void sendRedirect(String location) throws IOException;
```

测试：

```java
public class RedirectServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        /**
         * resp.setHeader("location","/response_war/image");
         * resp.setStatus(302);
         */
        resp.sendRedirect("/response_war/image");//重定向
    }
}
```



面试题：重定向和转发的区别

相同点：

- 页面都会跳转

不同点：

- 请求转发的时候，url不会发生变化
- 重定向的时候，url地址栏会发生变化

```java
public class RequestTest extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //处理请求
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        System.out.println("用户名是："+username);
        System.out.println("密码是"+password);
        //重定向一定要注意路径问题
        resp.sendRedirect("/response_war/success.jsp");
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

```html

<%--这里提交的路径，需要寻找到项目的路径--%>
<%--${pageContext.request.contextPath}代表当前项目--%>
<%@page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8" %>
<form action="${pageContext.request.contextPath}/login" method="get">
    用户名：<input type="text" name="username"><br>
    密码：<input type="password" name="password"><br>
    <input type="submit">
</form>
```



## 6.7 HttpServletRequest

HttpServletRequest代表客户端的请求，用户通过Http协议访问服务器，HTTP请求中的所有信息会被封装到HttpServletRequest，通过这个HttpServletRequest

```java
<!-- https://mvnrepository.com/artifact/com.github.kstyrc/embedded-redis -->
<dependency>
    <groupId>com.github.kstyrc</groupId>
    <artifactId>embedded-redis</artifactId>
    <version>0.6</version>
</dependency>
```

### 6.7.1 获取前端传递的参数，请求转发

![image-20201123105731838](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201123105731838.png)



```java
public class LoginServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        //获取参数
        String username = req.getParameter("username");
        String password = req.getParameter("password");
        String[] hobbys = req.getParameterValues("hobbys");

        System.out.println("========");
        System.out.println(username);
        System.out.println(password);
        System.out.println(Arrays.toString(hobbys));
        System.out.println("========");

        //通过请求转发
        req.getRequestDispatcher("/success.jsp").forward(req,resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

面试题：重定向和转发的区别

相同点：

- 页面都会跳转

不同点：

- 请求转发的时候，url不会发生变化  307
- 重定向的时候，url地址栏会发生变化   302



# 7. Cookie、Session

## 7.1 会话

`会话`：用户打开一个浏览器，点击了很多超链接，访问多个web资源，关闭浏览器，这个过程可以称之为会话

`有状态会话`：

一个网站，怎么证明你来过

	1. 服务端给客户端一个 信件，客户端下次访问服务端带上信件就可以了;Cookie
 	2. 服务器登记你来过了，下次你来的时候我匹配你；Session



## 7.2 保存会话的两种技术

`cookie`: 

- 客户端技术（响应，请求）

`session`:

- 服务器技术，利用这个技术，可以保存用户的会话信息，我们可以把信息或者数据放在 Session当中



## 7.3 Cookie

1. 从请求中拿到cookie信息
2. 服务器响应给客户端cookie

```java
Cookie[] cookies = req.getCookies();//获得cookie
cookie.getName();//获得cookie中的key
cookie.getValue();//获得cookie中的value
new Cooikie("","");//新建一个cookie
cookie.setMaxAge(24*60*60);//设置cookie的有效期
resp.addCooikie(cookie);//响应给客户端一个cookie
```

cookie一般会保存在本地的用户目录下appdata

- 一个cookie只能保存一个信息
- 一个web站点可以给浏览器发送多个cookie，最多存放20个cookie
- Cookie的大小有限制20kb
- 300个cookie浏览器上限



删除cookie：

- 不设置有效期，关闭浏览器，自动失效
- 设置有效期时间为0



## 7.4 Session

什么是Session：

- 服务器会给每一个用户（浏览器）创建一个seesion对象；
- 一个Session独占一个浏览器，只要浏览器没有关闭，这个Session就存在；
- 用户登录之后，整个网站它都可以访问—》保存用户的信息，保存购物车的信息



Session和Cookie的区别：

- cookie是把用户的数据写给用户的浏览器，浏览器保存（可以保存多个）
- Session把用户的数据写到用户独占的Session中，服务端保存 （保存重要的信息，减少服务器资源的浪费）
- Session对象由服务器创建



使用场景：

- 保存一个登录用户的信息
- 购物车信息
- 在整个网站中经常会使用的数据，我们将它保存到session中



```java
public class SessionDemo01 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8");

        //得到Session
        HttpSession session = req.getSession();
        //在Session中存东西
        session.setAttribute("person1",new person("lzw",8));
        //获取session的id
        String sessionId = session.getId();
        //判断session是不是新创建
        if(session.isNew()){
            resp.getWriter().write("session创建成功,id+"+sessionId);
        }else {
            resp.getWriter().write("session已经在服务器中存在，id"+sessionId);
        }

        //session创建的时候做了什么事情
        Cookie cookie = new Cookie("JESSIONID", sessionId);
        resp.addCookie(cookie);
    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



```java
public class SessionDemo02 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        //解决乱码问题
        req.setCharacterEncoding("utf-8");
        resp.setCharacterEncoding("utf-8");
        resp.setContentType("text/html;charset=utf-8");
        //得到Session
        HttpSession session = req.getSession();

        //获取资源
        person person1 = (person) session.getAttribute("person1");
        System.out.println(person1.toString());

    }
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```



![image-20201124141823865](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201124141823865.png)





