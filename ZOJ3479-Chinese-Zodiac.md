title: ZOJ3479 Chinese Zodiac
categories: [ACM,ZOJ]
tags: [ZOJ,模拟]
date: 2016-03-26 19:26:21
---
Chinese Zodiac

	The Shengxiao, better known in English as the Chinese Zodiac, is a 
	scheme that relates each year to an animal and its reputed attributes, 
	according to a 12-year cycle. The zodiac traditionally begins with the 
	sign of the Rat, and the twelve zodiac signs are Rat, Ox, Tiger, Rabbit, 
	Dragon, Snake, Horse, Ram, Monkey, Rooster, Dog and Pig. The zodiac signs 
	cycles continuously, and determines the animal or sign under which a 
	person is born. This year (2011, more accurately Chinese Xin Mao Year -- 
	3 February 2011 - 22 January 2012) is the Chinese Year of the Rabbit, so 
	the babies born in this year are said to be born under the Chinese Zodiac 
	sign of the Rabbit.

	In China, Xusui, also known as east Asian age reckoning, is used to count 
	a person's age. Newborns start at one year old, and each passing of a Lunar 
	New Year, rather than the birthday, adds one year to the person's age. In 
	other words, the first year of life is counted as one instead of zero, so 
	that a person is two years old in their second year, three years old in 
	their third, and so on.

	Given the traditional age (Xusui) of someone, you are requested to answer 
	his zodiac sign (Shengxiao).

<!--more-->

Input

	There are multiple test cases. The first line of input is an integer T ≈ 1000 
	indicating the number of test cases.

	Each test case contains only one positive integer y ≤ 200 -- the traditional age.

Output

	For each test case, output a string -- the zodiac sign.

Sample Input

	5
	1
	23
	40
	100
	160

Sample Output

	Rabbit
	Snake
	Rat
	Rat
	Rat

题意

	给你一个虚岁y，y是十二生肖中的哪一年生肖？

解题思路

	暴力模拟

参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
char s[12][20]={"Rabbit","Tiger","Ox",
"Rat","Pig","Dog","Rooster","Monkey",
"Ram","Horse","Snake","Dragon"};
int main()
{
	int t,n;
	cin>>t;
	while (t--)
	{
		cin>>n;
		cout<<s[(n%12-1+12)%12]<<endl;
	}
	return 0;
}
```