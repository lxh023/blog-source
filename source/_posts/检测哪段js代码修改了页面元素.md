---
title: 检测哪段js代码修改了页面元素(DOM断点调试)
date: 2017-08-28 22:30:35
tags:
- 调试技巧
categories:
- 前端开发
permalink: Check-which-JS-code-modifies-the-page-elements
---

# 开始

在开发中经常遇到这样的问题：

> 我想知道是哪段代码修改了这个div的颜色
> 我想知道我点击了这个东西后执行了哪里的代码

这时候改怎么办呢

假设现在有这样的一个页面

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title></title>
  </head>
  <body>
    <button id="btn">Button</button>
  </body>
  <script type="text/javascript">
    var btn = document.getElementById('btn')
      btn.onclick = function () {
      this.innerHTML = 'Hello'
    }
  </script>
</html>
```

显示在页面上是一个按钮，这个按钮在点击后会改变自身的显示文字

![](https://ws2.sinaimg.cn/large/006tNc79ly1fizth8gmbuj3042026mx2.jpg)

变为：

![](https://ws1.sinaimg.cn/large/006tNc79ly1fiztiatignj303m024a9y.jpg)

# 方法

首先按 `F12` 进入调试模式，切换到 `elements` 标签页，定位到按钮的代码部分

![](https://ws3.sinaimg.cn/large/006tNc79ly1fiztlt9u62j30t40pyaf5.jpg)

然后右键点击元素标签，可以看到最下面的 `Break on...` 选项，后面的三个功能分别是

- 子节点修改
- 自身属性修改
- 自身节点被删除

![](https://ws1.sinaimg.cn/large/006tNc79ly1fiztnkrnjrj30q00mojuv.jpg)

选中之后，Sources Panel 中右侧的 DOM Breakpoints 列表中就会出现该 DOM 断点。一旦执行到要对该 DOM 做相应修改时，代码就会在那里停下来，如下图所示

![](https://ws2.sinaimg.cn/large/006tNc79ly1fiztqh7kcpj31i614gqch.jpg)

这样就定位到了触发的JavaScript代码，可以进行下一步调试了