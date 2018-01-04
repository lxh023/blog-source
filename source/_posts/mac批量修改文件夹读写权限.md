---
title: mac批量修改文件夹读写权限
date: 2017-08-21 09:28:21
tags:
- mac
- 权限
categories:
- mac
permalink: 'mac-batch-modify-folder-read-and-write-permissions'
---

# 问题

最近发现很多文件的权限默认都是只读(为什么在我的用户下面我竟然默认只有只读权限？)，笨办法只能哪个文件报告没有权限了就去设置一下：

![](https://ws2.sinaimg.cn/large/006tNc79ly1fir3i58fm3j30d40ebwfa.jpg)

![](https://ws3.sinaimg.cn/large/006tNc79ly1fir3knyst4j307805xt8s.jpg)

# 解决办法

```
sudo chmod -R 777 文件夹
```

例如：

```
code sudo chmod -R 777 blog
```