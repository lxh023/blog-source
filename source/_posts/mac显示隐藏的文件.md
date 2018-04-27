---
title: mac显示隐藏的文件
date: 2018-04-27 13:17:43
tags:
- mac
categories:
- mac
permalink: mac-displays-hidden-files
---

## 快捷键方式

`Command` + `Shift` + `.` 可以显示隐藏文件、文件夹，再按一次，恢复隐藏

finder下使用 `Command` + `Shift` + `G` 可以前往任何文件夹，包括隐藏文件夹。

## 命令

显示隐藏文件

`defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder`

恢复隐藏文件隐藏状态

`defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finder`

