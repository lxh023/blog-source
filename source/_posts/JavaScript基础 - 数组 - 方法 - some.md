---
title: JavaScript some函数
date: 2017-08-20 22:44:01
tags:
- some()
- js
- js基础
- 数组
categories:
- JavaScript
permalink: 'js-base-some'
---

在vue-router的官方文档中，有这样一段代码：

```
router.beforeEach((to, from, next) => {
  if (to.matched.some(record => record.meta.requiresAuth)) {
    // this route requires auth, check if logged in
    // if not, redirect to login page.
    if (!auth.loggedIn()) {
      next({
        path: '/login',
        query: { redirect: to.fullPath }
      })
    } else {
      next()
    }
  } else {
    next() // 确保一定要调用 next()
  }
})
```

> 一个路由匹配到的所有路由记录会暴露为 $route 对象（还有在导航钩子中的 route 对象）的 $route.matched 数组。因此，我们需要遍历 $route.matched 来检查路由记录中的 meta 字段。

今天关注的不是这段代码的含义，而是 `to.matched.some(record => record.meta.requiresAuth)` 中的 `.some方法`

# 概述
some() 方法测试数组中的某些元素是否通过了指定函数的测试。

# 语法
arr.some(callback[, thisArg])

# 参数
`callback` 用来测试每个元素的函数
`thisArg` 执行 `callback` 时使用的 `this` 值

# 描述
some 为数组中的每一个元素执行一次 callback 函数，直到找到一个使得 callback 返回一个“真值”（即可转换为布尔值 true 的值）。如果找到了这样一个值，some 将会立即返回 true。否则，some 返回 false。callback 只会在那些”有值“的索引上被调用，不会在那些被删除或从来未被赋值的索引上调用。

callback 被调用时传入三个参数：元素的值，元素的索引，被遍历的数组。

如果为 some 提供了一个 thisArg 参数，将会把它传给被调用的 callback，作为 this 值。否则，在非严格模式下将会是全局对象，严格模式下是 undefined。

some 被调用时不会改变数组。

some 遍历的元素的范围在第一次调用 callback. 时就已经确定了。在调用 some 后被添加到数组中的值不会被 callback 访问到。如果数组中存在且还未被访问到的元素被 callback 改变了，则其传递给 callback 的值是 some 访问到它那一刻的值。

> some( ) 不会对空数组进行检测。
> some( ) 不会改变原始数组。

# 示例

## 回调函数接收的参数

```
function test1(element,index,array){
    console.log(element);
    console.log(index);
    console.log(array);
}
var return1 = [1,2,3].some(test1);
console.log(return1);

// 1
// 0
// Array[5]
// 2
// 1
// Array[5]
// 3
// 2
// false
```

## 检查数组

```
// 检查是否有大于2的元素
function test(ele){
    if(ele > 2){
        return true;
    }
    else{
        return false;
    }
}

console.log([0,1].some(test)); //false
console.log([0,1,2].some(test)); //false
console.log([0,1,2,3].some(test)); //true
```

## 有返回值为true时就不会继续执行

```
// 检查是否有大于2的元素
function test(ele){
    if(ele > 2){
        console.log(ele);
        return true;
    }
    else{
        console.log(ele);
        return false;
    }
}

console.log([0,1,2,3,4,5,6,7,8].some(test)); //0 1 2 3 true
```