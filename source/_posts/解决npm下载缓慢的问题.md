---
title: 解决npm下载缓慢的问题
date: 2018-04-27 13:27:43
tags:
- nrm
- npm
- Node.js
categories:
- Node.js
permalink: solve-the-problem-of-slow-download-of-npm
---

> 不建议使用 `cnpm`，可能会导致意想不到的bug

这里介绍如何使用 `nrm` 快速切换你的 `npm` 源

[https://github.com/Pana/nrm](https://github.com/Pana/nrm)

## 安装

```
$ npm install -g nrm
```

## 检查所有的可用源

```
$ nrm ls

* npm ---- https://registry.npmjs.org/
  cnpm --- http://r.cnpmjs.org/
  eu ----- http://registry.npmjs.eu/
  au ----- http://registry.npmjs.org.au/
  sl ----- http://npm.strongloop.com/
  nj ----- https://registry.nodejitsu.com/
```

# 切换源

```
$ nrm use cnpm //switch registry to cnpm
```

![](http://fairyever.qiniudn.com/15248077016960.jpg)

## 查看当前的源

```
nrm current
```

![](http://fairyever.qiniudn.com/15248077829234.jpg)

