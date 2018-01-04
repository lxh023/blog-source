---
title: Python3学习笔记
date: 2017-10-2 11:54:31
tags:
- Python3
categories:
- Python3
permalink: Python3-learning-notes-01-get-started
---

# 基础

## 直接运行py文件

首先在.py文件的开头加上，以`hello.py`为例

```python
#!/usr/bin/env python3
```

然后通过命令给予权限

```
chmod a+x hello.py
```

获取输入

```python
name = input()
name2 = input('输入你的名字')
print('你好', name2)
```

转义

```python
print('A\nB')
# A
# B

print('A\\nB')
# A\nB

print(r'A\nB')
# A\nB
```

## 显示多行内容

```python
print('''
第一行
第二行
第三行
''')
# 第一行
# 第二行
# 第三行

print('''
A\tB
A\nB
''')
# A       B
# A
# B

print(r'''
A\tB
A\nB
''')
# A\tB
# A\nB
```

## 常量

常量一般用全大写的字母表示

```python
PI = 3.14159265359
```

## 除法

```python
print(10 / 3)
# 3.3333333333333335

print(10 // 3)
# 3 称为地板除

print(10 % 3)
# 1
```

## 通常在头部增加的信息

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释；

第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。

申明了UTF-8编码并不意味着你的.py文件就是UTF-8编码的，必须并且要确保文本编辑器正在使用UTF-8 without BOM编码

## 格式化

```python
str = '亲爱的%s您好，您%d月的话费为%f元' % ('李杨', 3, 12.34)
print(str)
# 亲爱的李杨您好，您3月的话费为12.340000元

str = '亲爱的%s您好，您%d月的话费为%.2f元' % ('李杨', 3, 12.34)
print(str)
# 亲爱的李杨您好，您3月的话费为12.34元
```

| 占位符 | 含义 |
| --- | --- |
| %d | 整数 |
| %f | 浮点数 |
| %s | 字符串 |
| %x | 十六进制整数 |

数字格式化

```python
print('%2d和%02d' % (6, 6))
#  6和06
print('%d和%04d' % (6, 6))
# 6和0006

print('%f' % 3.123456789)
# 3.123457
print('%.2f' % 3.123456789)
# 3.12
```

转义百分号使用%%

```python
print('%s哈哈哈%%' % '嘻嘻嘻')
# 嘻嘻嘻哈哈哈%
```

## 数组基础

```python
people = ['AAA', 'BBB', 'CCC']
print(people)
print(len(people))
print(people[0])
print(people[1])
print(people[-1])
print(people[-2])
# ['AAA', 'BBB', 'CCC']
# 3
# AAA
# BBB
# CCC
# BBB
```

## 数组操作

```python
array = ['AAA', 'BBB', 'CCC', 'DDD']

# 在末尾追加
array.append('2333')
print(array)
# ['AAA', 'BBB', 'CCC', 'DDD', '2333']

# 插入到指定位置
array.insert(1, 'new!!!')
print(array)
# ['AAA', 'new!!!', 'BBB', 'CCC', 'DDD']

# 删除末尾
array.pop()
print(array)
# ['AAA', 'BBB', 'CCC']

# 删除指定位置
array.pop(1)
print(array)
# ['AAA', 'CCC', 'DDD']
```

## tuple

tuple和list非常类似，但是tuple一旦初始化就不能修改

```python
demoTuple = ('AAA', 'BBB', 'CCC')
print(demoTuple[0])
print(demoTuple[-1])
print(demoTuple)
# AAA
# CCC
# ('AAA', 'BBB', 'CCC')
```

如果定义只有一个元素的tuple，因为()还可以表示数学中的括号，所以需要多加一个逗号

```python
emptyTuple = ()
print(emptyTuple)
# ()

onlyOneTuple = (1)
print(onlyOneTuple)
# 1

onlyOneTuple2 = (1,)
print(onlyOneTuple2)
# (1,)
```

Python在显示只有1个元素的tuple时，也会加一个逗号,，以免你误解成数学计算意义上的括号

但是当tuple中的某个元素是数组的话，去改变了数组某个项目的值，tuple的值也会发生变化

```python
t = ('a', 'b', ['A', 'B'])
t[2][0] = 'X'
t[2][1] = 'Y'
print(t)
# ('a', 'b', ['X', 'Y'])
```

> 表面上看，tuple的元素确实变了，但其实变的不是tuple的元素，而是list的元素。tuple一开始指向的list并没有改成别的list，所以，tuple所谓的“不变”是说，tuple的每个元素，指向永远不变。即指向'a'，就不能改成指向'b'，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！

## for

```python
for ele in [1, 2, 3, 4, 5]:
  print(ele)
# 1
# 2
# 3
# 4
# 5

print(list(range(5)))
# [0, 1, 2, 3, 4]
```

## while

```python
sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)
```

在循环内部变量n不断自减，直到变为-1时，不再满足while条件，循环退出

## dict

dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度

```python
demo = {
  'A': '000',
  'B': '111',
  'C': '222'
}
print(demo['A'])
# 000
print(demo['C'])
# 222

# 检查字典里是否有这个项目
print('D' in demo)
# False

# 取值 可以附加取值失败时的返回值
print(demo.get('D'))
print(demo.get('D', '00000'))
# None
# 00000

# 删除元素
demo.pop('B')
print(demo)
# {'A': '000', 'C': '222'}
```

## set

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key

```python
s = set([1, 2, 3, 4, 4, 5, 1, 2, 6])
print(s)
# {1, 2, 3, 4, 5, 6}

s.add('HELLO')
print(s)
# {1, 2, 3, 4, 5, 6, 'HELLO'}

s.remove(4)
print(s)
# {1, 2, 3, 5, 6, 'HELLO'}
```

# 函数

## 基础

```python
def demo():
  return 'hello'

print(demo())
# hello

def sayHello():
  name = input('your name?')
  print('hello,%s上午好' % name)

sayHello()
# your name?liyang
# hello,liyang上午好
```

没有返回值的情况

```python
def noReturn():
  a = 'A'
test = noReturn()
print(test)
# None
# 没有返回值的函数会返回None
```

## 函数带参数

```python
def demo(name):
  return name + '123'
print(demo('liyang'))
# liyang123
```

另一个例子

```python
def power(num, count):
  res = 1
  while count > 0:
    count = count -1
    res = res * num
  return res
print(power(10, 2))
# 100
```

## 设置默认参数

```python
def demo(name = 'liyang'):
  return name + ' Hello'
print(demo())
print(demo('ban'))
# liyang Hello
# ban Hello
```

默认参数的坑

```python
def appendDemo(a = []):
  a.append('Hello')
  # return a.append('Hello') 竟然不可以
  return a
print(appendDemo())
# ['Hello']
print(appendDemo())
# ['Hello', 'Hello']
print(appendDemo())
# ['Hello', 'Hello', 'Hello']
```

> Python函数在定义的时候，默认参数L的值就被计算出来了，即[]，因为默认参数L也是一个变量，它指向对象[]，每次调用该函数，如果改变了L的内容，则下次调用时，默认参数的内容就变了，不再是函数定义时的[]了。

所以，定义默认参数要牢记一点：默认参数必须指向不变对象！

上面函数的改进方法

```python
def appendDemo2(a = None):
  if a is None:
    a = []
  a.append('Hello')
  return a
print(appendDemo2())
# ['Hello']
print(appendDemo2())
# ['Hello']
print(appendDemo2())
# ['Hello']
```

## 可变参数

```python
def demo(*nums):
  res = 0
  for num in nums:
    res = res + num
  return res
print(demo(1, 2, 3, 4, 5))
# 15
print(demo(11, 12, 13, 14, 15))
# 65

props = [111, 222, 333, 444, 555]
print(demo(*props))
# 1665
```

在一个参数前面加上`*`即变为可变参数，将一个数组或者tuple作为参数传递给可变参函数只需要在前面加上`*`

## 关键字参数

```python
def demo(name, age, **other):
  print(name)
  print(age)
  print(other)
demo('liyang', 24, a = 'Hello', b = 'Hi')
# liyang
# 24
# {'a': 'Hello', 'b': 'Hi'}
```

上面的调用方式可以使用简化写法

```python
dic = {
  'a':'Hello',
  'b':'Hi'
}
demo('liyang', 24, **dic)
# liyang
# 24
# {'b': 'Hi', 'a': 'Hello'}
```

在实际使用中，如果要检查关键字参数中是否有某个参数，要像这样检查：

```python
def demo(name, age, **info):
  if 'a' in info:
    print('a is in info')
  if 'b' in info:
    print('b is in info')
  print(name)
  print(age)
  print(info)

demo('liyang', 24, a = 'AAA', b = 'BBB', c = 'CCC')
# a is in info
# b is in info
# liyang
# 24
# {'b': 'BBB', 'c': 'CCC', 'a': 'AAA'}
demo('liyang', 24, a = 'AAA', c = 'CCC')
# a is in info
# liyang
# 24
# {'c': 'CCC', 'a': 'AAA'}
```

为了解决这个问题，可以使用命名的关键字参数

```python
def demo(name, age, *, a, b):
  print(name)
  print(age)
  print(a)
  print(b)

demo('liyang', 24, a = 'AAA', b = 'BBB')
# liyang
# 24
# AAA
# BBB
```

和关键字参数`**kw`不同，命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数

如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符*了，像下面这样

```python
def demo(name, age, *info, a, b):
  print(name)
  print(age)
  print(info)
  print(a)
  print(b)
arr = [1, 2, 3]
demo('liyang', 24, *arr, a = 'AAA', b = 'BBB')
# liyang
# 24
# (1, 2, 3)
# AAA
# BBB
```

## 函数的混合使用

```python
def f(a, b, c = 1, *d, **e):
  print('a = ', a)
  print('b = ', b)
  print('c = ', c)
  print('d = ', d)
  print('e = ', e)
f(1, 2, 3, 4, 5, 6, aa = 'AA', bb = 'BB')
# a =  1
# b =  2
# c =  3
# d =  (4, 5, 6)
# e =  {'aa': 'AA', 'bb': 'BB'}
f(1, 2, *(3, 4, 5, 6), aa = 'AA', bb = 'BB')
# a =  1
# b =  2
# c =  3
# d =  (4, 5, 6)
# e =  {'aa': 'AA', 'bb': 'BB'}
f(1, 2, aa = 'AA', bb = 'BB')
# a =  1
# b =  2
# c =  1
# d =  ()
# e =  {'bb': 'BB', 'aa': 'AA'}
```

所以，对于任意函数，都可以通过类似`func(*args, **kw)`的形式调用它，无论它的参数是如何定义的

## 递归函数

```python
def f(n):
  if n == 1:
    return 1
  return n * f(n - 1)
print(f(10))
# 3628800
```

使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（`stack`）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。

```python
print(f(1000))
# RecursionError: maximum recursion depth exceeded in comparison
```

解决递归调用栈溢出的方法是通过尾递归优化，事实上尾递归和循环的效果是一样的，所以，把循环看成是一种特殊的尾递归函数也是可以的。

尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。

对上面的例子进行尾递归优化

```python
def f2(n):
  return f2inner(n, 1)
def f2inner(num, res):
  if(num == 1):
    return res
  return f2inner(num - 1, num * res)
print(f2(10))
# 3628800
```

```python
print(f(1000))
# RecursionError: maximum recursion depth exceeded in comparison
```

尾递归调用时，如果做了优化，栈不会增长，因此，无论多少次调用也不会导致栈溢出。

遗憾的是，大多数编程语言没有针对尾递归做优化，Python解释器也没有做优化，所以，即使把上面的fact(n)函数改成尾递归方式，也会导致栈溢出。

也就是说没有用，任何递归函数都存在栈溢出的问题。

