title: 去除Hexo图片的外链
categories: [Hexo]
tags: [Hexo]
date: 2016-05-19 10:41:53
---

使用markdown的插入图片功能`![](http://img_path)`在Hexo下网页通常会对图片有个超链接，当你点击图片，图片就会弹出，感觉这个效果在你写的文章中没有必要出现，所以我对其做了修改，删除了Hexo图片的外链。

<!--more-->

打开`Hexo\themes\light\source\js\gallery.js`,删除如下的代码
```js
$(this).wrap('<a href="' + this.src + '" title="' + alt + '" class="fancybox" rel="gallery' + i + '" />');
```