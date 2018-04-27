---
title: 解决electron使用packager打包下载缓慢问题
date: 2018-04-27 13:37:00
tags:
- electron
categories:
- electron
permalink: solve-electron-slow-download-problem-with-packager-package
---

解决方法很简单，将你之前的打包命令比如

```
npm run packager
```

修改为

```
ELECTRON_MIRROR=https://npm.taobao.org/mirrors/electron/ npm run packager
```

即可使用淘宝的源，速度立马提升～

