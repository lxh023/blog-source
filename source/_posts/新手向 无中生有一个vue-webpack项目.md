---
title: 新手向 无中生有一个vue-webpack项目
date: 2018-04-19 12:00:00
tags:
- js
- vue
categories:
- JavaScript
permalink: how-to-create-a-vue-webpack-project
---

> 北京沃德博创科技有限公司内部分享使用文档

本文面向对象是简单接触过 vue 开发，但是没有从头搭建过项目的开发者
[]()
假设你已经有 HTML CSS JavaScript 基础，并且可以看懂 [JavaScript ES6](http://es6.ruanyifeng.com/) 的大部分语法

本文主要分为以下部分

* 开始一个 vue.js 项目
* 删除初始项目中无用的部分
* 设置路由
* 写第一个组件
* 加入一个 UI 组件库
* 使用 vuex
* 使用一个 vue 插件
* 使用一个非 vue 插件
* vue-dev-tool
* 编辑器插件
* vue 生态总览

在本文中对于每个部分不做多余赘述，只展示必要代码

## 开始一个 vue.js 项目

[示例代码地址 Github](https://github.com/FairyEver/wdbc-vue-demo)

使用 vue-cli 初始化 webpack 项目

![](http://fairyever.qiniudn.com/15241330610541.jpg)

完成后项目结构如下

![](http://fairyever.qiniudn.com/15241331928690.jpg)

安装依赖

```
cnpm install
```

![](http://fairyever.qiniudn.com/15241332859800.jpg)

启动热更新开发

```
npm run dev
```

![](http://fairyever.qiniudn.com/15241334919000.jpg)

出现 `Your application is running here: http://localhost:8080` 表示成功，你的项目在 8080 运行

![](http://fairyever.qiniudn.com/15241335757296.jpg)

截止到这里 [Git分支地址 master](https://github.com/FairyEver/wdbc-vue-demo/tree/master)

相关链接

[vue命令行工具 (CLI)](https://cn.vuejs.org/v2/guide/installation.html#%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%B7%A5%E5%85%B7-CLI)

> CLI 工具假定用户对 Node.js 和相关构建工具有一定程度的了解

## 删除初始项目中无用的部分

* 删除了首页图片
* 修改了 app.vue 中的样式
* 删除了 `src/components/HelloWorld.vue` 中无用代码和样式

现在页面看起来是这样的，没有了多余的东西

![](http://fairyever.qiniudn.com/15241348228075.jpg)

截止到这里 [Git分支地址 remove-redundant-code](https://github.com/FairyEver/wdbc-vue-demo/tree/remove-redundant-code)

## 设置路由

见项目代码 router 分支

![](http://fairyever.qiniudn.com/15241368109779.jpg)

demo 演示了基本路由配置，动态匹配路由，路由嵌套，和编程式导航，更多内容请自行查阅文档 [router.vuejs.org](https://router.vuejs.org/zh-cn/)

截止到这里 [Git分支地址 router](https://github.com/FairyEver/wdbc-vue-demo/tree/router)

## 写第一个组件

见项目代码 component 分支

![](http://fairyever.qiniudn.com/15241377842419.jpg)

page5 的简单示意图

![IMG_0933](http://fairyever.qiniudn.com/IMG_0933.jpg)

截止到这里 [Git分支地址 component](https://github.com/FairyEver/wdbc-vue-demo/tree/component)

## 加入一个 UI 组件库

vue.js 不和任何旧的 CSS 组件库冲突，并且可以使用大量的专用组件库，比如常见的 [element](http://element.eleme.io/#/zh-CN) 和 [iview](https://www.iviewui.com/)

```
cnpm install element-ui --save
```

在 `src/main.js` 添加

```
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(ElementUI)
```

![](http://fairyever.qiniudn.com/15241383166878.jpg)

截止到这里 [Git分支地址 element](https://github.com/FairyEver/wdbc-vue-demo/tree/element)

## vuex

[vuex.vuejs.org](https://vuex.vuejs.org/zh-cn/)

![](http://fairyever.qiniudn.com/15241392248302.jpg)

示意图

![IMG_0935](http://fairyever.qiniudn.com/IMG_0935.jpg)

截止到这里 [Git分支地址 vuex](https://github.com/FairyEver/wdbc-vue-demo/tree/vuex)

## 使用一个 vue 插件

插件 [effect-input](https://www.awesomes.cn/repo/XBT1/effect-input) ，选这个插件没有什么原因，随意选的

安装

```
cnpm install effect-input --save
```

注册

```
import EffectInput from 'effect-input'
import 'effect-input/dist/index.css'
Vue.use(EffectInput)
```

使用

```
<EffectInput v-model="value" type="haruki" label="姓名"></EffectInput>
```

![](http://fairyever.qiniudn.com/15241400354449.jpg)

截止到这里 [Git分支地址 vue-plugin](https://github.com/FairyEver/wdbc-vue-demo/tree/vue-plugin)

## 使用一个非 vue 插件

演示一个提示框插件 [sweetalert.js](https://sweetalert.js.org/)，这个插件和 vue 没有一点关系，是一个原生 JS 弹出框插件

```
cnpm install sweetalert --save
```

![](http://fairyever.qiniudn.com/15241406592869.jpg)

截止到这里 [Git分支地址 js-plugin](https://github.com/FairyEver/wdbc-vue-demo/tree/js-plugin)

## vue-dev-tool

![IMG_0949](http://fairyever.qiniudn.com/IMG_0949.jpg)

更改组件数据

![vue-dev-tool-demo-1](http://fairyever.qiniudn.com/vue-dev-tool-demo-1.gif)

## 编辑器插件

![Snip20180420_1](http://fairyever.qiniudn.com/Snip20180420_1.png)

效果

![Snip20180420_3](http://fairyever.qiniudn.com/Snip20180420_3.png)

> 另外推荐一款字体 [FiraCode](https://github.com/tonsky/FiraCode)，这是一个专门用来优化代码中符号显示的字体
> ![all_ligatures](http://fairyever.qiniudn.com/all_ligatures.png)


## vue 生态总览

![Vue生态概述0.2](http://fairyever.qiniudn.com/Vue生态概述0.2.png)

下面是一些 awesome

[首推！Github 千人贡献 30K+ star 的 vue-awesome](https://github.com/vuejs/awesome-vue)

[vue生态大指南](https://www.vue-js.com/topic/58750c15a9c1282817afbfb7)

[awesomes.cn vue专题](https://www.awesomes.cn/subject/vue)

> 这种东西网上很多，随便找找一大堆

## Q&A

**2018年应该怎样学习 web/JS**

我个人的建议是这样的顺序

1. HTML > CSS > JavaScript 依次学习，重要性递增
2. 学习 jQuery
3. 相关 IDE 了解 `Atom` `VScode`
4. 学会一款设计软件 `Sketch` `PS`
5. 了解 SCSS LESS，提高 CSS 水平
6. 学习 JavaScript ES6 ES7
7. 学习 node.js
8. 了解包管理工具 npm 和 yarn，了解 webpack，了解 Babel
9. `vue.js` `react.js` `angularJS` 三者任选其一先学会，必要的话最好首先掌握 `vue.js` `react.js`
10. 其它(JS)方向：微信小程序, RN开发移动端，浏览器插件, node.js服务端, 自动化测试，爬虫，Electron，数据可视化，2D3D游戏开发等

在现在的前端环境下，CSS的地位变的不太重要，JS蒸蒸日上，上面步骤中的 6 7 9 是最重要的

<img src="http://fairyever.qiniudn.com/v2-4858866498020973da9988c7bb98e6b6_hd.jpg" style="height: 100px;"/>

**END**

