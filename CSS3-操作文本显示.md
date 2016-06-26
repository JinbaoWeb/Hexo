title: CSS3 操作文本显示
categories: [Web,CSS3]
tags: [CSS3]
date: 2016-06-08 00:42:53
---

# line-height

`line-height`属性设置行间的距离（行高）。

可能的值
- `normal`:默认。设置合理的行间距。
- `number`:设置数字，此数字会与当前的字体尺寸相乘来设置行间距。
- `length`:设置固定的行间距。
- `%`:基于当前字体尺寸的百分比行间距。
- `inherit`:规定应该从父元素继承`line-height`属性的值。

<!--more-->

# letter-spacing

`letter-spacing`属性增加或减少字符间的空白（字符间距）。

可能的值
- `normal`:默认。规定字符间没有额外的空间。
- `length`:定义字符间的固定空间（允许使用负值）。
- `inherit`:规定应该从父元素继承`letter-spacing`属性的值。

# word-spacing

`word-spacing` 属性增加或减少单词间的空白（即字间隔）。

可能的值
- `normal`:默认。定义单词间的标准空间。
- `length`:定义单词间的固定空间。
- `inherit`:规定应该从父元素继承`word-spacing`属性的值。

# text-indent

`text-indent` 属性规定文本块中首行文本的缩进。

可能的值
- `length`:定义固定的缩进。默认值：0。
- `%	`:定义基于父元素宽度的百分比的缩进。
- `inherit`:	规定应该从父元素继承`text-indent`属性的值。

# text-align

`text-align`属性规定元素中的文本的水平对齐方式。

可能的值
- `left`:把文本排列到左边。默认值：由浏览器决定。
- `right`:把文本排列到右边。
- `center`:把文本排列到中间。
- `justify`:	实现两端对齐文本效果。
- `inherit`:	规定应该从父元素继承`text-align`属性的值。

# text-decoration

`text-decoration`属性规定添加到文本的修饰。

可能的值
- `none`:默认。定义标准的文本。
- `underline`:定义文本下的一条线。
- `overline`:定义文本上的一条线。
- `line-through`:定义穿过文本下的一条线。
- `blink	`:定义闪烁的文本。
- `inherit`:	规定应该从父元素继承`text-decoration`属性的值。

# text-transform

`text-transform` 属性控制文本的大小写。

可能的值
- `none`:默认。定义带有小写字母和大写字母的标准的文本。
- `capitalize`:文本中的每个单词以大写字母开头。
- `uppercase`:定义仅有大写字母。
- `lowercase`:定义无大写字母，仅有小写字母。
- `inherit`:	规定应该从父元素继承 `text-transform` 属性的值。

# white-space

`white-space` 属性设置如何处理元素内的空白。

可能的值
- `normal`:默认。空白会被浏览器忽略。
- `pre`:	空白会被浏览器保留。其行为方式类似 HTML 中的 <pre> 标签。
- `nowrap`:文本不会换行，文本会在在同一行上继续，直到遇到 <br> 标签为止。
- `pre-wrap`:保留空白符序列，但是正常地进行换行。
- `pre-line`:合并空白符序列，但是保留换行符。
- `inherit`:	规定应该从父元素继承 `white-space` 属性的值。
