title: ZOJ3483 Gaussian Prime
categories: [ACM,ZOJ]
tags: [ZOJ,模拟]
date: 2016-03-26 19:25:09
---
Gaussian Prime

	In number theory, a Gaussian integer is a complex number whose real and 
	imaginary part are both integers. The Gaussian integers, with ordinary 
	addition and multiplication of complex numbers, form an integral domain, 
	usually written as Z[i]. The prime elements of Z[i] are also known as 
	Gaussian primes. Gaussian integers can be uniquely factored in terms of 
	Gaussian primes up to powers of i and rearrangements.

	A Gaussian integer a + bi is a Gaussian prime if and only if either:

	One of a, b is zero and the other is a prime number of the form 4n + 3 
	(with n a nonnegative integer) or its negative -(4n + 3)；
	Both are nonzero and a2 + b2 is a prime number (which will not be of 
	the form 4n + 3).
	0 is not Gaussian prime. 1, -1, i, and -i are the units of Z[i], but 
	not Gaussian primes. 3, 7, 11, ... are both primes and Gaussian primes. 
	2 is prime, but is not Gaussian prime, as 2 = i(1-i)2.

	Your task is to calculate the density of Gaussian primes in the complex 
	plane [x1, x2] × [y1, y2]. The density is defined as the number of Gaussian 
	primes divided by the number of Gaussian integers.

<!--more-->

Input

	There are multiple test cases. The first line of input is an integer T ≈ 100 
	indicating the number of test cases.

	Each test case consists of a line containing 4 integers -100 ≤ x1 ≤ x2 ≤ 100, 
	-100 ≤ y1 ≤ y2 ≤ 100.

Output

	For each test case, output the answer as an irreducible fraction.

Sample Input

	3
	0 0 0 0
	0 0 0 10
	0 3 0 3

Sample Output

	0/1
	2/11
	7/16

题意

	复数a+bi是素数满足
	（1）a，b中有一个是0，另外一个是素数，且是4n+3，-(4n+3)的形式。
	（2）a，b中没有一个是0，a*a+b*b是素数，且不是4n+3的形式。
	a的取值范围为[x1,x2],b的取值范围为[y1,y2],求在a，b范围内能够形成复数是素数的占构成复数的分数比。

解题思路

	暴力枚举a和b

参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
int gcd(int a, int b)
{
    if(b == 0)
        return a;
    return gcd(b, a % b);
}
bool isprime(int x)
{
	if (x<2) return false;
	if (x==3 || x==2 || x==7 || x==5)
		return true;
	for (int i=2;i*i<=x;i++)
		if (x%i==0)
			return false;
	return true;
}
bool f(int i,int j)
{
	if (i==0&&j!=0)
	{
		if (j<0) j=(-j);
		if (j%4==3 && isprime(j)==true)
			return true;
		return false;
	}
	else if (i!=0&&j==0)
	{
		if (i<0) i=(-i);
		if (i%4==3 && isprime(i)==true)
			return true;
		return false;
	}
	else
	{
		if (i!=0 && j!=0)
		{
			if (isprime(i*i+j*j)==true)
				return true;
			return false;
		}
		return false;
	}
}
int main()
{
	int t,x1,x2,y1,y2;
	scanf("%d",&t);
	while (t--)
	{
		scanf("%d%d%d%d",&x1,&x2,&y1,&y2);
		int k=0,ans=0;
		for (int i=x1;i<=x2;i++)
		{
			for (int j=y1;j<=y2;j++)
			{
				k++;
				if (f(i,j)==true)
					ans++;
			}
		}
		int cnt=gcd(k,ans);
		k/=cnt;
		ans/=cnt;
		cout<<ans<<"/"<<k<<endl;
	}
	return 0;
}
```