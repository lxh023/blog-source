---
title: JavaScript 数组空位
date: 2017-11-27 19:34:43
tags:
- 空位
- js
- js基础
- 数组
- 等差数列
categories:
- JavaScript
permalink: 'js-array-empty'
---

注 本文所有的代码的前提是

```
let a = 3
let b = 9
```

并且示例代码都会return结果数组

# 问题

前几天一个朋友问的问题

> 已知数组的起始数字，生成一个公差为1的等差数列

# 基础方法

题目很简单，最简单的办法就是使用for循环

```
let arr = []
for (let i = 0; i < b - a + 1; i++) {
  arr.push(i + a)
}
return arr
```

# 进阶

这个很平常的题目之后再想起来时感觉之前的方法有点愚蠢，遂有想出以下办法，顺便标注所涉及的知识点

## 数组空位

> 数组的空位指，数组的某一个位置没有任何值，最简单我们可以使用Array构造函数来生成它，需要注意的是forEach(), filter(), every() 和some()都会跳过空位，也就代表你没有办法使用上述方法遍历到空位；map()也会跳过空位，但是依然会在返回的新数组里保留这个值；join()和toString()会将空位视为undefined(字符串形式)。

下面是一些方法实现同样的功能：

```
// 拼接 > 分割 > map
Array(b - a + 1).join(' ').split(' ').map((e, i) => a + i)

// 转字符串 > 分割 > map
Array(b - a + 1).toString().split(',').map((e, i) => a + i)
```

> Array.from方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）。

利用Array.from方法实现：

```
// 空数组转真数组
Array.from(Array(b - a + 1)).map((e, i) => a + i)

// 类似数组的对象转数组
Array.from({ length: b - a + 1 }).map((e, i) => a + i)
Array.from({ length: b - a + 1 }, (e, i) => a + i)
```

ES6的扩展运算符还可以帮我们更方便地完成这件事

```
[...Array(b - a + 1)].map((e, i) => a + i)
```

fill()、entries()、keys()方法也不会忽略空位

```
Array(b - a + 1).fill(' ').map((e, i) => a + i)
[...Array(b - a + 1).entries()].map(e => e[0] + a)
[...Array(b - a + 1).keys()].map(e => e + a)
```

还有其他的途径可以完成这件事，比如findIndex()、find()、for...of等，这几个方法实现起来也不够简单，就不多余赘述了