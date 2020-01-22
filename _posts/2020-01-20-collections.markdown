---
layout:     post
title:      "Python 的 Collections模块
"
subtitle:   "Collections模块"
date:       2020-01-20 18:48:00
author:     "tfflyer"
header-img: "img/home-bg-1.jpg"
tags:
    - study report
---

> “Yeah I am studying. ”
>


## Python 的 Collections模块

![image-20200120133526271](https://tva1.sinaimg.cn/large/006tNbRwly1gb2ywzvez4j31ai0jajye.jpg)

### tuple

Tuple 比list好的地方：

 	1. 性能优异
 	2. 线程安全
 	3. 可哈希作为dict的key
 	4. 拆包特性

tuple对应的是struct，而list对应array

### nametuple

`namedtuple`是一个函数，它用来创建一个自定义的`tuple`对象，并且规定了`tuple`元素的个数，并可以用属性而不是索引来引用`tuple`的某个元素。

这样一来，我们用`namedtuple`可以很方便地定义一种数据类型，它具备tuple的不变性，又可以根据属性来引用，使用十分方便。

```python
# -*- coding: utf-8 -*-
# @date: 2020/1/20 3:13 下午
# IDE  : PyCharm
# @name: name_tuple.py
# @author：tfflyer
from collections import namedtuple

User = namedtuple("User", ["name", "age", "school"])
usr=User("wtf", 24, "ppsuc")
print(usr.name)
print(usr.school)
```

相比于class而言，比较省空间，效率较高

 *args 相当于传递一个tuple，一整个元组，比如\*tfflyer(tfflyer为一个tuple)

也可以传入字典

```python
User = namedtuple("User", ["name", "age", "school", "location"])
tfflyer = ("王腾飞", 24, "ppsuc", "henan")
tfflyer_dic={
    "name":"HJJ",
    "age":23,
    "school":"ppsuc",
    "location":"luoyang"
}
usr = User(*tfflyer)
usr2 = User(**tfflyer_dic)
```

** kwargs 按照key给函数参数赋值

```python
usr3 = User._make(tfflyer)
```

使用_make方法可以不用✳️

exec 执行储存在字符串或文件中的Python语句，相比于 eval，exec可以执行更复杂的 Python 代码

```python
exec("print(tfflyer)")
```

> ```python
> # TODO dayday up
> ```

**TODO 可以添加todo事项，还有FIXME等等**

### dict.setdefault()

我们也可以使用dict.setdefault()方法来设置默认值：这个方法结构两个参数，一个是键的名称，另一个是默认值。如果键已经存在字典中就返回它的值，如果没有就将默认值保存并且返回该默认值。用dict.setdefault()重写上面的例子

```python
user_dic = {}
users = [
    "tfflyer1",
    "tfflyer2",
    "tfflyer1",
    "tfflyer3",
    "tfflyer1",
    "tfflyer2",
    "tfflyer1"]
for usr in users:
    user_dic.setdefault(usr, 0)
    user_dic[usr] += 1
print(user_dic)
```

### collections.defaultdict

class collections.defaultdict([default_factory[, …]])

defaultdict类返回一个类似于的字典对象，第一个参数给default_factory属性赋值，其它的参数都传递给dict构造器。通俗来说就是defaultdict类的初始化函数接收一个类型作为参数，当访问的键不存在，实例化一个值作为默认值。

```python
from collections import defaultdict

user_dic = {}
users = [
    "tfflyer1",
    "tfflyer2",
    "tfflyer1",
    "tfflyer3",
    "tfflyer1",
    "tfflyer2",
    "tfflyer1"]
defa_dic = defaultdict(int)
# 传递的为一个可调用对象（函数也阔以）
for usr in users:
    user_dic.setdefault(usr, 0)
    user_dic[usr] += 1
    defa_dic[usr] += 1
```

```python
调用函数
def gen_dic():
    return {
        "name": 0,
        "number": 1
    }


defa_dic = defaultdict(gen_dic)

defa_dic["group1"]
```

### deque双端队列

   deque容器为一个给定***\*类型\****的元素进行**线性处理**，像向量一样，它***\*能够快速地随机访问任一个元素\****，并且能够高效地***\*插入和删除\****容器的尾部元素。但它又与vector不同，***\*deque支持高效插入和删除容器的头部元素\****，因此也叫做*** 双端队列 ***

```python
from collections import deque

user = deque(["tf1", "tf2", "tf3", "tf4"])
user.appendleft("tf0")
print(user)
user.copy()  #浅拷贝
user.extend()  #扩容
```

**id()** 函数用于获取对象的内存地址。

Copy.deepcopy 深拷贝会完全复制生成一个新的

### Count

```python
from collections import Counter
# 可以统计list、tuple以及字符串
user = ["tf1", "tf2", "tf3", "tf4","tf4"]
user_count=Counter("abcksjskalwk")
print(user_count)

user_count.update("kkll")

```

heap堆数据结构



### OrderedDict

很多人认为python中的字典是无序的，因为它是按照hash来存储的，但是python中有个模块collections(英文，收集、集合)，里面自带了一个子类OrderedDict，实现了对字典对象中元素的排序。顺序为存入的顺序



```python
# -*- coding: utf-8 -*-
# @date: 2020/1/20 6:57 下午
# IDE  : PyCharm
# @name: order_dic.py
# @author：tfflyer
from collections import OrderedDict

dic_demo=OrderedDict()
dic_demo["A"]=0
dic_demo["c"]=1
dic_demo["b"]=2

# print(dic_demo.popitem())
print(dic_demo)

print(dic_demo.move_to_end("c"))
print(dic_demo)

```

### Chainmap

ChainMap将多个dict或其他映射组合在一起以创建单个可更新视图。[…] 查找基础映射，直到找到key为止。[…]如果其中一个基础映射得到更新，这些更改将反映在ChainMap中。 […] 支持所有常用的字典方法。

换句话说:**ChainMap是一个基于多dict的可更新的视图，它的行为就像一个普通的dict。**

```python
# -*- coding: utf-8 -*-
# @date: 2020/1/20 7:14 下午
# IDE  : PyCharm
# @name: chain_map.py
# @author：tfflyer
from collections import ChainMap
dic1 = {"a": 1, "b": 2, "c": 3}
dic2 = {"d": 4, "e": 5}
dic3 = ChainMap(dic1, dic2)
dic4=dic3.new_child({"f":7})
# 返回一个新的
print(dic3.maps)
print(dic4.maps)
for i, j in dic3.items():
    print(i, j)
# print(dic3)

```

next==》抽象基类
