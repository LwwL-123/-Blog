

# 1. Java Reflection

Reflection（反射）是Java被视为动态语言的关键，反射机制允许程序在执行期间，借助于Reflection API取得任何类的内部信息，并能直接操作人以对象的内部属性及方法。

```java
Class C = Class.forName("java.lang.String")
```



加载完类之后，在堆内存的方法区中就产生了一个Class类型的对象（一个类对应一个Class对象），这个对象就包含了完整类的结构信息。我们可以通过这个对象看到类的结构。

这个对象就像一面镜子，透过镜子看到类的结构，所以，我们称之为：**反射**



## 1.1 静态语言和动态语音

**动态语言**：

- 是一类在运行时可以改变其结构的语言：例如新的函数、对象、甚至代码可以被引进，已有的函数可以被删除或是其他结构上的辩护。（通俗来说就是运行时代码可以根据某些条件改变自身结构）
- 主要动态语言：Object-C、C#、JavaScript、PHP、Python



静态语言：

- 与动态语言相对，运行时结构不可改变的语言就是静态语言。
- 主要静态语言：Java、C、C++
- Java不是动态语言，但Java可以称之为“准动态语言“。即Java拥有一定的动态性，我们可以利用反射机制获得类似动态语言的特性。Java的动态性让编程的时候更加灵活。



## 1.2 Java反射机制提供的功能

- 在运行时判断任意一个对象所属的类
- 在运行时构造任意一个类的对象
- 在运行时判断任意一个类所具有的成员变量和方法
- 在运行时获取泛型信息
- 在运行时调用任意一个对象的成员变量和方法
- 在运行时处理注解
- 生成动态代理（Aop）



## 1.3 Java反射的优缺点

**优点：**

​			可以实现动态创建对象和编译，体现出很大的灵活性

**缺点：**

​			对性能有影响



# 2. Class类

- Class本身也是一个类
- Class对象只能由系统建立对象
- 一个加载的类JVM中只会有一个Class实例
- 一个Class对象对应的是一个加载到JVM中的一个class文件
- ==每个类的实例都会记得自己是由哪个Class实例所生成==
- 通过Class可以完整的得到一个类中的所有被加载的结构
- Class类是Reflection的根源，针对任何你想动态加载，运行的类，为优先获得的相应的Class对象

## 2.1 常用Class方法

| 方法名                                 | 功能说明                                                    |
| :------------------------------------- | :---------------------------------------------------------- |
| static ClassforName(String name)       | 返回指定类名name的Class对象                                 |
| Object newInstance()                   | 调用却行构造函数，返回Class对象的一个实例                   |
| getName()                              | 返回此Class对象所表示的实体(类，接口，数组类，或void)的名称 |
| Class getSuperClass()                  | 返回当前Class对象的父类的Class对象                          |
| Class[] getinterfaces()                | 获取当前Class对象的接口                                     |
| ClassLoader getClassLoader()           | 返回该类的类加载器                                          |
| Constructor[] getConstructor()         | 返回一个包含某些Constructor对象的数组                       |
| Method getMethod(String name,Class..T) | 返回一个Method对象，此对象的形参类型为paramType             |
| Field[] getDeclaredFields()            | 返回Field对象的一个数组                                     |

## 2.2 Java内存分析

![image-20201012112906582](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201012112906582.png)

## 2.3 类的加载与ClassLoader的理解



如果看过我写`JVM`的那篇文章的同学应该都知道一个对象的加载过程，如果没看过的同学可以再去看看，顺便在这里给大家复习一下：

- 一个`.java`的文件经过`javac`命令编译成功后，得到一个`.class的文件`
- 当我们执行了初始化操作(有可能是new、有可能是子类初始化 父类也一同被初始化、也有可能是反射…等)，会将`.class`文件通过**类加载器**装载到`jvm`中
- 将`.class`文件加载器加载到jvm中，又分了**好几个步骤**，其中包括 **加载、连接和初始化**
- 其中在加载的时候，会在Java堆中**创建一个java.lang.Class类的对象**，这个Class对象代表着**类相关的信息**。







- 加载：将class文件字节码内容加载到内存中，==并将这些静态数据转换成方法取得运行时的数据结构==，然后生成一个代表这个类的java.lang.Class对象
- 链接：将Java类的二进制代码合并到JVM的运行状态之中的过程。
  - 验证：确保加载的类信息符合JVM规范，没有安全方面的问题		
  - 准备：正式为类变量(static)==分配内存并设置类变量默认初始值==的阶段,这些内存都将在方法区中进行分配
  - 解析：虚拟机常亮池内的符号引用（常量名）替换为直接引用(地址)的过程
- 初始化：
  - 执行类构造器<clinit>()方法的过程。类构造器<clinit>()方法是由编译期自动收集类中所有类变量的赋值动作和静态代码块中的语句合并产生的。(类构造器是构造类信息的,不是构造该类对象的构造器)
  - 当初始化一个类的时候,如果发现其父类还没有进行初始化，则需要先触发其父类的初始化
  - 虚拟机会保证一个类的<clinit>()方法在多线程环境中被正确加锁和同步。

![img](https://img-blog.csdn.net/20170430160610299?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvamF2YXplamlhbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)



## 2.4 什么时候会发生类的初始化

- 类的主动引用（一定会发生类的初始化）
  - new一个类的对象
  - 调用类的静态成员（除了final常量）和静态方法
  - 使用java.lang.reflect包的方法对类进行反射调用
  - 当初始化一个类的时候,如果发现其父类还没有进行初始化，则需要先触发其父类的初始化
- 类的被动引用（不会发生类的初始化）
  - 当触发一个静态域时，只有真正声明这个域的类才会被初始化（如：当通过子类引用父类的静态变量，不会导致子类初始化）
  - 通过数组定义类引用，不会触发此类的初始化
  - 引用常量不会触发初始化



## 2.5 类加载器

```java
//获取系统类的加载器
ClassLoader systemClassLoader = ClassLoader.getSystemClassLoader();
System.out.println(systemClassLoader);

//获取系统类加载器的父类加载器-->扩展类加载器
ClassLoader parent = systemClassLoader.getParent();
System.out.println(parent);

//获取扩展类的父类加载器-->根加载器(c/c++)
ClassLoader parent1 = parent.getParent();
System.out.println(parent1);

//测试当前类是哪个加载器加载的
ClassLoader classLoader = Class.forName("com.Lee.reflection.Test05").getClassLoader();
System.out.println(classLoader);
```

![img](https://pic1.zhimg.com/80/v2-3c42da9f8214d69d0f4aee55ac90bbe8_720w.jpg)

双亲委派机制:**如果一个类收到类加载请求，它首先请求父类加载器去加载这个类**，**只有当父类加载器无法完成加载时**(其目录搜索范围内没找到需要的类)，**子类加载器才会自己去加载。**



**双亲委派的优势：**

使用双亲委派模型来组织类加载器之间的关系，有一个显而易见的好处就是Java类随着它的类加载器一起具备了一种带有优先级的层次关系。例如类java.lang.Object(存放于rt.jar中)，是所有类的父类，所以任意一个类启动类加载时，都需要先加载Object类。在类加载器来看，所有的加载Object类的请求，都会逐级委托，最后都委托给Bootstrap根类加载器加载，因此Object类在程序的各种类加载器环境中都是同一个类。（否则，系统中出现的Object类都不尽相同则会出现一片混乱）

## 2.6 有了Class对象能干什么

- 创建类的对象

  - 第一种：调用Class对象的newInstance()方法

    -  必须有一个无参构造器
    -  类的构造器必有足够的访问权限

  - 第二种：1）通过Class类的getDeclaredConstructor取得本类的指定形参类型的构造器

    ​			   2）向构造器的形参中传递一个对象数组进去，里面包含构造其中所需的各个参数

    ​			   3）通过Constructor实例化

```java
Constructor constructor = c1.getDeclaredConstructor(String.class, int.class, int.class);
User user2 = (User) constructor.newInstance("lzw", 001, 23);
```

- 调用指定方法
  - 通过Class类的getMethod()方法取得一个Method对象,并设置所需要的参数类型
  - 之后运用invoke进行调用,并在方法中传递要设置的obj对象的参数信息

```java
Method setName = c1.getDeclaredMethod("setName", String.class);
setName.invoke(user3,"lzw");
```

​		注：若原方法的声明为private，则需要在调用此invoke方法之前，显式调用方法对象的setAccessible(true)方法，则可访问private方法



# 3.总结:



```java
想要使用反射，我先要得到class文件对象，其实也就是得到Class类的对象
Class类主要API：
        成员变量  - Field
        成员方法  - Constructor
        构造方法  - Method
获取class文件对象的方式：
        1：Object类的getClass()方法
        2：数据类型的静态属性class
        3：Class类中的静态方法：public static Class ForName(String className)
--------------------------------  
获取成员变量并使用
        1: 获取Class对象
        2：通过Class对象获取Constructor对象
        3：Object obj = Constructor.newInstance()创建对象
        4：Field field = Class.getField("指定变量名")获取单个成员变量对象
        5：field.set(obj,"") 为obj对象的field字段赋值
如果需要访问私有或者默认修饰的成员变量
        1:Class.getDeclaredField()获取该成员变量对象
        2:setAccessible() 暴力访问  
---------------------------------          
通过反射调用成员方法
        1：获取Class对象
        2：通过Class对象获取Constructor对象
        3：Constructor.newInstance()创建对象
        4：通过Class对象获取Method对象  ------getMethod("方法名");
        5: Method对象调用invoke方法实现功能
如果调用的是私有方法那么需要暴力访问
        1: getDeclaredMethod()
        2: setAccessiable();          
```
