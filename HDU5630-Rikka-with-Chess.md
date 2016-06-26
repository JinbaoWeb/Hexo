title: HDU5630 Rikka with Chess
date: 2016-02-28 22:05:42
categories: [ACM,HDU]
tags: [HDU]
---
# Rikka with Chess

## 问题描述

	一个n × m的黑白相间的棋盘，每次可以选择一个矩形把其中的所有格子反色。问把所有格子变成一种颜色时的最少操作次数。

## 输入描述

	第一行一个整数 T(T≤10) 表示数据组数。
	每组数据有一行, 两个正整数 n,m(n<1e9,m<1e9);

## 输出描述

	对于每组数据输出一行一个整数，代表最少需要的操作次数。

<!--more-->

## 输入样例

	3
	1 2
	2 2
	3 3

## 输出样例

	1
	2
	2

## 参考代码
```objc
#include <stdio.h>
int main(){
	int t,n,m;
	scanf("%d",&t);
	while (t--){
		scanf("%d%d",&n,&m);
		printf("%d\n",n/2+m/2);
	}
	return 0;
}

```
