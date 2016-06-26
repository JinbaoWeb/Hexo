title: 消除Hexo中markdown语法跟Mathjax语法的冲突
categories: [Hexo]
tags: [Hexo,Mathjax]
date: 2016-05-19 10:22:02
---

在Hexo中写Mathjax语法`$L_{R_1}$`会出现错误，在网页上显示为`$L{R_1}$`，并没有像我们期望一样，显示为$L_{R_1}$，出现这个的原因是因为markdown语法中`__`表示粗体，`_`表示斜体，这使得markdown语法跟Mathjax语法的冲突，因此我们只需要对markdown删除对`_`的语法就可以了。

<!--more-->

打开`Hexo\node_modules\marked\lib\marked.js`，找到`Inline-Level Grammar`模块中的`<em>`和`Pedantic Inline Grammar`模块中的`<em>`（如果是用sublime打开，直接`ctrl+F`查找），结果如下：
```js
/**
 * Inline-Level Grammar
 */
var inline = {
  escape: /^\\([\\`*{}\[\]()#+\-.!_>])/,
  autolink: /^<([^ >]+(@|:\/)[^ >]+)>/,
  url: noop,
  tag: /^<!--[\s\S]*?-->|^<\/?\w+(?:"[^"]*"|'[^']*'|[^'">])*?>/,
  link: /^!?\[(inside)\]\(href\)/,
  reflink: /^!?\[(inside)\]\s*\[([^\]]*)\]/,
  nolink: /^!?\[((?:\[[^\]]*\]|[^\[\]])*)\]/,
  strong: /^__([\s\S]+?)__(?!_)|^\*\*([\s\S]+?)\*\*(?!\*)/,
  em: /^\b_((?:[^_]|__)+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
  code: /^(`+)\s*([\s\S]*?[^`])\s*\1(?!`)/,
  br: /^ {2,}\n(?!\s*$)/,
  del: noop,
  text: /^[\s\S]+?(?=[\\<!\[_*`]| {2,}\n|$)/
};
```
和
```js
/**
 * Pedantic Inline Grammar
 */
inline.pedantic = merge({}, inline.normal, {
  strong: /^__(?=\S)([\s\S]*?\S)__(?!_)|^\*\*(?=\S)([\s\S]*?\S)\*\*(?!\*)/,
  em: /^_(?=\S)([\s\S]*?\S)_(?!_)|^\*(?=\S)([\s\S]*?\S)\*(?!\*)/
});
```
对两个模块中的`<em>`删除对`_`的正则匹配。
对于`Inline-Level Grammar`中的`<em>`修改为
```js
em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
```
对于`Pedantic Inline Grammar`中的`<em>`修改为
```js
em: /^\*(?=\S)([\s\S]*?\S)\*(?!\*)/
```