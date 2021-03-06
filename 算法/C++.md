# C++ 常用语法

## 头文件

```cpp
#include <iostream>
#include <stdio.h>

#include <vector> 
#include <string>
#include <map> 

#include <algorithm>
using namespace std;
```

## 大小写转换

```c++
toupper('b');//B
tolower('B');
```

## c++链表创建

```c++
ListNode *l3 =new ListNode(INT_MAX);

// INT_MAX = 2^31-1
```



## 容器

| **标准容器类** |                   **特点**                   |
| -------------- | :------------------------------------------: |
| vector         |   从后面快速的插入与删除，直接访问任何元素   |
| map            | 一对多映射，基于关键字快速查找，不允许重复值 |

| 表 达 式      | 返 回 类 型 | 说 明               |
| ------------- | ----------- | ------------------- |
| a.size()      | 无符号整型  | 返回元素个数        |
| a.swap()      | void        | 交换a和b内容        |
| a.insert(p,t) | 迭代器      | 将t插入到p的前面    |
| a.erase(p)    | 迭代        | **删除p所指向的元素 |
|               |             |                     |
|               |             |                     |
|               |             |                     |



| **表 达 式**        | **返 回 类 型** | **含 义** | **支 持 的 容 器**      |
| ------------------- | --------------- | --------- | ----------------------- |
| **a.push_front(t)** |                 |           | **list、deque**         |
| **a.push_back(t)**  |                 |           | **vector、list、deque** |
| **a.pop_front(t)**  |                 |           | **list、deque**         |
| **a.pop_back(t)**   |                 |           | **vector、list、deque** |



## 遍历修改字符串

```c++
for(auto &c:s){
    if(c==' '){
        array.push_back('%');
        array.push_back('2');
        array.push_back('0');
    }
    else
        array.push_back(c);
}
```

## 栈 stack

>  头文件

**#include < stack>**



> **stack的成员函数介绍**

- empty() 堆栈为空则返回真


- pop() 移除栈顶元素


- push() 在栈顶增加元素


- size() 返回栈中元素数目


- top() 返回栈顶元素




## map

>  头文件

**#include < map>**

> **map的成员函数介绍**

- begin()     返回指向map头部的迭代器


- end()      返回指向map末尾的迭代器


- empty()     如果map为空则返回true


- count()     返回指定元素出现的次数


- erase()     删除一个元素


- find()     查找一个元素


- size()     返回map中元素的个数


- swap()      交换两个map

## c++ queue

>  头文件

**#include < queue >**

>  定义

- queue< int > s;
- queue< string > s;

> 常用函数

1. `push` ：在队列尾部插入元素
2. `pop` : 移除最顶端的数据
3. `size` : 输出队列中数据元素的个数
4. `empty` : 判断队列是否为空
5. `front` ：返回队列中第一个元素，但是并不删除
6. `back` ：返回队列中最后一个元素，并且不删除

