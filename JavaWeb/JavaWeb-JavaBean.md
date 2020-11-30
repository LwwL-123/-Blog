# 什么是javaBean

- **`JavaBean`就是一个普通的java类**，也称之为简单java对象--`POJO`（Plain Ordinary Java Object），**是Java程序设计中一种设计模式，是一种基于 Java 平台的软件组件思想**

- JavaBean遵循着特定的写法，通常有以下的规则：

- - **有`无参`的构造函数**
  - **成员属性`私有化`**
  - **封装的属性如果需要被外所操作，必须编写public类型的setter、getter方法**

上面的文字看起来好像很高大上，javaBean其实非常简单，**下面的代码就是按照特定写法、规则编写的一个JavaBean对象**

```JAVA
public class Person {
    private String username ;
    private int age;

    public Person() {

    }


    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```



# 为什么需要使用Javabean

- 使用javaBean的好处就是：**封装，重用,可读**！
- 下面引用知乎一段回答：

> JaveBean你可以理解为一辆货车，在你的java端和web页面进行数据传递的载体，你当然可以每个变量单独传递，或者使用集合传递，但是**javabean可以使你的数据更有可读性，方便开发时明确变量的意义**，也使其他阅读你代码的人能直接你的意图

如果把bean类与数据库联合使用，一张表使用bean类，可以使你的代码更加简洁高效，易于理解，现在大多数框架都会使用这种机制。



# JSP行为--JavaBean

- JSP技术提供了**三个关于JavaBean组件的动作元素**，即JSP行为（标签），它们分别为：

```JSP
<jsp:useBean>【在JSP页面中查找javaBean对象或者实例化javaBean对象】
<jsp:setProperty>【设置javaBean的属性】
<jsp:getProperty>【获取javaBean的属性】
```

































