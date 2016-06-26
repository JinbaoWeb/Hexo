title: HTML 样式、链接和表格
categories: [Web,HTML]
tags: [HTML]
date: 2016-05-28 21:52:45
---
# 样式

三种样式表插入方法：

## 外部样式表

外部样式表就是把css代码写一个单独的外部文件中，这个css样式文件以".css"为扩展名，在`<head>`内使用`<link>`标签将css样式文件链接到HTML文件内。注意：`rel="stylesheet" type="text/css"`是固定写法不可修改。
```
<link rel="stylesheet" type="text/css" href="style.css">
```

<!--more-->

## 内部样式表

内部样式表就是把css样式代码写在`<style type="text/css"></style>`标签之间。一般情况下内部样式表写在`<head></head>`之间。
```html
<style type="text/css">
body{background-color:red}
p{margin-left:20px}
</style>
```

## 内联样式表

内联样式表就是把css代码直接写在现有的HTML标签中，并且css样式代码要写在style=""双引号中，如果有多条css样式代码设置可以写在一起，中间用分号隔开。
```html
<p style="color:red">
```

# 链接

## 链接数据

链接数据分文本链接和图片链接

```
<!DOCTYPE html>
<html lang="en">
	<meta charset="utf-8">
	<head>
		<title>链接</title>
	</head>
	<body>
		<a href="http://www.baidu.com">百度</a>
		<a href="http://www.baidu.com"><img src="img/njust.jpg" width="100px" height="100px"><a>
	</body>
</html>
```
结果如下：
![](http://7xsvcj.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160530164743.jpg)

## 属性

href属性：指向另一个文档的链接

name属性：创建文档内的链接

## img标签属性

alt：替换文本属性，当图片显示不出来的时候，作为文字显示图片内容。
width：宽
height：高

