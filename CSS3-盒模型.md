title: CSS3 盒模型
categories: [Web,CSS3]
tags: [CSS3]
date: 2016-06-08 17:06:43
---

# CSS盒模型

![](http://7xv5vl.com1.z0.glb.clouddn.com/QQ%E6%88%AA%E5%9B%BE20160608171131.jpg)

<!--more-->

# margin

`margin`简写属性在一个声明中设置所有**外边距**属性。该属性可以有 1 到 4 个值。

可能的值
- `auto`:浏览器计算外边距。
- `length`:规定以具体单位计的外边距值，比如像素、厘米等。默认值是 0px。
- `%`:规定基于父元素的宽度的百分比的外边距。
- `inherit`:	规定应该从父元素继承外边距。

`margin: top right bottom left`:这些值的顺序是从上外边距 (top) 开始围着元素顺时针旋转的

单边外边距属性
- `margin-top`
- `margin-right`
- `margin-bottom`
- `margin-left`

# border

元素外边距内就是元素的的**边框**.

## border-width

`border-width`属性用来控制盒边框的宽度。

`border-width: top right bottom left`:这些值的顺序是从上外边框 (top) 开始围着元素顺时针旋转的.

可能的值
- `thin`:定义细的边框。
- `medium`:默认。定义中等的边框。
- `thick`:定义粗的边框。
- `length`:允许您自定义边框的宽度。
- `inherit`:	规定应该从父元素继承边框宽度。

## border-style

`border-style`属性来指定边框的样式。

可能的值
- `none`:定义无边框。
- `hidden`:与 "none" 相同。不过应用于表时除外，对于表，hidden 用于解决边框冲突。
- `dotted`:定义点状边框。在大多数浏览器中呈现为实线。
- `dashed`:定义虚线。在大多数浏览器中呈现为实线。
- `solid	`:定义实线。
- `double`:定义双线。双线的宽度等于 `border-width` 的值。
- `groove`:定义 3D 凹槽边框。其效果取决于 `border-color` 的值。
- `ridge	`:定义 3D 垄状边框。其效果取决于 `border-color` 的值。
- `inset	`:定义 3D `inset` 边框。其效果取决于 `border-color` 的值。
- `outset`:定义 3D `outset` 边框。其效果取决于 `border-color` 的值。
- `inherit`:	规定应该从父元素继承边框样式。

## border-color

`border-color` 属性设置四条边框的颜色。此属性可设置 1 到 4 种颜色。

可能的值
- `color_name`:规定颜色值为颜色名称的边框颜色（比如 red）。
- `hex_number`:规定颜色值为十六进制值的边框颜色（比如 #ff0000）。
- `rgb_number`:规定颜色值为 rgb 代码的边框颜色（比如 rgb(255,0,0)）。
- `transparent`:	默认值。边框颜色为透明。
- `inherit`:	规定应该从父元素继承边框颜色。

# padding

`padding` 属性定义元素的内边距。
`padding` 属性接受长度值或百分比值，但不允许使用负值。

也通过使用下面四个单独的属性，分别设置上、右、下、左内边距：
- `padding-top`
- `padding-right`
- `padding-bottom`
- `padding-left`