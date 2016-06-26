title: POJ2926 Requirements
date: 2016-02-14 16:17:59
categories: [ACM,POJ]
tags: [POJ,曼哈顿距离]
---
# Requirements

## Description

	  An undergraduate student, realizing that he needs to do research to improve his chances of being 
	accepted to graduate school, decided that it is now time to do some independent research. Of course, 
	he has decided to do research in the most important domain: the requirements he must fulfill to 
	graduate from his undergraduate university. First, he discovered (to his surprise) that he has to 
	fulfill 5 distinct requirements: the general institute requirement, the writing requirement, 
	the science requirement, the foreign-language requirement, and the field-of-specialization 
	requirement. Formally, a requirement is a fixed number of classes that he has to take during 
	his undergraduate years. Thus, for example, the foreign language requirement specifies that 
	the student has to take 4 classes to fulfill this requirement: French I, French II, French III, 
	and French IV. Having analyzed the immense multitude of the classes that need to be taken to fulfill 
	the different requirements, our student became a little depressed about his undergraduate 
	university: there are so many classes to take…
	  Dejected, the student began studying the requirements of other universities that he might have 
	chosen after high school. He found that, in fact, other universities had exactly the same 5 
	requirements as his own university. The only difference was that different universities had 
	different number of classes to be satisfied in each of the five requirement.
	  Still, it appeared that universities have pretty similar requirements (all of them require a lot 
	of classes), so he hypothesized that no two universities are very dissimilar in their requirements. 
	He defined the dissimilarity of two universities X and Y as |x1 − y1| + |x2 − y2| + |x3 − y3| + 
	|x4 − y4| + |x5 − y5|, where an xi (yi) is the number of classes in the requirement i of university 
	X (Y) multiplied by an appropriate factor that measures hardness of the corresponding requirement at 
	the corresponding university.

<!--more-->

## Input

	The first line of the input file contains an integer N (1 ≤ N ≤ 100 000), the number of 
	considered universities. The following N lines each describe the requirements of a university. 
	A university X is described by the five non-negative real numbers x1 x2 x3 x4 x5.

## Output

	On a single line, print the dissimilarity value of the two most dissimilar universities. 
	Your answer should be rounded to exactly two decimal places.

## Sample Input

	3
	2 5 6 2 1.5
	1.2 3 2 5 4
	7 5 3 2 5

## Sample Output

	12.80

## 题意

	在一个5维空间里找到两个点的曼哈顿距离最大。

## 解题思路

	先对二维进行分析，|x1-x2|+|y1-y2|表示曼哈顿距离，那么我们进行讨论可知道
	( x1+y1) - ( x2+y2), 
	( x1-y1) - ( x2-y2), 
	(-x1+y1) - (-x2+y2), 
	(-x1-y1) - (-x2-y2)
	可以发现，去绝对值之后把同一点的坐标放在一起，对应坐标的符号总是相反的
	假如我们用0表示负号，1表示正号，则(-x1+y1)与(x2-y2)两个括号内的符号可以表示为：01和10       
	当你多举几个例子之后，就会发现，对于一个确定的维数D,符号转化成的二进制数，它们的和总是一个定值，即2^d-1
	于是只要对所有的点(x1,y1)，依次计算出(x1+y1),(x1-y1),(-x1+y1),(-x1-y1)这四种形式，然后把每个点算出来的
	这四种情况的最大值分别记录到一个数组max[]中，然后枚举每一种去绝对值的组合，组合后的最大值即为answer

## 参考代码
```objc
#include <cstdio>  
#include <cstring>  
#include <algorithm>  
#include <iostream>  
using namespace std;  
#define N 100003  
#define inf 1e100  
double a[N][5];  
int n;  
int main() {  
    while (scanf("%d", &n) == 1) {  
        for (int i=0; i<n; i++)  
            for (int j=0; j<5; j++) 
				scanf("%lf", &a[i][j]);  
        double ans = 0, mi, mx, t;  
        for (int s=0; s<(1<<5); s++) {  
            mi = inf, mx = -inf;  
            for (int i=0; i<n; i++) {  
                t = 0;  
                for (int j=0; j<5; j++)  
                    if ((1<<j) & s) t += a[i][j];  
                    else t -= a[i][j];  
                mi = min(mi, t);  
                mx = max(mx, t);  
            }  
            ans = max(ans, mx-mi);  
        }  
        printf("%.2lf\n", ans);  
    }  
    return 0;  
}  
```
