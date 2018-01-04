---
title: node.js利用子进程调用系统命令
date: 2017-09-14 14:31:28
tags:
- Node.js
categories:
- Node.js
permalink: Node.js-uses-child-processes-to-invoke-system-commands
---

需要为 `nuxt` 项目做 `pm2` 进程守护，但是没有找到 `nuxt` 项目的入口文件，所以想到了再新建一个文件做为入口文件，在这个文件内执行 `npm run start` 达到相同的效果

```
var spawn = require('child_process').spawn
let start = spawn('npm', ['run', 'start'])

// 捕获标准输出
start.stdout.on('data', function (data) {
  console.log('[output]:\n' + data)
})
// 捕获标准错误
start.stderr.on('data', function (data) {
  console.log('[error output]:\n' + data)
})
// 注册子进程关闭事件
start.on('exit', function (code, signal) {
  console.log('[child process eixt] ,exit:' + code)
})
```

在服务器上执行 `pm2 start app.js` 即可
