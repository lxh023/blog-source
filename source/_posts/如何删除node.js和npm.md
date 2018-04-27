---
title: 如何删除node.js和npm
date: 2018-04-27 15:00:00
tags:
- electron
categories:
- electron
permalink: remove-nodejs-and-npm
---

## 官网下载pkg安装包的

一条命令 

```
sudo rm -rf /usr/local/{bin/{node,npm},lib/node_modules/npm,lib/node,share/man/*/node.*}
```

## 其他路子安装的

搞一个脚本，把需要删除的文件，一梭子全干掉

内容如下，命名为：uninstallnode.sh

```
#!/bin/bash
lsbom -f -l -s -pf /var/db/receipts/org.nodejs.pkg.bom \
| while read i; do
  sudo rm /usr/local/${i}
done
sudo rm -rf /usr/local/lib/node \
     /usr/local/lib/node_modules \
     /var/db/receipts/org.nodejs.*
```

修改文件权限 

```
chmod 777 uninstallNodejs.sh 
```

在命令行执行

## Tips

这些东西删完了，node就算删除了。 
但是还有好多基于node安装的一堆软件和命令行工具，也需要重新安装，例如 react-native, supervisor,pm2 etc 
需要删除/usr/local/bin 下面相关的文件，其实它们只是些软连接，正主都在 /usr/local/lib/node_modules/ 目录下