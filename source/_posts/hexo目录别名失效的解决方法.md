---
title: hexo目录别名失效的解决方法
date: 2017-08-29 20:29:44
tags:
- hexo
categories:
- hexo
permalink: Hexo-directory-alias-invalid-solution
---

突然发现hexo的目录别名失效了，多次尝试后找到了新的写法，文件结构见下图：

![](https://ws1.sinaimg.cn/large/006tKfTcly1fj0vkgsdabj308c0hamy0.jpg)

需要引入组件的页面是pages目录下的index.vue，各种写法见代码

按照官方文档中写的别名应该是这样引入，但是会报错

```
import navTop from '~components/nav/top/top.vue'
```

目前可以成功引入的写法,但是和官方文档不一致

```
import navTop from '~/components/nav/top/top.vue'
```

这样写也是可以的

```
import navTop from './../components/nav/top/top.vue'
```

还不知道为什么会这样，在之前确实是可以像 `~components` 这种写法的，暂时只有写成 `~/components` 解决
