---
layout: post
title: "为Octopress的Greyshade主题添加QQ空间的链接"
date: 2013-09-21 16:53
comments: true
categories:
- Programming
- Octopress
tags:
- Octopress
- github
---

其实做这个之前我想过有没有必要，因为编程社区会不会有必要访问`QQ空间`还说不定——不过后来我想，其实我的大多数社交活动还是在`QQ空间`上，`Facebook`和`Google+`都上的不多，主要是现在还没贡献多少，在开源界的人缘还没积累起来。

好，废话少说，看过程，该方法适用于任一链接，可以添加任意链接。
<!--more-->
### 显示效果
![链接显示效果](/images/2013-09-21-setupqzoneforoctopress/1.png)
### 准备工作
需要准备一个`20x20`的链接图标，最好是跟`Greyshade`图标风格相符的，这个自己画也画不了多久，我画的图标有锯齿问题，也没查到怎么在`GIMP`里面消除锯齿，就这样了。
### 修改页面
用编辑器打开`octopress/.themes/greyshade/source/_includes/header.html`，看到里面的一堆判断了吧，复制一个差不多的，改改，貌似这样(注意`{`和`%`之间本不该有空格, 此处时为了让Liquid忽略它)：

    { % if site.qq_user %}
    <a class="qzone" href="http://{{ site.qq_user }}.qzone.qq.com" title="Qzone">Qzone</a>
    { % endif %}
### 修改样式
用编辑器打开`octopress/.themes/greyshade/sass/parts/_header.scss`，找到`#sub-nav.social`在`facebook`附近添加一个自己的样式，比如说这样：
```sass
&.qzone{
	background: image-url('social/qzone.png') center no-repeat #50803f;
	border: 1px solid #50803f;
	&:hover{
		border: 1px solid darken(#50803f, 10%);
	}
}
```

好，修改就差不多了，把资源文件放进去，这里指的就是我们的小图标
### 拷贝资源
将`图标.xxx`放到`octopress/.themes/greyshade/source/images/social/`目录下面。

这样，所有的资源就齐了。

如果现在进行preview的话，肯定还是看不到效果的，需要手动编译一些资源文件，比如`sass`等
### 更新资源
运行命令
```bash
rake update_style["greyshade"]
rake update_source["greyshade"]
```
现在刷新预览，已经生效了。
