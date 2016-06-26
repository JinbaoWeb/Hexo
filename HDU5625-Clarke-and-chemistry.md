title: HDU5625 Clarke and chemistry
date: 2016-02-14 16:34:56
categories: [ACM,HDU]
tags: [HDU]
---
# Clarke and chemistry

## Problem Description

	Clarke is a patient with multiple personality disorder. One day, Clarke turned into a junior student 
	and took a chemistry exam. 
	But he did not get full score in this exam. He checked his test paper and found a naive mistake, 
	he was wrong with a simple chemical equation balancer. 
	He was unhappy and wanted to make a program to solve problems like this. 
	This chemical equation balancer follow the rules: 
	Two valences A combined by |A| elements and B combined by |B| elements. 
	We get a new valence C by a combination reaction and the stoichiometric coefficient of C is 1. 
	Please calculate the stoichiometric coefficient a of A and b of B that aA+bB=C,  a,b∈N∗.

<!--more-->

## Input

	The first line contains an integer T(1≤T≤10), the number of test cases. 
	For each test case, the first line contains three integers A,B,C(1≤A,B,C≤26), denotes |A|,|B|,|C| respectively. 
	Then A+B+C lines follow, each line looks like X c, denotes the number of element X of A,B,C 
	respectively is c. (X is one of 26 capital letters, guarantee X of one valence only appear one time, 1≤c≤100)
 

## Output

	For each test case, if we can balance the equation, print a and b. If there are multiple answers, 
	print the smallest one, a is smallest then b is smallest. Otherwise print NO.
 

## Sample Input

	2
	2 3 5	
	A 2
	B 2
	C 3
	D 3
	E 3
	A 4
	B 4
	C 9
	D 9
	E 9
	2 2 2
	A 4
	B 4
	A 3
	B 3
	A 9
	B 9
 

## Sample Output

	2 3
	NO

## Hint

	The first test case, $a=2, b=3$ can make equation right.  
	The second test case, no any answer.
 
## 题意

	求aA+bB=C，其中A是a*1的行列式，B是b*1的行列式，C是c*1的行列式，求a和b使得等式成立。

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
int A[30],B[30],C[30];
int main(){
	int t,a,b,c;
	char s;
	int num;
	scanf("%d",&t);
	while (t--){
		scanf("%d%d%d",&a,&b,&c);
		memset(A,0,sizeof(A));
		memset(B,0,sizeof(B));
		memset(C,0,sizeof(C));
		for (int i=0;i<a;i++){
			cin>>s>>num;
			A[s-'A']=num;
		}
		for (int i=0;i<b;i++){
			cin>>s>>num;
			B[s-'A']=num;
		}
		for (int i=0;i<c;i++){
			cin>>s>>num;
			C[s-'A']=num;
		}
		int x,y;
		int flag;
		bool ans=false;
		for (x=1;x<100;x++){
			for (y=1;y<100;y++){
				flag=0;
				for (int z=0;z<30;z++){
					if (x*A[z]+y*B[z]!=C[z]){
						flag=1;
						break;
					}
				}
				if (flag==0){
					ans=true;
					break;
				}
			}
			if (ans==true)
				break;
		}
		if (ans==true)
			cout<<x<<" "<<y<<endl;
		else
			cout<<"NO"<<endl;
	}
	return 0;
}
```
