---
layout: post
title: "一些关于词典和背单词的项目记录"
date: 2013-09-21 20:46
comments: true
categories: [shell, dictionary, java]
---
几个月前换上了Linux，感觉不错:), 就是星际词霸怎么排版有点怪？而且单词本的也没有…其实主要是希望能有`柯林斯词典`

呵呵，没办法，不习惯每次都要打开浏览器，然后点击有道词典的链接，然后输入单词…  
所以我就决定写个脚本来帮我做这些事情，项目位于：[YoudaoDict][]，有需要的朋友可以*clone*并使用

### YoudaoDict
YoudaoDict，名副其实，就是通过有道词典来查单词，支持且仅支持`柯林斯词典`
### Features
-  查询单词在柯林斯词典中的释义
-  美式发音和英式发音
-  加入单词本（脚本支持，需要自定义相关脚本中的变量）
-  导出`tab`分隔符的单词本数据（可以导入到Anki这样的卡片工具中，配合复习，非常好用）
<!--more-->
### Installation
-  将项目Clone到本地
```bash
git clone git@github.com:rankun203/YoudaoDict.git
```
-  用maven构建项目
```bash
cd YoudaoDict/YoudaoDict
mvn package
```
未完待续---


[YoudaoDict]: https://github.com/rankun203/YoudaoDict
