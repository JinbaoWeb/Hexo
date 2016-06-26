title: HTML5 新增的主体结构元素
categories: [Web,HTML5]
tags: [HTML5]
date: 2016-06-02 19:48:18
---
# article元素

> article元素代表文档、页面或应用程序中独立的、完整的、可以独自被外部引用的内容。它可以是一篇博客或者报刊中的文章，一篇论坛帖子、一段用户评论或独立的插件，或其他任何独立的内容。

article的结构
```
<article>
    <header>...</header>
    <footer>...</footer>
</article>
```
`header`和`footer`可以不写.

<!--more-->

示例：
```
<html>
<head lang="en">
  <meta charset="utf-8"></meta>
  <title>article元素</title>
</head>
<body>
  <!--article元素的结构-->
  <article>
    <header>静夜思 李白</header>
    <p>
      床前明月光，疑是地上霜。<br />
      举头望明月，低头思故乡。<br />
    </p>
    <footer>
      又作：床前看月光，疑是地上霜。举头望山月，低头思故乡。
    </footer>
  </article>
</body>
</html>
```

> article元素是可以嵌套使用的，内层的内容在原则上需要与外层的内容相关联。

```html
<article>
    <header></header>
    <article>
    </article>
    <footer></footer>
</article>
```
示例：
```
<html>
<head lang="en">
  <meta charset="utf-8"></meta>
  <title>article元素</title>
</head>
<body>
  <!--article元素的嵌套-->
  <article>
    <header>静夜思 李白</header>
    <article>
      <p>
        床前明月光，疑是地上霜。<br />
        举头望明月，低头思故乡。<br />
      </p>
    </article>
    <footer>
      又作：床前看月光，疑是地上霜。举头望山月，低头思故乡。
    </footer>
  </article>
</body>
</html>
```

> article元素可以用来表示插件，它的作用是使插件看起来好像内嵌在页面中一样。

示例：现在将[百度页面](https://www.baidu.com/)内嵌进去。
```
<html>
<head lang="en">
  <meta charset="utf-8"></meta>
  <title>article元素</title>
</head>
<body>
  <!--article元素的插件-->
  <article>
    <h1>article插件</h1>
    <object>
      <embed src="https://www.baidu.com/" height="600px" width="1000px"></embed>
    </object>
  </article>
</body>
</html>
```
`<embed>` 标签定义嵌入的内容，必须有 src 属性,比如插件。
`<object>` 定义一个嵌入的对象.

# section元素

> `section`元素用于对网站或应用程序中页面上的内容进行分块。一个`section`元素通常由内容及其标题组成。但`section`元素并非一个普通的容器元素；当一个容器需要被直接定义样式或通过脚步定义行为时，推荐使用`div`而非`section`元素。

> `section`元素中的内容可以单独存储到数据库或输出word文档中。

示例:`article`中包含`section`
```
<html>
<head lang="en">
  <meta charset="utf-8"></meta>
  <title>section元素</title>
</head>
<body>
  <header>
    <h1>Section</h1>
  </header>
  <article>
    <h1>苹果</h1>
    <p><b>苹果</b>,植物类水果，多次花果...</p>
    <section>
      <h2>红富士</h2>
      <p>红富士是从普通富士的芽变中选育出的着色系富的统称...</p>
    </section>
    <section>
      <h2>国光</h2>
      <p>国光苹果品，又名小国光、万寿，原产美国，1600年发现的偶然实生苗...</p>
    </section>
  </article>
</body>
<footer>
  <p><small>版权声明</small></p>
</footer>
</html>
```
对文章分段的工作也是使用`section`元素完成的。
为什么对上面示例中的下列代码不使用`section`元素呢？
```
<h1>苹果</h1>
<p><b>苹果</b>,植物类水果，多次花果...</p>
```
这里其实是可以使用`section`元素的，但是由于其结构清晰，分析器可以识别第一段内容在一个`section`元素里，所有也可以将第一个`section`元素省略，但是如果第一个`section`元素还要包含子`section`元素或子`article`元素，那么久必须写明第一个`section`元素了。

在HTML5中，`article`元素可以看成是一种特殊种类的`section`元素，它比`section`元素更强调独立性，即`section`元素强调分段或分块，而`article`强调独立性。具体来说，如果一块内容相对来说比较独立、完整的时候，应该使用`article`元素，但是如果你想将一个块内容分成几段的时候，应该使用`section`元素。

关于`section`元素的使用禁忌：
- 不用讲`section`元素用作设置样式的页面容器，那是`div`元素的工作。
- 如果`article`元素、`aside`元素、`nav`元素更符合使用条件，那不用使用`section`元素。
- 不要为没有标题的内容区块使用`section`元素。

# nav元素

> `nav`元素是一个可以用作页面导航的连接组，其中的导航元素链接到其他页面或当前页面的其他部分。并不是所有的连接组都要被放进`nav`元素，只需要将主要的、基本的连接组放进`nav`元素即可。

示例
```
<html>
<head lang="en">
  <meta charset="utf-8"></meta>
  <title>nav元素</title>
</head>
<body>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Article</a></li>
    </ul>
  </nav>
  <article>
    <header>
      <h1>HTML5 and CSS3</h1>
      <nav>
        <ul>
          <li><a href="#">HTML5</a></li>
          <li><a href="#">CSS3</a></li>
        </ul>
      </nav>
    </header>
    <section>
      <h1>HTML5</h1>
      <p>The article of HTML5</p>
    </section>
    <section>
      <h1>CSS3</h1>
      <p>The article of CSS3</p>
    </section>
    <footer>
      <a href="#">删除</a>
      <a href="#">修改</a>
    </footer>
  </article>
</body>
<footer>
  <p><small>版权声明</small></p>
</footer>
</html>
```
第一个`nav`元素用于页面导航，将页面跳转到其他页面上去，第二个`nav`元素放置在`article`元素中，用作这篇文章中两个组成部分的页内导航。

`nav`元素应用场景：
- 传统导航条
- 侧边栏导航
- 页内导航
- 翻页操作

注意：在HTML5中不用用`menu`元素代替`nav`元素。`menu`元素是用在一系列发出命令的菜单上的，是一种交互性的元素，或者更确切地说使用在Web应用程序中的。

# aside元素

> `aside`元素用来表示当前页面或文章的附属信息部分，它可以包含与当前页面或主要内容相关的引用、侧边栏、广告、导航条，以及其他类似的有区别于主要内容的部分。

`aside`元素主要有以下两种使用方法：
（1）被包含在`article`元素中作为主要内容的附属信息部分，其中的内容可以是与当前文章有关的参考资料、名词解释等待。

示例
```
<html>
<head lang="en">
  <meta charset="utf-8"></meta>
  <title>aside元素</title>
</head>
<body>
  <header>
    <h1>F# 入门</h1>
  </header>
  <article>
    <h1>第四节 词法闭包</h1>
    <p>lambda表达式可以创建词法闭包...</p>
    <aside>
      <h1>名词解释</h1>
      <dl>
        <dt>F#</dt>
        <dd>F#为.Net2010中引入的新型函数型编程语言</dd>
      </dl>
      <dl>
        <dt>词法闭包</dt>
        <dd>词法闭包是指将创建lambda表达式时的环境保存起来...</dd>
      </dl>
    </aside>
  </article>
</body>
<footer>
  <p><small>版权声明</small></p>
</footer>
</html>
```
这是一篇文章，网页的标题放在了`header`元素中，在`header`元素的后面将所有关于文章的部分放在了一个`article`元素中，将文章的正文部分放在了一个`p`元素中，但是该文章还有一个名词解释的附属部分，用来解释该文章中的一些名词，因此，在`p`元素的下部又放置一个`aside`元素，用来存放名词解释部分的内容。

（2）在`article`元素之外使用，作为页面或站点全局的附属信息部分。最典型的形式是侧边栏，其中的内容可以是友情链接，博客中其他文章列表、广告单元等。
```
<html>
<head lang="en">
  <meta charset="utf-8"></meta>
  <title>aside元素</title>
</head>
<body>
  <header>
    <h1>F# 入门</h1>
  </header>
  <article>
    <h1>第四节 词法闭包</h1>
    <p>lambda表达式可以创建词法闭包...</p>
    <aside>
      <h1>名词解释</h1>
      <dl>
        <dt>F#</dt>
        <dd>F#为.Net2010中引入的新型函数型编程语言</dd>
      </dl>
      <dl>
        <dt>词法闭包</dt>
        <dd>词法闭包是指将创建lambda表达式时的环境保存起来...</dd>
      </dl>
    </aside>
  </article>
  <aside>
    <nav>
      <h2>评论</h2>
      <ul>
        <li><a href="#">2016-6-2</li>
        <li><a href="#">2016-6-3</li>
      </ul>
    </nav>
  </aside>
</body>
<footer>
  <p><small>版权声明</small></p>
</footer>
</html>
```

# time元素和pubdate属性

`<time>` 标签定义日期或时间，或者两者，表示时刻时允许带时差，它可以定义多格式的日期和时间。

`pubdate` 属性指示 `<time>` 元素中的日期 / 时间是文档（或最近的前辈 `<article>` 元素）的发布日期。