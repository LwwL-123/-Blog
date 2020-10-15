# 1.spring

## 	1.1 简介



```xml
<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.0.RELEASE</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.0.jdbcE</version>
</dependency>
```

## 	1.2 优点

- Spring是一个开源的，免费的容器(框架)
- Spring是一个轻量级，非入侵式的框架
- 控制反转(IOC)，面向切面编程(AOP)
- 支持事物的处理，对框架整合的支持



==总结:Spring就是一个轻量级的控制反转(IOC)和面向切面编程(AOP)的框架!==



## 	1.3 组成

![image-20200928105443332](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200928105443332.png)



## 	1.4 扩展

- Spring Boot
  - 一个快速开发的脚手架
  - 基于Spring Boot可以快速的开发单个微服务
  - ==约定大于配置!!!!==
- Spring Cloud
  - Spring Cloud是基于Spring Boot实现的



现在大多数公司都在使用Spring Boot进行快速开发，学习Spring Boot的前提，需要完全掌握Spring和

Spring MVC

# 2. IOC 理论推导

1.UserDao 接口

2.UserDaoimpl 实现类

3.UserService 业务接口

4.UserServiceimpl 业务实现

在我们之前的业务中，用户的需求可能会影响我们原来的代码，我们需要根据用户的需求去修改源代码，如果程序代码量十分大，修改一次的成本代价十分昂贵.



我们使用一个Set接口实现

```java
    private UserDao userDao;
    //利用set进行动态实现值的注入
    public void setUserDao(UserDao userDao){
        this.userDao=userDao;
    }
```

- 之前，程序是主动创建对象!控制权在程序员手上
- 使用了set注入后，程序不再具有主动性，而是变成了被动的接受对象.

这种思想，从本质上解决了问题，我们程序员不用再去管理对象的创建了，

系统的耦合性大大降低，可以更加专注业务的实现上!这是IOC的原型



### IOC本质

控制反转IoC(Inversion of Control)，是一种设计思想，DI(依赖注入)是实现IoC的一种方法，也有人认为DI知识ioc的另一种说法。在没有ioc的程序中，我们使用面向对象编程，对象的创建与对象间的依赖关系完全硬编码在程序中，对象的创建由程序自己控制，控制反转后，将对象的创建转移给第三方，

**个人认为的所谓的控制反转就是：获得依赖对象的方式反转了**

**控制反转是一种通过描述（XML或注释）并通过第三方去生产或获取特定对象的方式。在Spring中实现控制反转的是ioc容器，其实现方法是依赖注入（Dependency Injection，DI）**

# 3.HelloSpring

hello对象是由Spring创建的

hello对象的属性是由Spring容器设置的



## 	控制反转

控制：谁来控制对象的创建，传统应用程序的对象是由程序本身控制创建的，在使用Spring以后，对象是由Spring来创建的

反转：程序本身不创建对象，而变成被动的接收对象

依赖注入：就是利用set方法来进行注入的

**IOC是一种编程思想，由主动编程变为被动的接收**

==**所以，我们彻底不用去程序中去改动了，只需要在xml配置文件中进行修改。所谓的ioc，就是：对象由Spring来创建，管理，装配-。**==



# 4.IOC创建对象的方式

1.使用无参数创建对象，默认。

2.假设我们要使用有参数构造创建对象

- 下标赋值	

```xml
    <bean id="user" class="com.kuang.pojo.User">
        <constructor-arg index="0" value="李治玮"/>
    </bean>
```

- 通过类型创建(不推荐，类型可能相同)

```xml
	<bean id="user" class="com.kuang.pojo.User">
  	 	 <constructor-arg type="java.lang.String" value="LZW"/>
	</bean>
```

- 直接通过参数名来创建(推荐)

```xml
    <bean id="user" class="com.kuang.pojo.User">
        <constructor-arg type="java.lang.String" value="LZW"/>
    </bean>
```

**总结：在配置文件加载的时候，容器中管理的对象就已经创建了**



# 5.Spring配置

## 	5.1 别名

```xml
    <alias name="user" alias="asdasd"/>
```



## 	5.2 Been的配置

​	id：bean的唯一标识符，也就是相当于我们的变量名

​	class：bean对象所对应的全限定名：包名+类型

​	name：别名，且可以同时取多个别名

​	

## 	5.3 import

​	一般用于团队开发，他可以将多个配置文件，导入合并为一个

```xml
<import resource="beans.xml"/>
<import resource="beans2.xml"/>
<import resource="beans3.xml"/>
```



# 6.依赖注入



## 		6.1 构造器注入

- 详情见

  ​    [第四章IOC创建对象的方式](#4.IOC创建对象的方式)

##     6.2 Set方式注入[重点]

- 依赖注入：Set注入！
  - 依赖：bean对象创建依赖于容器
  - 注入：bean对象中的所有属性，由容器来注入

【环境搭建】

1.复杂类型

```java
public class Address {
    private String address;

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
}
```

2.真实测试对象

```java
public class Student {
    private String name;
    private Address address;
    private String[] books;
    private List<String> hobbys;
    private Map<String, String> card;
    private Set<String> games;
    private String wife;
    private Properties info;
}
```

3.beans.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	<!--第一种：普通值注入，value-->
    <bean id="student" class="com.kuang.pojo.Student">
        <property name="name" value="李治玮"/>
    </bean>

</beans>
```

4.测试类

```java
public class MyTest {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        Student student = (Student) context.getBean("student");
        System.out.println("名字:"+student.getName());
    }
}
```



## 	6.3 拓展方式注入

​	我们可以使用p空间命令和c空间命令来注入 

```xml
    <!--p命名空间注入，可以直接注入属性的值,property-->
    <bean id="user" class="com.kuang.pojo.User" p:name="lzw" p:age="18"/>

    <!--c命名空间注入，通过构造器注入:construct-args-->
    <bean id="user2" class="com.kuang.pojo.User" c:name="lll" c:age="10"/>
```

测试

```java
@Test
public void test2(){
    ApplicationContext context = new ClassPathXmlApplicationContext("userbeans.xml");
    User user = context.getBean("user"， User.class);
    System.out.println(user.toString());
    }
```

注意点：p命名和c命名空间不能直接使用，需要导入xml约束

```xml
	xmlns:c="http://www.springframework.org/schema/c"
	xmlns:p="http://www.springframework.org/schema/p"
```



## 6.4 been的作用域



1.单例模式(默认)

![image-20200929145832116](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200929145832116.png)

```xml
    <bean id="user2" class="com.kuang.pojo.User" c:name="lll" c:age="10" scope="singleton"/>

```



2.原型模式：每次从容器中get的时候，都会产生一个新对象

![image-20200929150957431](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200929150957431.png)

```xml
    <bean id="user2" class="com.kuang.pojo.User" c:name="lll" c:age="10" scope="prototype"/>
```



3.其他的request,session,application只能在web开发中使用到



# 7.Bean自动装配

- 自动装配是Spring满足bean依赖的一种方式
- Spring会在上下文中自动寻找，并自动给bean装配属性



在Spring中有三种装配的方式

1.在xml中显示的配置

2.在java中显示配置

**3.隐式的自动装配bean(重要)**



## 	7.1 测试

环境搭建:一个人有两个宠物



## 	7.2 ByName自动装配

```xml
    <bean id="people" class="com.kuang.pojo.Peaple" autowire="byName">
        <property name="name" value="lzw"/>
    </bean>
```



## 	7.3 ByType自动装配

```xml
    <bean id="people" class="com.kuang.pojo.Peaple" autowire="byType">
        <property name="name" value="lzw"/>
    </bean>
```



 小结

byName:会自动在容器上下文中查找，和自己对象set方法后面的值对应的bean id!

​	==要保证所有的bean的id唯一，并且这个bean需要和自动注入的属性的set方法的值一致==

byName:会自动在容器上下文中查找，和自己对象set方法后面的值对应的bean id!

​	==要保证所有的bean的class唯一，并且这个bean需要和自动注入的属性的类型一致==



## 	7.4 使用注解实现自动装配

​	要使用注解须知:

​			1. 导入约束

​			2. ==配置注解的支持	 <context:annotation-config/>==

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>
</beans>
```



**==@Auotowired==**

```java
	@Autowired
	@Qualifier(value = "dog1")
	private Dog dog;
```

直接在属性上使用即可

如果@Autowired自动装配的环境比较复杂，自动装配无法通过一个注解【@Autowire】完成的时候，我们可以使用**@Qualifier(value=“xxx”)**去配置@Autowire的使用，指定一个唯一的bean使用



==**@Resource**==

```java
    @Resource(name = "dog1")
    private Dog dog;
```



小结：

@Resource和@Autowired的区别

- 都是用来自动装配的，都可以放在属性字段上
- @Autowired通过byTepe的方式实现
- @Resource默认通过byname的方式实现，如果找不到名字，则通过byType实现！如果两个都找不到的情况下，就报错！
- 执行顺序不同



# 8. 使用注解开发



1.been

2.属性如何注入

```java
@Component
public class User {
    public String name;
    //相当于 <bean name="name" class="com.kuang.pojo.User"/>
    @Value("111")
    public void setName(String name) {
        this.name = name;
    }
}
```

3.衍生的注解

@Component有几个衍生注解，我们在web开发中，会按照mvc三层架构分层！

- dao 【@Repository】

- service【@Service】

- controller【@Controller】这四个注解功能都是一样的，都是代表将某个类注册到Spring中，装配Been

  

4.自动装配

```xml
- @Autowired :自动装配类型，名字
    如果Autowired不能唯一自动装配上属性，则需要通过@Qualifier(value="xxx")
- @Resource  :自动装配名字，类型
- @Nullable  ：如果字段标记了这个注解，说明这个字段可以为null
```



5.小结



    <!--开启注解支持-->
    <context:annotation-config/>
    <!--指定要扫描的包，这个包下的注解就会生效-->
    <context:component-scan base-package="com.Lee"/>
​	xml与注解：

- xml更加万能，适用于任何场合，维护方便
- 注解不是自己的类用不了，维护相对复杂



​	xml与注解最佳实践：

- xml用来管理Been

- 注解只负责完成属性的注入

- 我们在使用的过程中，只需要注意一个问题，必须让注解生效

  即：开启注解的支持

```xml
<!--开启注解支持-->
<context:annotation-config/>
<!--指定要扫描的包，这个包下的注解就会生效-->
<context:component-scan base-package="com.Lee"/>
```



# 9. 使用Java的方式配置Spring

完全不使用Spring的xml配置，全权交给java来做！

JavaConfig使Spring的子项目，在Spring4之后，成了核心功能

```java
public class MyTest {
    public static void main(String[] args) {
        //如果完全使用了配置类方式去做，我们就只能通过AnnotationConfig上下文来获取容器，通过配置类的class对象加载
        ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
        User getUser = (User) context.getBean("getUser");//getUser是Been的名字
        System.out.println(getUser.getName());
    }
}
```



# 10. 代理模式

代理模式就是SpringAOP的底层【SpringAOP 和 SpringMVC】

​	代理模式的分类：

- 静态代理
- 动态代理

![image-20201010152420109](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201010152420109.png)

## 10.1 静态代理

角色分析：

- 抽象角色：一般会使用接口或者抽象类来解决
- 真实角色：被代理的角色
- 代理角色：代理真实角色，代理真实角色后，我们一般会做一些附属操作
- 客户：访问代理对象的人



代码步骤：

​	1.接口

```java
//租房
public interface Rent {
    public void rent();
}
```

​	2.真实角色

```java
//房东
public class Host implements Rent{
    public void rent() {
        System.out.println("房东要出租房子");
    }
}
```

​	3.代理角色

```java
public class Proxy implements Rent {
    private Host host;

    public void rent() {
        host.rent();
    }

    public Proxy() {
    }

    public Proxy(Host host) {
        this.host = host;
    }

    //看房
    public void seeHouse() {
        System.out.println("中介带你看房");
    }

    //收费
    public void fee() {
        System.out.println("收中介费");
    }

    //签合同
    public void contract() {
        System.out.println("签合同");
    }
}
```



​	4.客户端访问代理角色

```java
public class Client {
    public static void main(String[] args) {
        //房东要出租房子
        Host host = new Host();
        //代理
        Proxy proxy = new Proxy(host);
        proxy.rent();
        proxy.seeHouse();
        proxy.fee();
        proxy.contract();
    }
}
```



代理模式的好处：

- 可以使真是角色的操作更加纯粹，不用去关注一些公共的业务

- 公共也就交给代理角色！实现了业务的分工

- 公共业务发生拓展的时候，方便集中管理

  

代理模式的缺点:

- 一个真实角色就会产生一个代理角色，代码量会翻倍，开发效率会变低



## 10.2 动态代理

- 动态代理和静态代理角色一样
- 动态代理的代理代理类是动态生成的，不是我们直接写好的！
- 动态代理分为两大类：基于接口的动态代理，基于类的动态代理
  - 基于接口   —   JDK动态代理
  - 基于类：cglib
  - java字节码实现：javasist



需要了解两个类：

​			Proxy：代理

​			InvocationHandler：调用处理程序

```java
//会用这个类,自动生成代理类
public class ProxyInvocationHandler implements InvocationHandler {

    //被代理的接口
    private Object target;

    public void setTarget(Object target) {
        this.target = target;
    }
    //生成得到的代理类
    public Object getProxy() {
        return Proxy.newProxyInstance(this.getClass().getClassLoader(),target.getClass().getInterfaces(),this);
    }
    //处理代理实例,并返回结果
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //动态代理的本质就是使用反射机制
        log(method.getName());
        Object result = method.invoke(target, args);
        return result;
    }

    public void log(String msg){
        System.out.println("执行了"+msg+"方法");
    }
}
```

动态代理其实挺简单。就两个类。

生成代理类Proxy.newProxyInvocation(参数1.参数2，参数3)

- 参数1：表名你要用那个类加载器去加载生成的代理类。（这个是JVM类加载的知识，可以去了解一下，挺简单）。

- 参数2：说明你要生成的代理类的接口。

- 参数3：实现了InvocationHandle的类，这个类只有一个方法需要你要实现它。
  invoke(Object proxy, Method method, Object【】 args) ｛

```java
Proxy.newProxyInstance(this.getClass().getClassLoader(),target.getClass().getInterfaces(),this);
```

这个方法第一个参数，是生成的代理类，目前没发现用处，不管它。
		第二个参数，是执行的方法(利用反射的原理，可以去看反射，也很简单。)
		第三个参数，是执行某方法需要的参数。
		第二个第三个参数解释执行的方法意思是：代理类不是要代理某个对象么，然后增强里面的方法么，指得就是这个方法，代理类会为几乎所有方法都增强，除非你在这里做判断。

返回值，是执行这个方法所返回的值。

然后你要去执行方法，就是用第二参数的invoke(obj,args);第一个参数是你要增强的对象。第二个是参数。object是你返回的类型

Object object= method.invoke(obj,args);
｝



# 11. AOP

AOP（Aspect oriented Programming）：面向切面编程

**在AOP中切面就是与业务逻辑独立，但又垂直存在于业务逻辑的代码结构中的通用功能组合；切面与业务逻辑相交的点就是切点；连接点就是把业务逻辑离散化后的关键节点；切点属于连接点，是连接点的子集；Advice（增强）就是切面在切点上要执行的功能增加的具体操作；在切点上可以把要完成增强操作的目标对象（Target）连接到切面里，这个连接的方式就叫织入。**

- `Aspect`（切面）： Aspect 声明类似于 Java 中的类声明，在 Aspect 中会包含着一些 Pointcut 以及相应的 Advice。
- `Joint point`（连接点）：表示在程序中明确定义的点，典型的包括方法调用，对类成员的访问以及异常处理程序块的执行等等，它自身还可以嵌套其它 joint point。
- `Pointcut`（切点）：表示一组 joint point，这些 joint point 或是通过逻辑关系组合起来，或是通过通配、正则表达式等方式集中起来，它定义了相应的 Advice 将要发生的地方。
- `Advice`（增强）：Advice 定义了在 `Pointcut` 里面定义的程序点具体要做的操作，它通过 before、after 和 around 来区别是在每个 joint point 之前、之后还是代替执行的代码。
- `Target`（目标对象）：织入 `Advice` 的目标对象.。
- `Weaving`（织入）：将 `Aspect` 和其他对象连接起来, 并创建 `Advice`d object 的过程



## 11.1 使用Spring实现Aop

【重点】使用AOP织入，必须要导入一个依赖包

```xml
<dependencies>
    <dependency>
        <groupId>org.aspectj</groupId>
        <artifactId>aspectjweaver</artifactId>
        <version>1.9.4</version>
    </dependency>
</dependencies>
```



方法一：使用Spring的API接口【主要SpringAPI接口实现】

```xml
方式一:使用原生的String API接口
    <!--配置aop-->
    <aop:config>
        <!--切入点:expression:表达式.execution(要执行的位置!)-->
        <aop:pointcut id="pointcut" expression="execution(* com.Lee.service.UserServiceImpl.*(..))"/>
        <!--执行环绕增强-->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
        <aop:advisor advice-ref="afetlog" pointcut-ref="pointcut"/>
    </aop:config>
```



方式二：自定义来实现AOP【主要是切面定义】

```xml
    <!--方式二:自定义类-->
    <bean id="diy" class="com.Lee.diy.DiyPointCut"/>
    <aop:config>
        <!--自定义切面,ref:要引用的类-->
        <aop:aspect ref="diy">
            <!--切入点-->
            <aop:pointcut id="pointcut" expression="execution(* com.Lee.service.UserServiceImpl.*(..))"/>
            <!--通知-->
            <aop:before method="before" pointcut-ref="pointcut"/>
            <aop:after method="after" pointcut-ref="pointcut"/>
        </aop:aspect>
    </aop:config>
```





## 11.2 execution表达式

开发项目中经常会使用spring的AOP切面功能，用XML配置或注解的方式都可以。
不管用那种方式都要定义pointcut切入点

例如：常用的一种表达式是如

```
execution (* com.db.dao..*.*(..))
```

整个表达式可以分为五个部分：

1、execution(): 表达式主体。

2、第一个*星号：表示返回类型，星号表示所有的类型。注意星号后面有个空格。

3、包名com.db.dao：表示需要拦截的包名，只拦截这个包，其他包不拦截。
报名后面的两个句点表示当前包和当前包的所有子包，com.db.dao包、子孙包下所有类的方法。

4、第二个*号：表示类名，星号表示所有的类。

5、*(..)最后这个星号表示方法名，星号表示所有的方法，后面括弧里面表示方法的参数，两个句点表示任何参数。









