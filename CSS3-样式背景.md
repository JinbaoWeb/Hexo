title: CSS3 样式背景
categories: [Web,CSS3]
tags: [CSS3]
date: 2016-06-08 01:25:49
---

# background-color

`background-color`属性设置元素的背景颜色。

`background-color`属性为元素设置一种纯色。这种颜色会填充元素的内容、内边距和边框区域，扩展到元素边框的外边界（但不包括外边距）。如果边框有透明部分（如虚线边框），会透过这些透明部分显示出背景色。

可能的值
- `color_name`:规定颜色值为颜色名称的背景颜色（比如 red）。
- `hex_number`:规定颜色值为十六进制值的背景颜色（比如 #ff0000）。
- `rgb_number`:规定颜色值为 rgb 代码的背景颜色（比如 rgb(255,0,0)）。
- `transparent`:默认。背景颜色为透明。
- `inherit`:规定应该从父元素继承 `background-color` 属性的设置。

<!--more-->

# background-image

`background-image`属性为元素设置背景图像。
元素的背景占据了元素的全部尺寸，包括内边距和边框，但不包括外边距。
默认地，背景图像位于元素的左上角，并在水平和垂直方向上重复。

可能的值
- `url('URL')`:指向图像的路径。
- `none`:默认值。不显示背景图像。
- `inherit`:	规定应该从父元素继承 `background-image` 属性的设置。

# background-repeat

`background-repeat`属性设置是否及如何重复背景图像。默认地，背景图像在水平和垂直方向上重复。

可能的值
- `repeat`:默认。背景图像将在垂直方向和水平方向重复。
- `repeat-x`:背景图像将在水平方向重复。
- `repeat-y`:背景图像将在垂直方向重复。
- `no-repeat`:背景图像将仅显示一次。
- `inherit`:规定应该从父元素继承 `background-repeat` 属性的设置。

# background-position

`background-position` 属性设置背景图像的起始位置。

可能的值
(1)
top left
top center
top right
center left
center center
center right
bottom left
bottom center
bottom right
如果您仅规定了一个关键词，那么第二个值将是"center"。
默认值：0% 0%。
(2)
x% y%	
第一个值是水平位置，第二个值是垂直位置。
左上角是 0% 0%。右下角是 100% 100%。
如果您仅规定了一个值，另一个值将是 50%。
(3)
xpos ypos	
第一个值是水平位置，第二个值是垂直位置。
左上角是 0 0。单位是像素 (0px 0px) 或任何其他的 CSS 单位。
如果您仅规定了一个值，另一个值将是50%。
您可以混合使用 % 和 position 值。

# background-attachment

`background-attachment`属性设置背景图像是否固定或者随着页面的其余部分滚动。

可能的值
- `scroll`:默认值。背景图像会随着页面其余部分的滚动而移动。
- `fixed`:当页面的其余部分滚动时，背景图像不会移动。
- `inherit`:	规定应该从父元素继承 `background-attachment` 属性的设置。

# background-size

`background-size` 属性规定背景图像的尺寸。

可能取值
- `length`:设置背景图像的高度和宽度。第一个值设置宽度，第二个值设置高度。如果只设置一个值，则第二个值会被设置为 "auto"。
- `percentage`:以父元素的百分比来设置背景图像的宽度和高度。第一个值设置宽度，第二个值设置高度。如果只设置一个值，则第二个值会被设置为 "auto"。
- `cover`:把背景图像扩展至足够大，以使背景图像完全覆盖背景区域.背景图像的某些部分也许无法显示在背景定位区域中。
- `contain`:把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域。

# background-origin

`background-origin` 属性规定 `background-position` 属性相对于什么位置来定位。

可能取值
- `padding-box`:	背景图像相对于内边距框来定位.
- `border-box`:背景图像相对于边框盒来定位。
- `content-box`:	背景图像相对于内容框来定位。

# background-clip

`background-clip` 属性规定背景的绘制区域。

可能取值
- `border-box`:背景被裁剪到边框盒。
- `padding-box`:	背景被裁剪到内边距框。
- `content-box`:背景被裁剪到内容框。