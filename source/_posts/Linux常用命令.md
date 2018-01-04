---
title: Linux常用命令
date: 2017-09-13 21:13:15
tags:
- Linux
categories:
- Linux
permalink: Linux-common-commands
---

> 记录用到过的Linux命令

# 文件删除

删除文件夹
```
rm -rf [文件夹名称]
```

删除文件
```
rm -f [文件名称]
```

# 端口

查看所有端口
```
netstat -ntlp
```

查看所有nginx的端口
```
ps -ef|grep nginx
```