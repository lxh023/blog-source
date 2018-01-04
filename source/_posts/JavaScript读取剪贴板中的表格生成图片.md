---
title: JavaScript读取剪贴板中的表格生成图片
date: 2017-08-23 06:22:35
tags:
- 剪贴板
- Excel
- 表格
categories:
- JavaScript
permalink: JavaScript-reads-the-table-in-the-clipboard-and-generates-pictures
thumbnail: https://ws3.sinaimg.cn/large/006tNc79ly1fiujhqf2r8j30ok07sgor.jpg
---

# 演示地址

> 你可以访问下面的地址体验每个demo

[https://fairyever.github.io/excel-to-image-demo/](https://fairyever.github.io/excel-to-image-demo/)

# 需求

前些天公司要求做一个可以在输入框粘贴Excel表格的控件，也算是折腾了半天时间，写下来做个记录

> 具体效果可以参考京东客服聊天界面，在输入框粘贴表格后会生成图片发送出去

# 实现步骤

具体当时怎么栽的坑就不具体说了，下面只是系统的演示一遍步骤

以下演示都是在这样的一个输入框中进行：

![](https://ws4.sinaimg.cn/large/006tNc79ly1fitpm7zyuyj30dg09wq3a.jpg)

```
<div class="input-group ma-b-10">
    <span class="input-group-addon" id="basic-addon3">在这里粘贴Excel表格</span>
    <input ref="input" type="text" class="form-control" id="basic-url" aria-describedby="basic-addon3">
</div>
```

使用了 `VUE` 和 `bootstrap4` 以及 `HTML2canvas`

# 测试表格

![](https://ws1.sinaimg.cn/large/006tNc79ly1fitpwe8wagj30k20exta8.jpg)

# 测试环境

## windows

浏览器环境 Chrome | win10 in Parallels Desktop
![](https://ws4.sinaimg.cn/large/006tNc79ly1fitd0fx3wrj311w0nbmzz.jpg)

## mac

浏览器环境 Chrome | macOS Sierra 10.12.4
![](https://ws4.sinaimg.cn/large/006tNc79ly1fitcyvhwa2j30mr0krwgk.jpg)

# 剪贴板里有什么

## 代码

> 省略了部分不重要的内容

CDN库

```
<link rel="stylesheet" href="https://cdn.bootcss.com/bootstrap/4.0.0-beta/css/bootstrap.min.css" integrity="sha384-/Y6pD6FV/Vv2HJnA6t+vslU6fwYXjCFtcEpHbNJ0lyAFsXTsjBbfaDjzALeQsN6M" crossorigin="anonymous">
<script src="https://unpkg.com/vue"></script>
```

HTML

```
<div class="container" id="app">
	<h1>检查值类型</h1>
	<div class="input-group ma-b-10">
	  <span class="input-group-addon" id="basic-addon3">在这里粘贴Excel表格</span>
	  <input ref="input" type="text" class="form-control" id="basic-url" aria-describedby="basic-addon3">
	</div>
	<p><small>结果在控制台打印</small></p>
</div>
```

JavaScript

```
var vm = new Vue({
  el: '#app',
  mounted: function() {
    this.$refs.input.addEventListener("paste",
    function(e) {
      if (! (e.clipboardData && e.clipboardData.items)) {
        return;
      }
      for (var i = 0; i < e.clipboardData.items.length; i++) {
        console.log(e.clipboardData.items[i].type);
      }
    });
  }
```

## 结果

### mac

```
text/plain
text/html
text/rtf
image/png
```

### windows

```
text/plain
text/rtf
image/png
```

### 分析

可见在 `windows` 环境下，剪切板里的内容少了一个 `text/html`
为什么？
目前我也不知道。

# 检查获取到的实际值

## 代码

```
for (var i = 0; i < e.clipboardData.items.length; i++) {
	var item = e.clipboardData.items[i]
	if (item.kind === "string") {
		item.getAsString(function (str) {
			console.log(str);
		})
	}
}
```

## 结果

### text/plain

> 纯文本

```
姓名	年龄	职业	email 张三	20	不详	不详 李四	21	不详	不详 王五	22	不详	不详
```

### text/html

> HTML字符串

```
<html xmlns:v="urn:schemas-microsoft-com:vml"
xmlns:o="urn:schemas-microsoft-com:office:office"
xmlns:x="urn:schemas-microsoft-com:office:excel"
xmlns="http://www.w3.org/TR/REC-html40">

<head>
<meta http-equiv=Content-Type content="text/html; charset=utf-8">
<meta name=ProgId content=Excel.Sheet>
<meta name=Generator content="Microsoft Excel 15">
<link id=Main-File rel=Main-File
href="file://localhost/Users/liyang/Library/Group%20Containers/UBF8T346G9.Office/msoclip1/01/clip.htm">

... 省略 ...

 </tr>
 <tr height=35 style='mso-height-source:userset;height:26.0pt'>
  <td height=35 class=xl64 style='height:26.0pt;border-top:none'>王五</td>
  <td class=xl65 style='border-top:none;border-left:none'>22</td>
  <td class=xl65 style='border-top:none;border-left:none'>不详</td>
  <td class=xl65 style='border-top:none;border-left:none'>不详</td>
 </tr>
<!--EndFragment-->
</table>
</body>
</html>
```

### text/rtf

> 编码后的文本

```
{\rtf1\mac \ansicpg10008
{\fonttbl{\f0\fnil \fcharset134 ËÎÌå;}{\f1\fnil \fcharset134{\f16\fnil 
......
```

### image/png

> 在后面的测试中可以得到这是一个图片文件，但不是一个图片对象，更像文件选择得到的文件

```
// 控制台打印为空
```

# 尝试显示 text/html 类型的数据

## 代码

HTML

```
<div class="input-group ma-b-10">
  <span class="input-group-addon" id="basic-addon3">在这里粘贴Excel表格</span>
  <input ref="input" type="text" class="form-control" id="basic-url" aria-describedby="basic-addon3">
</div>
<div class="card ma-b-10">
	<div class="card-body">
		<h4 class="card-title">
			尝试使用<code>text/html</code>类型数据
		</h4>
		<h6 class="card-subtitle mb-2 text-muted">
			如果可以获取到数据，将会在这里显示结果
		</h6>
		<template v-if="tempData">
			<div class="form-group">
				<label for="exampleFormControlTextarea1">数据源码</label>
				<textarea
					class="form-control"
					id="exampleFormControlTextarea1"
					rows="3"
					v-model="tempData">
				</textarea>
			</div>
			<div ref="tempGroup" v-html="tempData"></div>    
		</template>
	</div>
</div>
```

JavaScript

```
var vm = new Vue({
	el: '#app',
	data: {
		tempData: ''
	},
	mounted: function () {
		var _this = this
		this.$refs.input.addEventListener("paste", function (e){
			if ( !(e.clipboardData && e.clipboardData.items) ) {
				return ;
			}
			if (e.clipboardData.items[1].type === 'text/html') {
				e.clipboardData.items[1].getAsString(function(str){
					_this.tempData = str
				})    
			}
		});
	}
})
```

## 结果

### mac

![](https://ws4.sinaimg.cn/large/006tNc79ly1fitqhzhaylj30os0jddit.jpg)

### windows

![](https://ws4.sinaimg.cn/large/006tNc79ly1fitqj2pqm2j311w0nbjtz.jpg)

### 结论

`text/html` 类型的数据在mac上是可用的（比如用在使用electron开发的macOS应用中），但是这不适用于windows平台

# 使用text/html类型的数据生成图片

更进一步，既然在mac上可以使用 `text/html` 类型的数据，那就尝试使用这个数据生成可以上传至服务器的图片资源

## 代码

新引入了一个库

```
<script src="https://cdn.bootcss.com/html2canvas/0.5.0-beta4/html2canvas.min.js"></script>
```

HTML比较长，请访问[仓库](https://github.com/FairyEver/excel-to-image-demo)查看源码

JavaScript关键部分

```
var _this = this
this.$refs.input.addEventListener("paste", function (e){
	if ( !(e.clipboardData && e.clipboardData.items) ) {
		return ;
	}
	if (e.clipboardData.items[1].type === 'text/html') {
		e.clipboardData.items[1].getAsString(function(str){
			_this.tempData = str
			Vue.nextTick(function(){
				html2canvas(_this.$refs.tempGroup, {
					onrendered: function(canvas) {
						_this.$refs.canvasGroup.appendChild(canvas)
						_this.base64 = canvas.toDataURL()
					}
				})    
			})
		})    
	}
})
```

## 结果(mac)

![](https://ws2.sinaimg.cn/large/006tNc79ly1fitqs3ebozj30sg0x3gr0.jpg)

到此为止在mac上一切顺利！，下面我们尝试使用mac和windows共有的数据类型进行解析

# 使用image/png类型的数据生成图片

##代码

注意，这种方式不需要 `html2canvas`

HTML比较长，请访问[仓库](https://github.com/FairyEver/excel-to-image-demo)查看源码

JavaScript关键部分

```
for (var i = 0; i < e.clipboardData.items.length; i++) {
	if (e.clipboardData.items[i].type === 'image/png'){
		var pasteFile = e.clipboardData.items[i].getAsFile();
		var reader = new FileReader();
		reader.readAsDataURL(pasteFile);  
		reader.onload=function(e){
			_this.base64 = this.result;
		}
	}
}
```

## 结果

### mac

![](https://ws1.sinaimg.cn/large/006tNc79ly1fitqvak5fhj30nq0ivad5.jpg)

### windows

![](https://ws2.sinaimg.cn/large/006tNc79ly1fitqxi1og2j311w0nbae3.jpg)

# 总结

使用 `image/png` 数据是可行的，而且这种方式相较于 `html2canvas` 还有一个优点就是即使表格尺寸超过了一屏的大小(宽度和高度都可以)，仍然可以很好的生成base64图片

所有源码请移至[仓库](https://github.com/FairyEver/excel-to-image-demo)

end
