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























