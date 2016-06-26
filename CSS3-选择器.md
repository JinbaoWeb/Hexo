title: CSS3 选择器
categories: [Web,CSS3]
tags: [CSS3]
date: 2016-06-07 17:20:06
---

# 类选择器

类选择器以一个点开头，接下来是所选择的类名本身。类名一般只包含字母、数字和连字符，必须以字母开头。

示例
```
.plant{
    margin: 10px 0;
}
```

<!--more-->

在CSS规则中，出现类名之前的点告诉CSS正在引用一个类选择器。这个点不需要出现在class属性值中；事实上它也不能出现在其中，因为class属性值只是类名本身。

示例
```
div.plant{
    margin: 10px 0;
}
```

元素同样可以被分配多个类名。属性中的每个类名之间用一个空格隔开。在相同的样式表中，两个类可能会有两条独立的规则引用。

示例:对于`class="plant jupiter"`
```
.plant{
    margin: 10px 0;
}
.jupiter{
    background-image: url(jupiter.jpg);
}
```

# ID选择器

ID选择器是唯一的标识符。要引用一个ID，需要在ID名称前加一个散列符号（#）。像类名一样，ID名称中也不能包含空格，而且必须以字母开头。只能由字母、数字、连字符和下划线组成的名称。

示例：
```
<style type="text/css">
    #jupiter{
        background-image: url(jupiter.jpg);
    }
</style>
<div class="planet" id="jupiter">
    <h1>Jupiter</h1>
</div>
```

# 通用选择器

通用选择器是一个星号，单独使用时，通用选择器告诉CSS解释器将该CSS规则应用于文档中的所有元素。

示例
```
*{
    font-family: Arial,Helvetica,sans-serif;
}
```

# 后代选择器

后代选择器基于一个元素是否包含另一个元素来应用样式。

```
<div class="planet" id="jupiter">
    <h1>Jupiter</h1>
</div>
```

要基于其祖先定位一个元素
```
div.planet h1{
    font-size:18px;
}
```

# 伪类选择器

## :link伪类和:visited伪类

`:link`伪类：表示未访问的超链接
`:visited`伪类：表示已访问过的超链接。

示例
```
a:link{color:blue};
a:visited{color:red};
```

## :hover伪类和:focus伪类

`hover`伪类:适用于用户的鼠标指针当前停留的那些元素，当用户的鼠标指针停留在相应元素上时，特定的样式将被应用；当用户的鼠标离开该元素时，元素将返回到之前的样式。
`:focus`伪类：与`:hover`类似，但是用于键盘焦点。

示例
```
a:hover{color:blue};
a:focus{color:red};
```

## :active伪类

`:active`伪类使用于用户当前正在其上单击并按住鼠标按键的元素。如果用户不释放鼠标按键，那么指定的样式将持续作用，直到用户释放鼠标按键，元素才会恢复原来的状态。

示例
```
a:active{color:blue};
```
