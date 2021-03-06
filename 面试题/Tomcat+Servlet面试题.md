# Tomcat常见面试题

## 1.  Tomcat的缺省端口是多少，怎么修改

**到tomcat主目录下的conf/server.xml文件中修改**,把8080端口改成是8088或者是其他的

## 2. Tomcat 有哪几种Connector 运行模式(优化)？

1. bio(blocking I/O)
2. nio(non-blocking I/O)
3. apr(Apache Portable Runtime/Apache可移植运行库)

相关解释:

- bio: **传统的Java I/O操作，同步且阻塞IO。**
- nio: **JDK1.4开始支持，同步阻塞或同步非阻塞IO**
- aio(nio.2): **JDK7开始支持，异步非阻塞IO**
- apr: Tomcat将以JNI的形式调用Apache HTTP服务器的核心动态链接库来处理文件读取或网络传输操作，从而大大地**提高Tomcat对静态文件的处理性能**

### 2.1 名词概念

在高性能的IO体系设计中，有几个名词概念常常会使我们感到迷惑不解。具体如下： 

1. 什么是`同步`？ 

2. 什么是`异步`？ 

3. 什么是`阻塞`？ 

4. 什么是`非阻塞`？ 

5. 什么是`同步阻塞`？ 

6. 什么是`同步非阻塞`？ 

7. 什么是`异步阻塞`？ 

8. 什么是`异步非阻塞`？



先来举个实例生活中的例子：



如果你想吃一份宫保鸡丁盖饭：

同步阻塞：你到饭馆点餐，然后在那等着，还要一边喊：好了没啊！

同步非阻塞：在饭馆点完餐，就去遛狗了。不过溜一会儿，就回饭馆喊一声：好了没啊！

异步阻塞：遛狗的时候，接到饭馆电话，说饭做好了，让您亲自去拿。

异步非阻塞：饭馆打电话说，我们知道您的位置，一会给你送过来，安心遛狗就可以了。



在弄清楚上面的几个问题之前，我们首先得明白什么是同步，异步，阻塞，非阻塞，只有这几个单个概念理解清楚了，然后在组合理解起来，就相对比较容易了。 

1,同步和异步是针对应用程序和内核的交互而言的。 

2,阻塞和非阻塞是针对于进程在访问数据的时候，根据IO操作的就绪状态来采取的不同方式，说白了是一种读取或者写入操作函数的实现方式，阻塞方式下读取或者写入函数将一直等待，而非阻塞方式下，读取或者写入函数会立即返回一个状态值。 

由上描述基本可以总结一句简短的话，同步和异步是目的，阻塞和非阻塞是实现方式。 


1.同步：指的是用户进程触发IO操作并等待或者轮询的去查看IO操作是否就绪。自己上街买衣服，自己亲自干这件事，别的事干不了。 
2.异步：异步是指用户进程触发IO操作以后便开始做自己的事情，而当IO操作已经完成的时候会得到IO完成的通知（异步的特点就是通知） 告诉朋友自己合适衣服的尺寸，大小，颜色，让朋友委托去卖，然后自己可以去干别的事。（使用异步IO时，Java将IO读写委托给OS处理，需要将数据缓冲区地址和大小传给OS） 
3.阻塞：所谓阻塞方式的意思是指, 当试图对该文件描述符进行读写时, 如果当时没有东西可读,或者暂时不可写, 程序就进入等待 状态, 直到有东西可读或者可写为止 去公交站充值，发现这个时候，充值员不在（可能上厕所去了），然后我们就在这里等待，一直等到充值员回来为止。（当然现实社会，可不是这样，但是在计算机里确实如此。） 
4.非阻塞：非阻塞状态下, 如果没有东西可读, 或者不可写, 读写函数马上返回, 而不会等待， 银行里取款办业务时，领取一张小票，领取完后我们自己可以玩玩手机，或者与别人聊聊天，当轮我们时，银行的喇叭会通知，这时候我们就可以去了。



一个IO操作其实分成了两个步骤：发起IO请求和实际的IO操作。 

同步IO和异步IO的区别就在于第二个步骤是否阻塞，如果实际的IO读写阻塞请求进程，那么就是同步IO。 
阻塞IO和非阻塞IO的区别在于第一步，发起IO请求是否会被阻塞，如果阻塞直到完成那么就是传统的阻塞IO，如果不阻塞，那么就是非阻塞IO。 

同步和异步是针对应用程序和内核的交互而言的，同步指的是用户进程触发IO操作并等待或者轮询的去查看IO操作是否就绪，而异步是指用户进程触发IO操作以后便开始做自己的事情，而当IO操作已经完成的时候会得到IO完成的通知。而阻塞和非阻塞是针对于进程在访问数据的时候，根据IO操作的就绪状态来采取的不同方式，说白了是一种读取或者写入操作函数的实现方式，阻塞方式下读取或者写入函数将一直等待，而非阻塞方式下，读取或者写入函数会立即返回一个状态值。 
所以,IO操作可以分为3类：同步阻塞（即早期的BIO操作）、同步非阻塞（NIO）、异步非阻塞（AIO）。 


同步阻塞(BIO)： 
在此种方式下，用户进程在发起一个IO操作以后，必须等待IO操作的完成，只有当真正完成了IO操作以后，用户进程才能运行。JAVA传统的IO模型属于此种方式。 
同步非阻塞(NIO)：
在此种方式下，用户进程发起一个IO操作以后便可返回做其它事情，但是用户进程需要时不时的询问IO操作是否就绪，这就要求用户进程不停的去询问，从而引入不必要的CPU资源浪费。其中目前JAVA的NIO就属于同步非阻塞IO。 
异步非阻塞(AIO)：

此种方式下是指应用发起一个IO操作以后，不等待内核IO操作的完成，等内核完成IO操作以后会通知应用程序。



同步阻塞IO（JAVA BIO）： 
  同步并阻塞，服务器实现模式为一个连接一个线程，即客户端有连接请求时服务器端就需要启动一个线程进行处理，如果这个连接不做任何事情会造成不必要的线程开销，当然可以通过线程池机制改善。 

同步非阻塞IO(Java NIO)：同步非阻塞，服务器实现模式为一个请求一个线程，即客户端发送的连接请求都会注册到多路复用器上，多路复用器轮询到连接有I/O请求时才启动一个线程进行处理。用户进程也需要时不时的询问IO操作是否就绪，这就要求用户进程不停的去询问。 

异步阻塞IO（Java NIO）： 
  此种方式下是指应用发起一个IO操作以后，不等待内核IO操作的完成，等内核完成IO操作以后会通知应用程序，这其实就是同步和异步最关键的区别，同步必须等待或者主动的去询问IO是否完成，那么为什么说是阻塞的呢？因为此时是通过select系统调用来完成的，而select函数本身的实现方式是阻塞的，而采用select函数有个好处就是它可以同时监听多个文件句柄（如果从UNP的角度看，select属于同步操作。因为select之后，进程还需要读写数据），从而提高系统的并发性！ 

（Java AIO(NIO.2)）异步非阻塞IO: 
  在此种模式下，用户进程只需要发起一个IO操作然后立即返回，等IO操作真正的完成以后，应用程序会得到IO操作完成的通知，此时用户进程只需要对数据进行处理就好了，不需要进行实际的IO读写操作，因为真正的IO读取或者写入操作已经由内核完成了。  



BIO、NIO、AIO适用场景分析: 
  BIO方式适用于连接数目比较小且固定的架构，这种方式对服务器资源要求比较高，并发局限于应用中，JDK1.4以前的唯一选择，但程序直观简单易理解。 
  NIO方式适用于连接数目多且连接比较短（轻操作）的架构，比如聊天服务器，并发局限于应用中，编程比较复杂，JDK1.4开始支持。 
  AIO方式使用于连接数目多且连接比较长（重操作）的架构，比如相册服务器，充分调用OS参与并发操作，编程比较复杂，JDK7开始支持。 





# Servlet面试题

## Servlet生命周期

Servlet生命周期可分为5个步骤

1. **加载Servlet**。当Tomcat第一次访问Servlet的时候，**Tomcat会负责创建Servlet的实例**
2. **初始化**。当Servlet被实例化后，Tomcat会**调用init()方法初始化这个对象**
3. **处理服务**。当浏览器**访问Servlet**的时候，Servlet **会调用service()方法处理请求**
4. **销毁**。当Tomcat关闭时或者检测到Servlet要从Tomcat删除的时候会自动调用destroy()方法，**让该实例释放掉所占的资源**。一个Servlet如果长时间不被使用的话，也会被Tomcat自动销毁
5. **卸载**。当Servlet调用完destroy()方法后，等待垃圾回收。如果**有需要再次使用这个Servlet，会重新调用init()方法进行初始化操作**

简单总结：**只要访问Servlet，service()就会被调用。init()只有第一次访问Servlet的时候才会被调用。destroy()只有在Tomcat关闭的时候才会被调用。**



## get方式和post方式有何区别

`数据携带`上:

- GET方式：在URL地址后附带的参数是有限制的，其数据容量通常不能超过1K。
- POST方式：可以在请求的实体内容中向服务器发送数据，传送的数据量无限制。

`请求参数的位置`上:

- GET方式：请求参数放在URL地址后面，以?的方式来进行拼接
- POST方式:请求参数放在HTTP请求包中

用途上:

- GET方式一般用来获取数据

- POST方式一般用来提交数据

- - 首先是因为GET方式携带的数据量比较小，无法带过去很大的数量
  - POST方式提交的参数后台更加容易解析(使用POST方式提交的中文数据，后台也更加容易解决)
  - GET方式比POST方式要快 , 详情可看:https://www.cnblogs.com/strayling/p/3580048.html

## Servlet相关 API

> doGet与doPost方法的两个参数是什么

1. HttpServletRequest：封装了与请求相关的信息
2. HttpServletResponse：封装了与响应相关的信息

> 获取页面的元素的值有几种方式，分别说一下

1. request.getParameter() 返回客户端的请求参数的值
2. request.getParameterNames() 返回所有可用属性名的枚举
3. request.getParameterValues() 返回包含参数的所有值的数组

> request.getAttribute()和request.getParameter()区别

用途上:

- request.getAttribute()， **一般用于获取request域对象的数据**(在跳转之前把数据使用setAttribute来放到request对象上)
- request.getParameter()， **一般用于获取客户端提交的参数**

存储数据上:

- request.getAttribute()可以获取Objcet对象
- request.getParameter()只能获取字符串(这也是为什么它一般用于获取客户端提交的参数)



## forward和redirect的区别

1. **实际发生位置不同，地址栏不同**

- - `转发`是发生在服务器的
  - **`转发`是由服务器进行跳转的**，细心的朋友会发现，在转发的时候，**浏览器的地址栏是没有发生变化的**，在我访问Servlet111的时候，即使跳转到了Servlet222的页面，浏览器的地址还是Servlet111的。也就是说**浏览器是不知道该跳转的动作，转发是对浏览器透明的**。通过上面的转发时序图我们也可以发现，**实现转发只是一次的http请求**，**一次转发中request和response对象都是同一个**。这也解释了，为什么可以使用**request作为域对象进行Servlet之间的通讯**
  - `重定向`是发生在浏览器的 - **重定向是由浏览器进行跳转的**，进行重定向跳转的时候，**浏览器的地址会发生变化的**。曾经介绍过：实现重定向的原理是由response的状态码和Location头组合而实现的。**这是由浏览器进行的页面跳转**实现重定向**会发出两个http请求**，**request域对象是无效的，因为它不是同一个request对象**

2. **能够去往的URL的范围不一样:**

- - **转发是服务器跳转只能去往当前web应用的资源**
  - **重定向是服务器跳转，可以去往任何的资源**

3. **传递数据的类型不同**

- - **转发的request对象可以传递各种类型的数据，包括对象**
  - **重定向只能传递字符串**

4. **跳转的时间不同**

5. - **转发时：执行到跳转语句时就会立刻跳转**
   - **重定向：整个页面执行完之后才执行跳转**

那么转发(forward)和重定向(redirect)使用哪一个？

- 根据上面说明了转发和重定向的区别也可以很容易概括出来**。转发是带着转发前的请求的参数的。重定向是新的请求**。

  

典型的应用场景：

1. 转发: 访问 Servlet 处理业务逻辑，然后 forward 到 jsp 显示处理结果，浏览器里 URL 不变
2. 重定向: 提交表单，处理成功后 redirect 到另一个 jsp，防止表单重复提交，浏览器里 URL 变了

## tomcat容器是如何创建servlet类实例？用到了什么原理？

1. 当容器启动时，会读取在webapps目录下所有的web应用中的web.xml文件，然后对 **xml文件进行解析，并读取servlet注册信息**。然后，将每个应用中注册的servlet类都进行加载，并通过 **反射的方式实例化**。（有时候也是在第一次请求时实例化）
2. 在servlet注册时加上1如果为正数，则在一开始就实例化，如果不写或为负数，则第一次请求实例化。

## 什么是cookie？Session和cookie有什么区别？

> 什么是cookie？

Cookie是由W3C组织提出，最早由netscape社区发展的一种机制

- 网页之间的**交互是通过HTTP协议传输数据的，**而Http协议是**无状态的协议**。无状态的协议是什么意思呢？**一旦数据提交完后，浏览器和服务器的连接就会关闭，再次交互的时候需要重新建立新的连接**。
- 服务器无法确认用户的信息，于是乎，W3C就提出了：**给每一个用户都发一个通行证，无论谁访问的时候都需要携带通行证，这样服务器就可以从通行证上确认用户的信息**。通行证就是Cookie

> Session和cookie有什么区别？

- **从存储方式上比较**

- - Cookie只能存储字符串，如果要存储非ASCII字符串还要对其编码。
  - Session可以存储任何类型的数据，可以把Session看成是一个容器

- **从隐私安全上比较**

- - **Cookie存储在浏览器中，对客户端是可见的**。信息容易泄露出去。如果使用Cookie，最好将Cookie加密
  - **Session存储在服务器上，对客户端是不透明的**。不存在敏感信息泄露问题

- **从有效期上比较**
  - 如果浏览器禁用了Cookie，那么Cookie是无用的了！
  - 如果浏览器禁用了Cookie，Session可以通过URL地址重写来进行会话跟踪

- **从跨域名上比较**

- - Cookie可以设置domain属性来实现跨域名
  - Session只在当前的域名内有效，不可夸域名

## Servlet安全性问题

由于Servlet是单例的，当多个用户访问Servlet的时候，**服务器会为每个用户创建一个线程**。**当多个用户并发访问Servlet共享资源的时候就会出现线程安全问题**。

原则：

1. 如果一个**变量需要多个用户共享**，则应当在访问该变量的时候，**加同步机制synchronized (对象){}**
2. 如果一个变量**不需要共享**，则**直接在 doGet() 或者 doPost()定义**.这样不会存在线程安全问题

