title: HTML5 新增的的非主体结构元素
categories: [Web,HTML5]
tags: [HTML5]
date: 2016-06-02 21:43:39
---

# header元素

> header元素是一种具有引导和导航作用的结构元素，通常用来放置整个页面或页面内的一个内容区块的标题，但也可以包含其他内容，例如数据表格、搜索表单或相关的logo图片。

示例
```
<header><h1>页面标题</h1></header>
```

> 一个网页内并未限制header元素的个数，可以拥有多个，可以为每个内容区块加一个header元素。

示例
```
<header>
    <h1>页面标题</h1>
</header>
<article>
    <header>
        <h1>文章标题</h1>
    </header>
    <p>文章正文</p>
</article>
```

<!--more-->

# hgroup元素

> hgroup元素是将标题及其子标题进行分组 的元素。hgroup元素通常会将h1-h6元素进行分组，比如一个内容区块的标题及其子标题算一组。

示例
```
<article>
    <header>
        <hgroup>
            <h1>文章主标题</h1>
            <h2>文章子标题</h2>
        </hgroup>
        <p><time datetime="2010-03-20">2010年3月20号</time></p>
    </header>
    <p>文章正文</p>
</article>
```
通常，如果文章只有一个主标题，是不需要hgroup元素的。

# footer元素

> footer元素可以作为其上层父级内容区块或是一个根区块的脚注。footer通常包括其相关区块的脚注信息，如作者、相关阅读链接及版权信息等。

示例
```
<footer>
    <ul>
        <li>版权信息</li>
        <li>站点地图</li>
        <li>联系方式</li>
    </ul>
</footer>
```
与header元素一样，一个页面中也未限制footer元素的个数。同时，可以为article元素或section元素添加footer元素。

# address元素

> address元素用来在文档中呈现联系信息，包括文档作者或文档维护者的名字、他们的网站链接、电子邮箱、真实地址、电话号码等。address应该不只是用来呈现电子邮箱或真实地址，还应用来展示跟文档相关联系人的所有联系信息。

示例
```
<footer>
    <div>
        <address>
            <a href="#">Iwen</a>
        </address>
        发表于<time datetime="2016-06-03">2016年6月3号</time>
    </div>
</footer>
```