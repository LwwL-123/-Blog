# 1. Filter 过滤器

用来过滤网站的数据

- 处理中文乱码
- 登录验证

![image-20201125132719735](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201125132719735.png)



我们很容易发现，**过滤器可以比喻成一张滤网**。我们想想现实中的滤网可以做什么：**在泡茶的时候，过滤掉茶叶**。那滤网是怎么过滤茶叶的呢？**规定大小的网孔**，只要网孔比茶叶小，就可以实现过滤了！



Filter开发步骤：

1. 导包
2. 编写过滤器

实现Filter接口，重写对应的方法

```java
public class CharacterEncodingFilter implements javax.servlet.Filter {
    //初始化
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("CharacterEncodingFilter初始化了");
    }
        /*
        1. 过滤中的所有代码，在过滤特定请求的时候都会执行
        2. 必须要让过滤器继续同行
        chain.doFilter(request,response);
        */
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        servletRequest.setCharacterEncoding("utf-8");
        servletResponse.setCharacterEncoding("utf-8");
        servletResponse.setContentType("text/hrml;charset=utf-8");

        System.out.println("CharacterEncodingFilter执行前。。。");
        //让我们的请求继续走，如果不写，程序到这里就停止了
        filterChain.doFilter(servletRequest,servletResponse);
        System.out.println("CharacterEncodingFilter执行后。。。");
    }
    //销毁 web服务器关闭的时候，过滤会销毁
    public void destroy() {
        System.out.println("CharacterEncodingFilter销毁了");
    }
}
```

3.  在web.xml中配置 Filter

```xml
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>com.Lee.filter.CharacterEncodingFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <!--过滤servlet下的所有请求-->
    <url-pattern>/servlet/*</url-pattern>
</filter-mapping>
```

# 2. 监听器

监听器就是一个**实现特定接口的普通Java程序**，这个程序专门用于**监听一个Java对象的方法调用或属性改变**，当被监听对象发生上述事件后，监听器某个方法将立即被执行。

实现一个监听器的接口；（有N种）
1. 编写一个监听器
   实现监听器的接口…

```java

public class OnlineCountListener implements HttpSessionListener {
    //创建session监听:看你的一举一动
    //一旦创建一个session，就会触发一个事件
    public void sessionCreated(HttpSessionEvent se) {
        ServletContext ctx =se.getSession().getServletContext();
        Integer onlieCount = (Integer) ctx.getAttribute("onlieCount");

        if(onlieCount==null){
            onlieCount = new Integer(1);
        }else{
            int count = onlieCount.intValue();
            onlieCount = new Integer(count+1);
        }

        ctx.setAttribute("onlieCount",onlieCount);
    }
    //销毁session监听
    //一旦session销毁，就会触发一个事件
    public void sessionDestroyed(HttpSessionEvent se) {
        ServletContext ctx =se.getSession().getServletContext();
        Integer onlieCount = (Integer) ctx.getAttribute("onlieCount");

        if(onlieCount==null){
            onlieCount = new Integer(1);
        }else{
            int count = onlieCount.intValue();
            onlieCount = new Integer(count-1);
        }

        ctx.setAttribute("onlieCount",onlieCount);
    }
}
```

2. web.xml中注册监听器

```xml
<!--注册监听器-->
<listener>
    <listener-class>com.Lee.listener.OnlineCountListener</listener-class>
</listener>
```



# 3. 过滤器，监听器常见应用

监听器：GUI界面经常使用

```java
public class TestPanel {
    public static void main(String[] args) {
        Frame frame = new Frame("你好");//新建一个窗体
        Panel panel = new Panel(null);//面板
        frame.setLayout(null);//设置窗体的布局
        frame.setBounds(300,300,500,500);
        frame.setBackground(new Color(0,0,255));
        panel.setBounds(50,50,300,300);
        panel.setBackground(new Color(0x00FF00));
        frame.add(panel);
        frame.setVisible(true);

        //监听事件，监听关闭事件
        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                System.out.println("关闭了");
                System.exit(0);
            }
        });


    }
}
```



# 4.面试题

## 监听器有哪些作用和用法？

Java Web开发中的监听器（listener）就是application、session、request三个对象创建、销毁或者往其中添加修改删除属性时自动执行代码的功能组件，如下所示：

- ①ServletContextListener：对Servlet上下文的创建和销毁进行监听。

- ②ServletContextAttributeListener：监听Servlet上下文属性的添加、删除和替换。

- ③HttpSessionListener：对Session的创建和销毁进行监听。

- session超时（可以在web.xml中通过

- <session- config>/<session-timeout>标签配置超时时间）；

- - 通过调用session对象的invalidate()方 法使session失效。
  - 补 充：session的销毁有两种情况：

- ④HttpSessionAttributeListener：对Session对象中属性的添加、删除和替换进行监听。

- ⑤ServletRequestListener：对请求对象的初始化和销毁进行监听。

- ⑥ServletRequestAttributeListener：对请求对象属性的添加、删除和替换进行监听。

常见的监听器用途主要包括：**网站在线人数技术、监听用户的行为(管理员踢人)**。



## 过滤器有哪些作用和用法？

Java Web开发中的过滤器（filter）是从Servlet 2.3规范开始增加的功能，并在Servlet 2.4规范中得到增强。对Web应用来说，**过滤器是一个驻留在服务器端的Web组件**，它可以截取客户端和服务器之间的请求与响应信息，并对这些信息进行过 滤。当Web容器接受到一个对资源的请求时，它将判断是否有过滤器与这个资源相关联。如果有，那么容器将把请求交给过滤器进行处理。在过滤器中，**你可以改 变请求的内容，或者重新设置请求的报头信息，然后再将请求发送给目标资源。当目标资源对请求作出响应时候，容器同样会将响应先转发给过滤器，再过滤器中， 你可以对响应的内容进行转换，然后再将响应发送到客户端。**

常见的过滤器用途主要包括：**对用户请求进行统一认证、对用户的访问请求进行记录和审核、对用户发送的数据进行过滤或替换、转换图象格式、对响应内容进行压缩以减少传输量、对请求或响应进行加解密处理、触发资源访问事件、对XML的输出应用XSLT等**。

和过滤器相关的接口主要有：Filter、FilterConfig、FilterChain











































