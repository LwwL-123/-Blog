# JavaScript

# 1. 概述

JavaScript是世界上最流行的脚本语言，因为你在电脑、手机、平板上浏览的所有的网页，以及无数基于HTML5的手机App，交互逻辑都是由JavaScript驱动的。简单地说，JavaScript是一种运行在浏览器中的解释型的编程语言。

==一个合格的后端人员，必有需要**精通**JavaScript==

# 2. 快速入门

## 2.1 引入JavaScript

1.内部标签

```html
<script>
	alert('hello');
</script>
```

2.外部引用

abc.js

```java
alert('hello');
```

引用

```html
<script src="abc.js"></script>
```



## 2.2 基本语法入门

```html
    <!--严格区分大小写-->
    <script>
        // 1.定义变量
        var num = 1;
        var name = "lzw";
        // 2.条件控制
        if(2>1){
            alert(name);
        }
        //console.log(name) 在浏览器的控制台打印变量
    </script>
```

## 2.3 数据类型

数值,文本,图形,音频,视频

==number==：js不区分小数和整数,Number

==字符串==：‘abc’  “abc”

==布尔值==：true，false

==逻辑运算==：

```
&& 与 :两个都为真,结果为真
|| 或 :一个为真,结果为真
!  非 :取反
```

==比较运算符==：!!!!重要

```java
=		赋值  
==		等于(类型不一样,值一样,也会判断为true)
===		绝对等于(类型一样,值也一样,结果才为true)
```

==null和undefined==

- null 空
- undefined 未定义

==数组==

java的数组必须是相同类型的对象,js中不需要

```javascript
var arr=[1,2,3,"hello",null,true];
```

==对象==

对象是大括号,数组是中括号

```javascript
var Person = {
    name:"lzw",
    age:22,
    tags:[1,2,3,4,5]
}
```

## 2.4 严格检查模式

```html
"use strict";
```

# 3. 数据类型

## 3.1 字符串 

- 正常字符串我们使用单引号或者双引号包裹
- 注意转义字符 \

```javascript
\'
\n
\t
\u4e2d 	unicode字符
\x41	Ascll字符
```

- 多行字符串编写

```javascript
var msg = `
hello
你好
1
2
3
4
`
```

用反引号包裹 ``

- 模板字符串

```javascript
<script>
    let name ="lzw";
    let age = 1;
    let msg = `你好,我是${name},今年${age}岁`
</script>
```

用反引号包裹 ``，用${}引用

- 大小写转换

```javascript
//注意,这里是方法
student.toUpperCase()
student.toLowerCase()
```

- substring

```javascript
[)
 student.substring(1) //从第一个字符串截取到最后
 student.sunstring(1,3)..//左闭右开,包含第一个,不包含第三个
```



## 3.2 数组  

Array可以包含任意的数据类型

```javascript
var arr = [1,2,3,4,5,"lzw"];
```

- 长度

```javascript
arr.length
```

注意:加入给arr.length赋值,数组的大小就会发生变化,如果赋值过小,元素就会丢失

- 通过元素得下标索引 indexOf

```javascript
arr.indexOf('lzw')
//5
```

- slice()    截取Array的一部分,类似String中的substring

- push()，pop()

```javascript
push:压入到尾部
pop:从尾部弹出
```

- unshift(),shift()

```javascript
unshift:压入头部
shift:弹出头部的一个元素
```

- 多维数组

```javascript
var arr = [[1,2],[3,4],['lzw','llzw']];
//arr[0][1]=2
```

- concat()  拼接数组

```javascript
<script>
    var arr1 = [1,2,3];
    var arr2 = ['a','b','c'];
    var arr3 = arr1.concat(arr2)
</script>

arr1 
(3) [1, 2, 3]
arr2
(3) ["a", "b", "c"]
arr3
(6) [1, 2, 3, "a", "b", "c"]
```

注意:concat并没有修改数组,知识会返回一个新的数组

- 连接符join:  打印拼接字符,使用特定的字符串拼接

```javascript
arr1.join('-')
"1-2-3"
```



## 3.3 对象

若干键值对

```javascript
var person = {
    name: 'lzw',
    age: 1,
    gender: 'male',
    score: 60
}//使用逗号隔开,最后一个属性不加逗号
```

1.对象赋值

```javascript
person.name='lll'
```

2.使用一个不存在的对象属性,不会报错!

```javascript
person.name1
undefined
```

3.动态删减属性,通过delete删除对象的属性

```javascript
delete person.gender
true
person
{name: "lzw", age: 1, score: 60}
```

4.动态的添加,直接给新的属性添加值即可

```javascript
person.gender = 'male'
"male"
person
{name: "lzw", age: 1, score: 60, gender: "male"}
```

5.判断属性值是否偶在这个对象中

```javascript
'age' in person
true
//继承
'toString' in person
true
```

6.判断一个属性是否是这个对象自身拥有的 hasOwnProperty()

```javascript
person.hasOwnProperty('toString')
false
person.hasOwnProperty('age')
true
```



## 3.4 Set和Map

Map:

```javascript
var map = new Map([['lzw',100],['zw',90],['w',80]]);
var score = map.get('lzw');//通过key获得value
console.log(score);//100
```

Set:无需不重复的集合

```javascript
var set = new Set([1,1,1,2,2,2,3,3])
set
Set(3) {1, 2, 3}

//新增
set.add(4)
Set(4) {1, 2, 3, 4}

//删除
set.delete(4)
true
set
Set(3) {1, 2, 3}
```

## 3.6 itertor

- 遍历数组

```javascript
var arr = [1,2,3];
//通过for of遍历  //for in 是遍历下标
for (let x of arr) {
    console.log(x);
}

1
2
3
```

- 遍历Map

```javascript
var map = new Map([['lzw',100],['zw',90],['w',80]]);
for (let mapElement of map) {
    console.log(mapElement)
}

(2) ["lzw", 100]
(2) ["zw", 90]
(2) [w", 80]
```

# 4. 函数

## 4.1 定义函数

- Java中定义：

```javascript
pbulic 返回值类型 方法名(){
    return 返回值;
}
```

- JavaScript中定义

```javascript
function 函数名(){
    return ;
}
```



> 定义方式一

```javascript
function abs(x){
    if(x>=0)
        return x;
    else
        return -x;
}
```



> 定义方式二

```javascript
var abs = function(x){
    if(x>=0)
        return x;
    else
        return -x;
}
```



> arguments

`arguments`是一个js自带的关键字

代表传递进来的所有参数,是一个数组

> rest

ES6引入的新特性,获取已经定义了的参数之外的所有参数

```javascript
function f(a,b,...rest){
    console.log("a="+a);
    console.log("b="+b);
    console.log("rest="+rest);
}

f(1,2,3,4,5,6,7,8,9,10)
a=1
b=2
rest=3,4,5,6,7,8,9,10
```

## 4.2 变量的作用域

在JavaScript中，var定义变量其实是有作用域的

假设在**函数体中声明，则在函数体外不能使用**（非要实现的话，后面可以研究`闭包`）



假设在JavaScript中,函数查找变量从自身函数开始,由`“内”`向`“外”`查找，假设外部存在这个同名的函数变量，则内部函数会屏蔽外部函数的变量

**规范**：所有变量定义都放在函数的头部，不要乱放，便于代码维护



> 全局函数

全局对象window

```javascript
var x = 'xxx';
alert(x);
alert(window.x)//默认所有的全局变量,都会自动绑定在window对象下
```

alert()这个函数本身也是一个`window`的变量



JavaScript实际上只有一个全局作用域，任何变量（函数也可视为变量），假设没有在函数作用范围内找到，就会向外查找，如果在全局作用域都没有找到，报错`ReferenceError`

>规范

由于我们所有的全局变量都会绑定到我们的window上,如果不同的js文件,使用了相同的全局变量,就会产生冲突

那我们如何能减少冲突呢

```javascript
//唯一全局变量
var LeeApp = {};

//定义全局变量
LeeApp.name = 'lzw';
LeeApp.add = function(a,b){
    return a+b;
}
```

把自己的代码全部放入自己定义的唯一空间名字中,降低全局命名冲突的问题



> 局部作用域let

```javascript
function aaa(){
    for (var i = 0; i < ; i++) {
        console.log(i)
    }
    console.log(i+1);//问题:除了这个作用域 i还是可以使用
}
aaa();
1,2,3,....,99,101.
```

ES6 `let`关键字，解决局部作用于冲突问题

```javascript
function aaa(){
    for (let i = 0; i < ; i++) {
        console.log(i)
    }
    console.log(i+1);//i is not defined
}
aaa();
1,2,3,....,99
```

建议都用`let`去定义局部作用域的变量

> 常量const

在ES6之前，怎么定义常量：只有用全部`大写字母`命名的变量，就是常量。建议不要修改这样的值

在ES6引入了常量关键字`const`

## 4.3 方法

> 定义方法

方法就是把函数放在对象里面，对象只有两个东西：属性和方法

```javascript
var Lee = {
    name: 'lzw',
    birth: 1998,
    age: function(){
        var now = new Date().getFullYear();
        return now-this.birth;
    }
}
//属性
Lee.name
//方法
Lee.age();
```



> apply

在js中可以控制this的指向！

```javascript
function getAge() {
    var now = new Date().getFullYear();
    return now-this.birth;
}

var Lee = {
    name: 'lzw',
    birth: 1998,
    age: getAge
}

var xiaoming = {
    name: '小明',
    birth: 2019,
    age: getAge
}

getAge.apply(Lee,[]);//this.指向了Lee，参数为空
```



# 5. 内部对象

## 5.1 Date

```javascript
    var now = new Date();
    now.getFullYear();//年
    now.getMonth();//月
    now.getDate();//日
    now.getDay();//星期几
    now.getHours();//时
    now.getMinutes();//分
    now.getSeconds();//秒
    now.getTime();//时间戳 世界统一
    console.log(new Date(1603249847736));//时间戳转时间
```

## 5.2 json

> json是什么

早期，所有的数据习惯使用XML文件！

- JSON（JavaScript Object Notation，JS对象简谱）是一种轻量级的数据交换格式
- 简洁和清晰的层次结构使得JSON成为理想的数据交换语言
- 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率

在JavaScript中一切皆为对象，任何js支持的类型都可以用json来表示：

- 对象都用{}
- 数组都用[]
- 所有的键值对都是用key：value

```javascript
    var user={
        name:'lzw',
        age:3,
        gender:'male'
    }
    //将对象转换为json {"name":"lzw","age":3,"gender":"male"}
    var jsonUser = JSON.stringify(user);

    //将json字符串转换为对象,参数为json字符串
    var obj = JSON.parse('{"name":"lzw","age":3,"gender":"male"}')
```



很多人不清楚，JSON和JS对象的区别

```javascript
var obj = {a:'hello',b:'hellob'}
var json = '{"a":"hello","b":"hellob"}'
```



## 5.3 AJAX

- 原生的js写法   xhr异步请求
- jQuery封装好的方法  $(“#name”).ajax(“”)
- axios请求

# 6. 面向对象编程

## 6.1 什么是面向对象

JavaScript，java，c#…… 

> 一般的面向对象：

- 类：模板
- 对象：具体的实例

> JavaScript中的面向对象

在JavaScript中需要大家换一下思路

```javascript
    var Student = {
        name:"lzw",
        age:3,
        gender:"male",
        run: function(){
            console.log(this.name+"正在跑步");
        }
    };
    var xiaoming = {
        name:"xiaoming"
    };
    xiaoming.__proto__ = Student;//__proto__：原型，相当于继承
//xiaoming.run()
//xiaoming正在跑步
```



> class继承

`class`关键字，是在ES6之后引入的

1.定义一个类，属性，方法

```javascript
    // function Student(name){
    //     this.name = name;
    // }
    //给Student增加一个方法
    // Student.prototype.hello = function (){
    //     alert('hello')
    // };
    //ES6之后=============
    //定义一个学生的类
    class Student{
        constructor(name) {
            this.name=name;
        }
        
        hello(){
            alert('hello');
        }
    }
var xiaoming = new Student('xiaoming');
var xiaohong = new Student('xiaohong');
```

2.继承

```javascript
var xiaoming = new Student('xiaoming');

    class university extends Student{
        constructor(name,grade) {
            super(name);
            this.grade=grade;
        }
        mygrade(){
            console.log('我是一名大学生'+this.name);
        }
    }
var xiaohong = new university('xiaohong',100);
```

![image-20201021150015402](https://gitee.com/lzw657434763/pictures/raw/master/Blog/image-20201021150015402.png)

> 原型链

__proto\_\_:

![img](https://gitee.com/lzw657434763/pictures/raw/master/Blog/850375-20190708152327825-11086376.png)

# 7. **操作BOM对象**（重点）

> 浏览器介绍

JavaScript和浏览器关系？

JavaScript就是为了能让他在浏览器中运行

BOM：浏览器对象模型



> window(重要)

window代表浏览器窗口

```javascript
window.innerHeight
258
window.innerWidth
1093
window.outerHeight
728
window.outerWidth
1366
```

> Navigator

Navigator，封装了浏览器的信息

```javascript
navigator.appName
"Netscape"
navigator.appVersion
"5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.75 Safari/537.36"
navigator.userAgent
"Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.75 Safari/537.36"
navigator.platform
"Win32"
```

大多数时候，我们不会使用`Navigator`对象，因为会被人为修改！

不建议使用这些属性来判断和编写代码

> screen

```java
screen.width
1366
screen.height
768
```

> location

location代表当前页面的URL信息

```javascript
host: "lzw.today"
href: "http://lzw.today/"
protocol: "http:"
reload: ƒ reload() //刷新网页
```



> document

document代表当前的页面，HTML，DOM文档树

```javascript
<dl id="app">
    <dt>Java</dt>
    <dd>JavaEE</dd>
    <dd>JavaSE</dd>
</dl>

<script>
    var dl = document.getElementById("app");
</script>
```

获得cookie

```
document.cookie
"BIDUPSID=9AB28203AE5E7ECE52D8FCB7103D1A50; PSTM=1600673778; BD_UPN=12314353; BAIDUID=09BDBEBBACB4522C296ED70DB3ADC0BE:FG=1; BDORZ=FFFB88E999055A3F8A630C64834BD6D0; BDRCVFR[NPt2Vg_wYt_]=mk3SLVN4HKm; delPer=0; BD_CK_SAM=1; BD_HOME=1; PSINO=2; H_PS_PSSID=; H_PS_645EC=382cd7TLpK8%2BDIC32qItFow472lEjT0hRVIueTPBxJeBaSKRoukvh3jz6nr5N4ONSp3VKalp; BA_HECTOR=ah0k848l0k2h0ldvcn1fovpa40k; BDSVRTM=0; COOKIE_SESSION=0_0_1_0_1_3_1_0_0_1_66_0_0_0_25_0_1603265862_0_1603265837%7C1%230_0_1603265837%7C1"
```

# 8. 操作DOM对象（重点）

> 核心

浏览器网页就是一个Dom树形结构

- 更新：更新Dom节点
- 遍历Dom节点：得到Dom节点
- 删除：删除一个Dom节点
- 添加：添加一个新的节点

要操作一个Dom节点，就必须先获得这个Dom节点

> 获得Dom节点

```javascript
    <div id="father">
        <h1>一级标题</h1>
        <p id="p1">p1</p>
        <p class="p2">p2</p>
    </div>
    <script>
        var h1 = document.getElementsByTagName('h1');
        var p1 = document.getElementById("p1");
        var p2 = document.getElementsByClassName('p2');
        var father = document.getElementById('father');
    </script>

father.children//获取父节点下的所有子节点
HTMLCollection(3) [h1, p#p1, p.p2, p1: p#p1]
//father.firstChild
//father.firstChild                 
```

这是原生代码，后期我们都使用JQ



> 更新节点

`id1.innerText='123'`修改文本的值

`id1.innerHTML='<strong>123<strong>'`可以解析HTML文本标签

`id1.style.color='yellow'`设置颜色

`id1.style.fontSize='200px'`设置字体大小

`id1.style.padding='50px'`设置padding

> 删除节点

步骤：先获取父节点，通过父节点删除自己

```javascript
var ss = document.getElementById('s_wrap')    //获取节点
var father = ss.parentElement				//获取父节点
father.removeChild(ss)					    //通过父节点，删除节点
```



> 插入节点

我们获得了某个Dom节点，假设这个dom节点是空的，我们通过innerHTML可以增加一个元素，但是这个DOM节点已经存在元素，我们就不能这么使用，因为会产生覆盖



> 创建节点















