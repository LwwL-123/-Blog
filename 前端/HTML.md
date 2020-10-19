# 1. HTML

HTML： Hyper Text Markup Language（**超文本标记语言**）



W3C标准：

- 结构化标准语言（HTML，XML）
- 表现标准语言（CSS）
- 行为标准（DOM,ECMAScript）

## 1.1 网页基本信息



```html
<!--DOCTYPE告诉浏览器,要使用什么规范-->
<!DOCTYPE html>

<html lang="en">
    
<!--代表网页头部-->
<head>
    <!--meta用来描述网页的一些信息-->
    <!--meta一般用来做SEO-->
    <meta charset="UTF-8">

    <!--网页标题-->
    <title>我的第一个网页</title>
</head>


<!--代表网页主题-->
<body>
    <h3>sss</h3>
</body>

</html>
```

## 1.2 网页的基本标签

### 	1.2.1 标题标签

```html
<!--标题标签-->
<h1>一级标签</h1>
<h2>二级标签</h2>
<h3>三级标签</h3>
```

### 	1.2.2 段落标签

```html
<!--段落标签-->
<p>1111  2222</p>
<p>3333  4444</p>
```

### 	1.2.3 换行标签

```html
<br/>
```

### 	1.2.4 水平线标签

```html
<hr>
```

### 	1.2.5 粗体斜体

```html
<!--粗体-->
<strong>111</strong>
<!--斜体-->
<em>222</em>
```

### 	1.2.6 特殊符号

```html
<!--特殊符号-->
空格&nbsp;空格
<!--直接写&然后调用	-->
```

## 1.3 图片标签

```html
<img src="../resouce/image/1.jpg" alt="图片加载失败" title="头像" width="200" height="200"/>
```

src：图片地址   ../相对地址

alt：图片名字

title：悬停文字

width，height

## 1.4 链接标签

```html
<!--target="_blank"在新标签中打开-->
<!--target="_self"在自己界面中打开-->
<a href="http://www.lzw.today" target="_blank">点我跳转</a>


<a href="http://www.lzw.today">
    <img src="../resouce/image/1.jpg" alt="图片加载失败" title="头像" width="200" height="200"/>
</a>
```



锚链接:

```html
<a name="top"></a>

<a href="#top">回到顶部</a>
```



## 1.5 列表

```html
<!--有序列表-->
        <ol>
            <li>java</li>
            <li>python</li>
            <li>c</li>
        </ol>
<!--无序列表-->
        <ul>
            <li>java</li>
            <li>python</li>
            <li>c</li>
        </ul>

<!--自定义列表-->
        <dl>
            <dt>学科</dt>

            <dd>java</dd>
            <dd>python</dd>
            <dd>c</dd>
        </dl>
```

## 1.6 表格

```html
<!--表格 table
行 tr
列 td
-->

<table border="1px">
    <tr>
        <!--colspan 跨列-->
        <td colspan="2">1-1</td>
        <td>1-3</td>
        <td>1-4</td>
    </tr>

    <tr>
        <!--rowspan 跨行-->
        <td rowspan="2">2-1</td>
        <td>2-2</td>
        <td>2-3</td>
        <td>2-4</td>
    </tr>

    <tr>
        <!--rowspan 跨行-->
        <td>3-2</td>
        <td>3-3</td>
        <td>3-4</td>
    </tr>

</table>
```

- 行 tr
- 列 td

## 1.7 页面结构分析

| 元素名  |                       描述                       |
| :-----: | :----------------------------------------------: |
| header  |  标题头部区域的内容(用于页面或页面中的一块区域)  |
| footer  | 标记脚部区域的内容(用于整个页面或页面的一块区域) |
| section |            Web页面中的一块独立的区域             |
| article |                   独立文章内容                   |
|  aside  |                  相关内容或应用                  |
|   nav   |                   导航辅助内容                   |

## 1.8 iframe内联框架

```html
<iframe src="http://www.lzw.today" name="blog"></iframe>
```



## ==1.9 表单==



|   属性    |                             说明                             |
| :-------: | :----------------------------------------------------------: |
|   type    | 指定元素的类型。text，password，checkbox，radio，submit，reset，file，hidden，image和button，默认为text |
|   name    |                      指定表单元素的名称                      |
|   value   |          元素的初始值。type为dadio时必须指定一个值           |
|   size    | 指定表单元素的初始宽度。当type为text或password时，表单元素的大小以字符为单位。对于其他类型，宽度以像素为单位 |
| maxlength |           type为text或password时，输入的最大字符数           |
|  checked  |         type为radio或checkbox时，指定按钮是否被选中          |

### 1.9.1 单选框

```html
<form action="1.第一个网页.html" method="get">
    <p>
        <input type="radio" value="boy" name="gender">男
        <input type="radio" value="girl"name="gender">女
    </p>
    <p>
        <input type="submit">
        <input type="reset">
    </p>
</form>
```

> 单选框标签

- input type="radio"
- value:单选框的值
- name:表示组

### 1.9.2 多选框

```html
<p>
    <input type="checkbox" value="sleep" name="hobby">睡觉
    <input type="checkbox" value="code" name="hobby">代码
    <input type="checkbox" value="game" name="hobby">游戏
</p>
```