title: HTML5 增强的页面元素
categories: [Web,HTML5]
tags: [HTML5]
date: 2016-06-04 14:08:37
---

# figure元素与figcaption元素

&nbsp;&nbsp;&nbsp;&nbsp;`figure`元素是一种元素的组合，带有可选标题。`figure`元素用来表示网页上一块独立的内容，将其从网页上移除后不会对网页上的其他内容产生任何影响。`figure`元素所表示的内容可以是图片、统计图或者代码示例。

&nbsp;&nbsp;&nbsp;&nbsp;`figcaption`元素表示`figure`元素的标题，它从属与`figure`元素，必须书写在`figure`元素内容，可以书写在`figure`元素内的其他从属元素的前面或后面。一个`figure`元素内最多只允许放置一个`figcaption`元素，但允许放置多个其他元素。

示例
```
<figure>
    <img src="xx.jpg" alt="img1">
    <figcaption>img1</figcaption>
</figure>
```

<!--more-->

# details元素

`details`元素提供了一种替代Javascript的、将画面上局部区域进行展开或收缩的方法。

示例
```
<details>
    <summary>HTML</summary>
    <p>超文本标记语言</p>
</details>
```

&nbsp;&nbsp;&nbsp;&nbsp;`summary`元素从属与`details`元素，用鼠标点击`summary`元素中的内容文字时，`details`元素中的其他所有从属元素将会展开或收缩。

# mark元素

&nbsp;&nbsp;&nbsp;&nbsp;`mark`元素表示页面中需要突出显示或高亮显示的，对于当前用户具有参考作用的一段文字。它通常使用于引用原文的时候，目的是引起读者的注意。`mark`元素是对原文内容具有补充作用的一个元素，它应该用于一段原文作者不认为重要，但为了与原文作者不相关的其他目的而需要突出显示或高亮显示的文字上面。

# progress元素

&nbsp;&nbsp;&nbsp;&nbsp;`progress`元素代表一个任务的完成进度，这个进度可以是不确定的，只是表示进度正在进行，但不清楚还有多少工作量没有完成，可以用0到某个最大数字之间的数字来表示准确的进度完成情况。该元素具有两个属性来表示当前任务完成情况，`value`属性表示已经完成了多少工作量，`max`属性表示总共有多少工作量。
&nbsp;&nbsp;&nbsp;&nbsp;在属性设定时，`value`属性和`max`属性只能指定为有效的浮点数，`value`属性的值必须大于0，且小于或等于`max`属性，`max`属性的值必须大于0.

示例
```
<!DOCTYPE HTML>
<html>
<head lang="en">
  <meta charset="utf-8">
  <title>progress元素</title>
  <script>
    function btn(){
      var i=0;
      function thread_one(){
        if (i<100){
          i++;
          updateprogress(i);
        }
      }
      setInterval(thread_one,100);
    }
    function updateprogress(newValue){
      var progressBar=document.getElementById("p");
      progressBar.vale=newValue;
      progressBar.getElementByTagName("span")[0].textContent=newValue;
    }
  </script>
</head>
<body>
  <section>
    <h2>progress元素的使用</h2>
    <p>进度<progress style="background-color:red" id="p" max="100"><span>0</span>%</progress></p>
    <input type="button" onclick="btn()" value="提交">
  </section>
</body>
</html>
```

# meter元素

`meter`元素表示规定范围内的数量值。

`meter`元素有六个属性：
- value：在元素中特地表示出来的实际值。该属性值默认为0，可以给改属性指定一个浮点小数。
- min：指定规定的范围时允许使用的最小值，默认为0，设定该属性时设定的值不能小于0。
- max：指定规定的范围时允许使用的最大值，如果设定时该属性值小于min属性的值，那么把min属性的值视为最大值，max属性的默认值为1。
- low：规定范围的下限值。必须小于或等于high属性的值。同样的，如果low属性值小于min属性的值，那么把min属性的值视为low属性的值。
- high：规定范围的上限值。如果该属性值小于low属性的值，那么把low属性的值视为high属性的值，同样的，如果该属性值大于max属性的值，那么把max属性的值视为high属性的值。
- optimum：最佳值，属性值必须在min属性值与max属性值之间，可以大于high属性值。

# ol列表

在HTML5中，将`ol`列表进行了改良，为它添加了`start`属性与`reversed`属性。`start`属性自定义编号的初始值。如果你想对列表进行反向排序，那么你可以使用`ol`列表的`reversed`属性。
