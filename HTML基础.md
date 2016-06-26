title: HTML基础
categories: [Web,HTML]
tags: [HTML]
date: 2016-05-18 16:16:16
---

# 一、HTML简介

## 1.1 HTML概念

HTML是用来描述网页的一种语言。

> HTML指的是**超文本标记语言**（Hyper Text Markup Language）
> HTML是一种标记语言

## 1.2 HTML标签

HTML标记标签通常被称为HTML标签（HTML tag）。

> HTML标签是由**尖括号**包围的关键词
> HTML标签通常是成对出现的。
> 标签对中的第一个标签是**开始标签**（也叫开放标签），第二个标签是**结束标签**（也叫闭合标签）。

<!--more-->

## 1.3 HTML文档

HTML文档 = 网页

> HTML文档描述网页
> HTML文档包含HTML标签和纯文本

# 二、HTML基础

## 2.1 HTML标题

HTML标题（Heading）是通过`<h1>-<h6>`等标签进行定义的。

实例
```html
<html>
<body>
<h1>This is heading 1</h1>
<h2>This is heading 2</h2>
<h3>This is heading 3</h3>
<h4>This is heading 4</h4>
<h5>This is heading 5</h5>
<h6>This is heading 6</h6>
</body>
</html>
```

## 2.2 HTML段落

HTML段落是通过`<p></p>`标签进行定义的。

实例
```html
<html>
<body>
<p>This is a paragraph.</p>
</body>
</html>
```

## 2.3 HTMl链接

HTML链接是通过`<a href="html_address"></a>`标签进行定义的。在href属性中指定链接的地址。

实例
```html
<html>
<body>
<a href="www.dongjinbao.com">Jinbao</a>
</body>
</html>
```

## 2.4 HTML图像

HTML图像是通过`<img src="img_path" />`标签进行定义的。图像的名称和尺寸是可以以属性的形式提供。

实例
```html
<html>
<body>
<img src="img_path" width="104" height="142" />
</body>
</html>
```

# 三、HTML元素

HTML元素指的是从开始标签到结束标签的所有代码。

## 3.1 HTML元素语法

> HTML元素以开始标签起始,一结束标签终止。
> 某些HTML元素具有空内容。
> 大多数HTML元素可拥有属性。
> 空元素在开始标签中进行关闭。

## 3.2 嵌套的HTML元素

大多数HTML元素可以嵌套，HTML文档由嵌套的HTML元素构成。

实例
```html
<html>
<body>
<p>This is my first HTML.</p>
</body>
</html>
```
实例包含三个HTML元素。
（1）<p>元素：
```html
<p>This is my first paragraph.</p>
```
这个<p>定义了HTML文档中的一个段落。这个元素拥有一个开始标签<p>，以及一个结束标签</p>，元素的内容是：`This is my first HTML.`。
（2）<body>元素：
```html
<body>
<p>This is my first paragraph.</p>
</body>
```
<body> 元素定义了 HTML 文档的主体。这个元素拥有一个开始标签 <body>，以及一个结束标签 </body>。元素内容是另一个 HTML 元素（p 元素）。
（3）<html>元素：
```html
<html>
<body>
<p>This is my first HTML.</p>
</body>
</html>
```
<html> 元素定义了整个 HTML 文档。这个元素拥有一个开始标签 <html>，以及一个结束标签 </html>。元素内容是另一个 HTML 元素（body 元素）。

## 3.3 空的HTML元素

没有内容的HTML元素被称为空元素。空元素是在开始标签中关闭的。
<br />就是没有关闭标签的空元素。

# 四、HTML属性

> 属性为HTML元素提供的附加信息。
> 属性总是以名称/值对的形式出现。
> 属性总是在HTML元素的开始标签中规定。

实例
```html
<html>
<body>
<h1 align="center">This is heading 1</h1>
</body>
</html>
```

# 五、HTML标题

## 5.1 HTML标题

标题（Heading）是通过 `<h1> - <h6>` 等标签进行定义的。`<h1>` 定义最大的标题。`<h6>` 定义最小的标题。

## 5.2 HTML水平线

`<hr />`标签在HTML页面中创建水平线。hr元素可用于分隔内容。

实例
```html
<html>
<body>
<p>First</p>
<hr />
<p>Second</p>
</body>
</html>
```

## 5.3 HTML注释

将注释插入HTML代码中，可以提高代码的可读性，浏览器会忽略注释，也不会显示它们。

实例
```html
<html>
<body>
<p>First</p>
<!-- This is a comment -->
</body>
</html>
```

# 六、HTML文本格式化

| 标签	        |     描述       |
| ------------- |:-------------| 
|`<b>`	|定义粗体文本。|
|`<big>`	|定义大号字。|
|`<em>`	|定义着重文字。|
|`<i>`	|定义斜体字。|
|`<small>`|	定义小号字。|
|`<strong>`|	定义加重语气。|
|`<sub>`	|定义下标字。|
|`<sup>`	|定义上标字。|
|`<ins>`	|定义插入字。|
|`<del>`	|定义删除字。|
|`<code>`	|定义计算机代码。|
|`<kbd>`	|定义键盘码。|
|`<samp>`	|定义计算机代码样本。|
|`<tt>`	|定义打字机代码。|
|`<var>`	|定义变量。|
|`<pre>`	|定义预格式文本。|
|`<abbr>`	|定义缩写。|
|`<acronym>`	|定义首字母缩写。|
|`<address>`	|定义地址。|
|`<bdo>`	|定义文字方向。|
|`<blockquote>`	|定义长的引用。|
|`<q>`	|定义短的引用语。|
|`<cite>`	|定义引用、引证。|
|`<dfn>`	|定义一个定义项目。