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

## 3.1 





























