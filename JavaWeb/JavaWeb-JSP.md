# 1.  什么是JSP

Java Server Pages：Java服务器端页面，也和Servlet一样，用于动态web技术

最大的特点：

- 写JSP就像在写HTML
- 区别：
  - HTML只给用户提供静态的数据
  - JSP页面中可以嵌入JAVA代码 ，为用户提供动态数据



## 2. 原理

思路：jsp到底怎么执行的：

- 代码层面没有任何问题 

- 服务器内部工作 

  tomcat中有一个work目录； 

  IDEA中使用Tomcat的会在IDEA的tomcat中生产一个work目录



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
public void _jspService(.HttpServletRequest request,HttpServletResponse
response)
```

浏览器向服务器发送请求，不管访问什么资源，其实都是在访问servlet



编译过程是这样子的：**浏览器第一次请求1.jsp时，Tomcat会将1.jsp转化成1_jsp.java这么一个类，并将该文件编译成class文件。编译完毕后再运行class文件来响应浏览器的请求**。

以后访问1.jsp就不再重新编译jsp文件了，直接调用class文件来响应浏览器。当然了，**如果Tomcat检测到JSP页面改动了的话，会重新编译的**。

![image-20201201132539104](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201201132539104.png)

既然JSP是一个Servlet，**那JSP页面中的HTML排版标签是怎么样被发送到浏览器的**？我们来看下上面1_jsp.java的源码就知道了。原来就是用write()出去的罢了。**说到底，JSP就是封装了Servlet的java程序罢了。**

```java
out.write("\r\n");
out.write("\r\n");
out.write("<html>\r\n");
out.write("<head>\r\n");
out.write("    <title>简单使用JSP</title>\r\n");
out.write("</head>\r\n");
out.write("<body>\r\n");
```

有人可能也会问：**JSP页面的代码服务器是怎么执行的**？再看回1_jsp.java文件，**java代码就直接在类中的service()中。**

```java
String s = "HelloWorda";
out.println(s);
```

**JSP内置了9个对象！**内置对象有：`out`、`session`、`response`、`request`、`config`、`page`、`application`、`pageContext`、`exception`。

重要要记住的是：**JSP的本质其实就是Servlet**。只是JSP当初设计的目的是为了简化Servlet输出HTML代码。

## 什么时候用JSP

重复一句：**JSP的本质其实就是Servlet**。只是JSP当初设计的目的是为了简化Servlet输出HTML代码。

我们的Java代码还是写在Servlet上的，不会写在JSP上。在知乎曾经看到一个问题：“如何使用JSP连接JDBC”。显然，**我们可以这样做，但是没必要**。

JSP看起来就像是一个HTML，再往里边增加大量的Java代码，这是不正常，不容易阅读的。

所以，我们一般的模式是：**在Servlet处理好的数据，转发到JSP，JSP只管对小部分的数据处理以及JSP本身写好的页面。**

例如，下面的Servlet处理好表单的数据，放在request对象，转发到JSP

```java
//验证表单的数据是否合法，如果不合法就跳转回去注册的页面
if(formBean.validate()==false){
  //在跳转之前，把formbean对象传递给注册页面
  request.setAttribute("formbean", formBean);
  request.getRequestDispatcher("/WEB-INF/register.jsp").forward(request, response);
  return;
}
```

JSP拿到Servlet处理好的数据，做显示使用





# 2.JSP基本语法

> jsp表达式

```jsp
<%--
  JSP表达式
  作用：用来将程序的输出，输出到客户端
  <%= 变量或者表达式 %>
--%>
<%= new java.util.Date() %>
```



> jsp脚本片段

```jsp
<%--jsp脚本片段--%>
<%
  int sum = 0;
  for (int i = 0; i < 100; i++) {
    sum+=i;
  }
  out.println("<h1>Sum = "+sum+"</h1>");
%>
```



> 脚本片段的在实现

```jsp
  <%--在代码中嵌入html元素--%>
  <%
    for (int i = 0; i < 5; i++) {
  %>
    <h4>hello <%=i%> </h4>
  <%
    }
  %>
```

## JSP需要学什么

JSP我们要学的其实两块就够了：**JSTL和EL表达式**

### EL表达式

**表达式语言（Expression Language，EL）,EL表达式是用`${}`括起来的脚本，用来更方便的读取对象！**EL表达式主要用来读取数据，进行内容的显示！

**为什么要使用EL表达式？**我们先来看一下**没有EL表达式是怎么样读取对象数据的吧**！在1.jsp中设置了Session属性

```jsp
<%@ page language="java" contentType="text/html" pageEncoding="UTF-8"%>
<html>
<head>
    <title>向session设置一个属性</title>
</head>
<body>

<%
    //向session设置一个属性
    session.setAttribute("name", "aaa");
    System.out.println("向session设置了一个属性");
%>

</body>
</html>	
```

**在2.jsp中获取Session设置的属性**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title></title>
</head>
<body>

<%
        String value = (String) session.getAttribute("name");
        out.write(value);
%>
</body>
</html>
```

<img src="https://mmbiz.qpic.cn/sz_mmbiz_png/2BGWl1qPxib2liaHskXvs8jia8oGNc9p4Hzic6h3O3A21n8oCX8sDhnTGkiab6EZUo6RJBHEibbt2I8sMfvZncVELo9A/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1" alt="img"  />



上面看起来，也没有多复杂呀，那我们试试EL表达式的！

**在2.jsp中读取Session设置的属性**

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title></title>
</head>
<body>

${name}

</body>
</html>
```

**只用了简简单单的几个字母就能输出Session设置的属性了！并且输出在浏览器上！**

![img](https://mmbiz.qpic.cn/sz_mmbiz_png/2BGWl1qPxib2liaHskXvs8jia8oGNc9p4HzDAr66fYLrEmmWdclqlrp69jMsERf64dB94fZlWgEFQQiaGtZtK0NiaNw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

使用EL表达式**可以方便地读取对象中的属性、提交的参数、JavaBean、甚至集合**！

### JSTL

**`JSTL`全称为 JSP Standard Tag Library 即JSP标准标签库**。JSTL作为最基本的标签库，**提供了一系列的JSP标签，实现了基本的功能：集合的遍历、数据的输出、字符串的处理、数据的格式化等等！**



> **为什么要使用JSTL？**

**EL表达式不够完美，需要JSTL的支持**！在JSP中，我们前面已经用到了EL表达式，体会到了EL表达式的强大功能：**使用EL表达式可以很方便地引用一些JavaBean以及其属性，不会抛出NullPointerException之类的错误！**但是，EL表达式非常有限，**它不能遍历集合，做逻辑的控制。这时，就需要JSTL的支持了**！

**Scriptlet的可读性，维护性，重用性都十分差！**JSTL与HTML代码十分类似，遵循着XML标签语法，**使用JSTL让JSP页面显得整洁，可读性非常好，重用性非常高，可以完成复杂的功能！**

之前我们在使用EL表达式获取到集合的数据，遍历集合都是用scriptlet代码循环，现在我们学了forEach标签就可以舍弃scriptlet代码了。



**向Session中设置属性，属性的类型是List集合**

```jsp
    <%
        List list = new ArrayList<>();
        list.add("zhongfucheng");
        list.add("ouzicheng");
        list.add("xiaoming");

        session.setAttribute("list", list);
    %>
```

**遍历session属性中的List集合,items：即将要迭代的集合。var：当前迭代到的元素**

```jsp
    <c:forEach  var="list" items="${list}" >
        ${list}<br>
    </c:forEach>
```







































