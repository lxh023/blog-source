---
title: Laya学习笔记 显示文本
date: 2017-08-22 09:05:11
tags:
- LayaAir
categories:
- LayaAir
permalink: 'laya-air-01-show-text'
---

# 新建文件

![](https://ws1.sinaimg.cn/large/006tKfTcly1fis8f55gptj30830bcaah.jpg)

# 代码

```
//创建舞台，默认背景色是黑色的
Laya.init(600, 300); 
var txt = new Laya.Text(); 
//设置文本内容
txt.text = "Hello World";  
//设置文本颜色
txt.color = "#333333";
//设置文本字体大小，单位是像素
txt.fontSize = 66;  
//设置字体描边
txt.stroke = 5;//描边为5像素
txt.strokeColor = "#FFFFFF";  
//设置为粗体
txt.bold = true;  
//设置文本的显示起点位置X,Y
txt.pos(60,100);
//设置舞台背景色
Laya.stage.bgColor  = '#333333';
//将文本内容添加到舞台 
Laya.stage.addChild(txt);
```

# 运行

![](https://ws2.sinaimg.cn/large/006tKfTcly1fis8inoxxpj30kn0d03z3.jpg)

# 文字居中

设置文字区域尺寸后设置对齐方式

```
txt.width = 600;
txt.height = 300;
txt.align = 'center';
txt.valign = 'middle';
```
