title: HTML5 表单验证
categories: [Web,HTML5]
tags: [HTML5]
date: 2016-06-04 13:14:03
---

# 自动验证

示例
```
<form method="post">
    <input name="text" type="text" required pattern="^\w.*$">
    <input type="submit">
</form>
```

## required属性

HTML5中新增的`required`属性可以应用在大多数输入元素上（除了隐藏元素、图片元素按钮上，在提交时，如果元素中内容为空白，则不允许提交，同时在浏览器中显示信息提示文字，提升用户这个元素中必须输入内容。

<!--more-->

## pattern属性

对一些`input`元素，例如`email`、`number`、`url`等，要求输入内容符合一定的格式，对`input`元素使用`pattern`属性，并且将属性值设为某个格式的正则表达式，在提交时会检查其内容是否符合给定格式。当输入的内容不符合给定格式时，则不允许提交，同时在浏览器中显示信息提示文字，提示输入的内容必须符合给定格式。

示例
```
<input pattern="[0-9][A-Z]{3}" name=part placeholder="输入内容：一个数字与三个大写字母">
```

## min属性与max属性

限制了在`input`元素中输入的数值与日期的范围。

## step属性

`step`属性控制`input`元素中的值增加或减少时的步幅。

# 显示验证

&nbsp;&nbsp;&nbsp;&nbsp;在HTML5中，`form`元素与`input`元素（包括`select`元素与`textarea`元素）都具有一个`checkValidity`方法。调用该方法，可以显示地对表单内所有元素内容或单个元素内容进行有效性验证。

示例
```
<!DOCTYPE HTML>
<html>
<head lang="en">
  <meta charset="utf-8">
  <title>HTML5表单显示验证</title>
  <script type="text/javascript">
  function check()
  {
    var email=document.getElementById("email");
    if (email.value=="")
    {
      alert("请输入email地址");
      return false;
    }
    else if (!email.checkValidity())
      alert("请输入正确的Email地址");
    else
      alert("您输入的Email地址有效！");
  }
  </script>
</head>
<body>
  <form id="testform" onsubmit="return check();">
    <label for="email">Email</label>
    <input name="email" id="email" type="email" />
    <input type="submit">
  </form>
</body>
</html>
```

# 取消验证

有两种方法取消表单验证：
（1）利用`form`元素的`novalidate`属性，它可以关闭整个表单验证，当整个表单的第二部分需要验证的内容比较多，但又想先提交表单的第一部分内容时，可以使用这种方法。先把该属性设为`true`，关闭表单验证，提交第一部分内容，然后再提交第二部分时再把它设为`false`，打开表单验证，提交第二部分内容。
（2）利用`input`元素或`submit`元素的`formnovalidate`属性，利用`input`元素的`formnovalidate`属性可以让表单验证对单个`input`元素失效，在前面所举例子中，当表单的第二部分中需要验证的元素数量很少时，可以只利用这些元素的`formnovalidate`属性，让表单验证对这些元素失效。