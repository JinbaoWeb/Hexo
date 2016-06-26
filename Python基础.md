title: Python基础
date: 2016-03-10 16:23:40
categories: [Python]
tags: [Python]
---
![](http://b.zol-img.com.cn/desk/bizhi/image/7/1024x768/1457422837901.jpg)
<!--more-->
1.数据类型

	整数：例如100、0xa5b4c3d2
	浮点数：例如1.23、1.2e-5
	字符串：以''或""括起来的任意文本
	布尔值：True、False
	空值：None
    
2.输入/输出

	print会依次打印每个字符串，遇到逗号“,”会输出一个空格
	Python提供内置的input()函数，用来接收来自用户的输入

```python
>>> print ('Hello,world')
Hello,world
>>> print ('Hello','world')
Hello world
>>> x = input()
123
>>> print (x+3)
Traceback (most recent call last):
  File "<pyshell#19>", line 1, in <module>
    print (x+3)
TypeError: Can't convert 'int' object to str implicitly
>>> y = int(input())
123
>>> print (y+3)
126
```

3.注释
 
	以 # 开头，后面的文字直到行尾都算注释
 
 4.变量
 
	变量名必须是大小写英文、数字和下划线（_）的组合，且不能用数字开头。
	在Python中，等号=是赋值语句，可以把任意数据类型赋值给变量，同一个变量可以反复赋值，
	而且可以是不同类型的变量。
    
5.逻辑操作符

	身份操作符：is操作符是一个二元操作符，如果其左端的对象引用与右端的对象引用指向的是
	同一个对象，则会放回true

```python
>>> a=["R",3,None]
>>> b=["R",3,None]
>>> a is b
False
>>> b = a
>>> a is b
True
>>>a is not None , b is None
(True,False)
```

	比较操作符：<表示小于,<=小于或等于,==表示等于,!=表示不等于,>=表示大于或等于,>表示大于

```python
>>> a=2
>>> b=6
>>> a==b
False
>>> a<b
True
>>> a<=b,a!=b,a>=b,a>b
(True,True,False,False)
>>> 0<=a<=10
True
```

	成员操作符：in用来测试成员关系，not in用来测试非成员关系

```python
>>> p=(4,'frog',9,-33,9,2)
>>> 2 in p
True
>>> 'dog' not in p
True
>>> phrase="Wild Swans by Jung Chang"
>>> "J" in phrase
True
>>> 'han' in phrase
True
```

	逻辑运算符：and,or与not，and与or返回决定结果的操作数，不是返回布尔值,not总是返回布尔值

```python
>>> five = 5
>>> two = 2
>>> zero = 0
>>> five and two
2
>>> two and five
5
>>> five or two
5
>>> two or five
2
```

6.控制流语句

```python
#if语句
if boolean_expression1:
    suite1
elif boolean_expression2:
    suite2
...
elif boolean_expressionN:
    suiteN
else:
    else_suite
    
#while语句
while boolean_expression:
    suite
    
#for...in语句
for variable in iterable:
    suite
```

7.基本异常处理

```python
try:
    try_suite
except exception1 as variable1:
    exception_suite1
...
except exceptionN as variableN:
    exception_suiteN
```

8.算术操作符

```python
>>> 5+6
11
>>> 3-7
-4
>>> 4*8
32
>>> 12/3
4.0
>>> 12%7
5
>>> 12//7
1
```

	Python重载了操作符+与+=，将其分别用于字符串与列表，前者表示连接，后者表示追加字符串并扩展

```python
>>> name = 'John'
>>> name + 'Doe'
'JohnDoe'
>>> name += 'Doe'
'JohnDoe'
>>> s = [1,2]
>>> s += [3]
>>> print (s)
[1, 2, 3]
```

9.函数

```python
def functionName(arguments):
    suite
```

10.练习

	输出0123456789的显示

```python
zero=['****',
	  '*  *',
	  '*  *',
	  '*  *',
	  '*  *',
	  '*  *',
	  '****']
one=['   *',
	  '   *',
	  '   *',
	  '   *',
	  '   *',
	  '   *',
	  '   *']
two=['****',
	  '   *',
	  '   *',
	  '****',
	  '*   ',
	  '*   ',
	  '****']
tree=['****',
	  '   *',
	  '   *',
	  '****',
	  '   *',
	  '   *',
	  '****']
four=['*  *',
	  '*  *',
	  '*  *',
	  '****',
	  '   *',
	  '   *',
	  '   *']
five=['****',
	  '*   ',
	  '*   ',
	  '****',
	  '   *',
	  '   *',
	  '****']
six=['****',
	  '*   ',
	  '*   ',
	  '****',
	  '*  *',
	  '*  *',
	  '****']
seven=['****',
	   '   *',
	   '   *',
	   '   *',
	   '   *',
	   '   *',
	   '   *']
eight=['****',
	   '*  *',
	   '*  *',
	   '****',
	   '*  *',
	   '*  *',
	   '****']
nine=['****',
	  '*  *',
	  '*  *',
	  '****',
	  '   *',
	  '   *',
	  '****']
row = 0
while row<7:
	print (zero[row],one[row],
	two[row],tree[row],four[row],
	five[row],six[row],seven[row],
	eight[row],nine[row])
	row += 1
```

