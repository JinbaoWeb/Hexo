title: HTML5 改良的input元素的种类
categories: [Web,HTML5]
tags: [HTML5]
date: 2016-06-03 19:03:45
---
# url类型

`url`类型的`input`元素是一种专门用来输入`url`地址的文本框。提交时如果该文本框中内容不是url地址格式的文字，则不允许提交。

示例
```
<input name="url1" type="url" value="http://www.baidu.com">
```

# email类型

`email`类型的`input`元素是一种专门用来输入`email`地址的文本框。提交时如果该文本框中内容不是`email`地址格式的文字则不允许提交，但是它并不检查该`email`地址是否存在。提交时该文本框可以为空，除非加上`required`属性。

`email`类型的文本框具有一个`multiple`属性——它允许在该文本框中输入一串以逗号分隔的`email`地址。当然，并不强调要求用户输入该`email`地址列表。在实际使用过程中，可以由开发者通过编程的方式将用户联系人地址列表中的邮件列表弹出，在每个联系人的邮件地址旁边带有复选框i，供用户选择输入。

<!--more-->

示例
```
<input name="email1" type="email" value="xxxx@sina.com">
```

# date类型

`date`类型的`input`元素以日历的形式方便用户输入，当该文本框获得焦点时，显示日历，可以在日历中选择日期进行输入。

示例
```
<input name="date1" type="date" value="2010-10-02">
```

# time类型

`time`类型的`input`元素是一种专门用来输入时间的文本框，并且在提交时会对输入时间的有效性进行检查。它的外观取决于浏览器，可能是简单的文本框，只在提交时检查是否在其中输入了有效的时间，也可能以时钟形式出现，还可以携带时区。

示例
```
<input name="time1" type="time" value="10:00">
```

# datetime类型

`datetime`类型的`input`元素是一种专门用来输入UTC日期和时间的文本框，并且在提交时会对输入的日期和时间进行有效性检查。

示例
```
<input name="datetime1" type="datetime">
```

# datetime-local类型

`datetime-local`类型的`input`元素是一种专门用来输入本地日期和时间的文本框，并且在提交时会对输入的日期和时间进行有效性检查。

示例
```
<input name="datetime-local1" type="datetime-local">
```

# month类型

`month`类型的`input`元素是一种专门用来输入月份的文本框，并且在提交时会对输入的月份的有效性进行检查。

示例
```
<input name="month1" type="month" value="2010-10">
```

# week类型

`week`类型的`input`元素是一种专门用来输入周号之有效性检查。它可能是一个简单的输入文本框，允许用户输入一个数字，也可能更复杂、更精确。

示例
```
<input name="week1" type="week" value="2010-w40">
```

# number类型

`number`类型的`input`元素是一种专门用来输入数字的文本框，并且在提交时会检查其中的内容是否为数字，它具有`min`、`max`与`step`属性。

示例
```
<input name="number1" type="number" value="25" min="10" max="110" step="5">
```

# range类型

`range`类型的`input`元素是一种只允许输入一段范围内数值的文本框，它具有`min`属性与`max`属性，可以设定最小值与最大值（默认为0-100），它还具有`step`属性，可以指定每次托动的步幅。

示例
```
<input name="range1" type="range" value="25" min="0" max="100" step="5">
```

# search类型

`search`类型的`input`元素是一种专门用来输入搜索关键词的文本框。`search`类型与`text`类型仅仅在外观上有区别。

# tel类型

`tel`类型的`input`元素被设计为用来输入电话号码的专用文本框。它没有特殊的校验规则，不强制输入数字，但是开发者可以通过`pattern`属性来指定对输入的电话号码格式的验证。

# color类型

`color`类型的`input`元素用来选取颜色，它提供了一个颜色选取器。

# output元素

`output`元素定义不同类型的输出，`output`元素必须从属于某个表单，也就是说，必须将它书写在表单内部，或者对它添加`form`属性。

示例
```
<form id="testform">
    数值<input name="range1" type=range min=0 max=100 step=5 />
    <output onforminput="value=range1.value">50</output>
</form>
```