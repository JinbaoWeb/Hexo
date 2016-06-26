title: HTML5 新增元素与属性
categories: [Web,HTML5]
tags: [HTML5]
date: 2016-06-03 15:43:26
---

# form属性

在HTML4中，表单内的从属元素必须书写在表单内部，但是在HTML5中，可以把它们书写在页面上任何地方，然后给该元素指定一个`form`属性，属性值为该表单的`id`，这样就可以声明该元素从属与指定表单了。

示例
```
<form id="testform"><input type="text"></form>
<textarea form="testform"></textarea>
```

<!--more-->

# formaction属性

在HTML4中，一个表单内的所有元素都只能通过表单的`action`属性统一提交到另一个页面，而在HTML5中可以给所有的提交按钮，如`<input type="submit">`、`<input type="image">`、`<button type="submit">`都增加不同的`formaction`属性，使得点击不同的按钮可以将表单提交到不同的页面。

示例
```
<form id="testform" action="serve.jsp">
    <input type="submit" name="s1" value="v1" formaction="s1.jsp">提交到s1
    <input type="submit" name="s2" value="v2" formaction="s2.jsp">提交到s2
    <input type="submit" name="s3" value="v3" formaction="s3.jsp">提交到s3
    <input type="submit">
</form>
```

# formmethod属性

在HTML4中，一个表单内只有一个`action`属性来对表单内所有元素统一指定提交到页面，所以每个表单内也只有一个`method`属性来指统一指定提交方法。在HTML5中，可以使用`formaction`属性来对每个表单元素分别指定不同的提交页面，同时也可以使用`formmethod`属性来对每个表单元素分别指定不同的提交方法。

实例
```
<form id="testform" action="serve.jsp">
    <input type="submit" name="s1" value="v1" formaction="s1.jsp" formmethod="get">提交到s1
    <input type="submit" name="s2" value="v2" formaction="s2.jsp" formmethod="post">提交到s2
    <input type="submit" name="s3" value="v3" formaction="s3.jsp" formmethod="get">提交到s3
    <input type="submit">
</form>
```

# placeholder属性

`placeholder`是指当文本框处于未输入状态时文本框中显示的输入提示。

示例
```
<input type="text" placeholder="input me">
```

# autofocus属性

给文本框、选择框或按钮控件加上该属性，当画面打开时，该控件自动获得光标焦点。目前为止要做到这一点需要使用javascript,如“control.focus()”。

示例
```
<input type="text" autofocus>
```

一个页面上只能有一个控件具有该属性，从实用角度来说，请不要随便滥用该属性。强烈建议只有当一个页面是以使用某个控件为主要目的时，才对该控件使用`autofocus`属性，例如搜索页面中的搜索文本框。

# list属性

在HTML5中，为单行文本框增加一个lsit属性，该属性值为某个datalist元素的id。datalist元素也是HTML5中新增元素，该元素类似于选择框，但是当用户想要设定的值不在选择列表之内时，允许其自行输入。该元素本身并不显示，而是当文本框获得焦点时以提升输入的方式显示。为了避免在没有支持该元素的浏览器上出现显示错误，可以用css等将它设定为不显示。

示例
```
<input type="text" name="greeting" list="greetings">
<datalist id="greeting" style="display:none;">
    <option value="Good Morning">Good Morning</option>
    <option value="Good Afternoon">Afternoon</option>
    <option value="Good">Good</option>
</datalist>
```

# autocomplete属性

辅助输入所用的自动完成功能，是一个节省输入时间，同时也十分方便的功能。对于autocomplete属性，可以指定“on”，“off”与“”（不指定）这三种值。不指定时，使用浏览器的默认值（取决于各浏览器的决定）。把属性设为on时，可以显示指定候补输入的数据列表。使用datalist元素与list属性提供候补输入的数据列表，自动完成时，可以将datalist元素中的数据作为候补输入的数据在文本框中自动显示。

示例
```
<input type="text" name="greeting" autocomplete="on" list="greetings">
<datalist id="greeting" style="display:none;">
    <option value="Good Morning">Good Morning</option>
    <option value="Good Afternoon">Afternoon</option>
    <option value="Good">Good</option>
</datalist>
```