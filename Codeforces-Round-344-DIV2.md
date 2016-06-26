title: 'Codeforces Round #344 (DIV2)'
categories: [ACM,Codeforces]
tags: [Codeforces]
date: 2016-05-15 21:32:37
---
# A、Interview

## 题意

>给出两组一样长的数组A0~n-1 B0~n-1 求A中连续元素 按位或(or)的最大值与 B中连续元素 按位或(or)的最大值的和

## 解题思路

>或运算的话遇到一个新的数只増或不变，不会减，所以直接把所有数按位或，之后求和即可

<!--more-->

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int a[10005],b[10005];
int ans[1005][1005];
int ans2[1005][1005];
int main(){
	int n;
	cin>>n;
	for (int i=0;i<n;i++){
		cin>>a[i];
		ans[i][i]=a[i];
	}

	for (int i=0;i<n;i++){
		cin>>b[i];
		ans2[i][i]=b[i];
	}
	if (n==1){
		cout<<1LL*a[0]+b[0]<<endl;
		return 0;
	}
	ll Max=-1;
	for (int i=0;i<n;i++){
		for (int j=i+1;j<n;j++){
			ans[i][j]=ans[i][j-1]|a[j];
		}
	}
	for (int i=0;i<n;i++){
		for (int j=i+1;j<n;j++){
			ans2[i][j]=ans2[i][j-1]|b[j];
		}
	}

	for (int i=0;i<n;i++){
		for (int j=i+1;j<n;j++){
			Max=max(Max,1LL+ans[i][j]+ans2[i][j]);
		}
	}

	cout<<Max-1<<endl;
	return 0;
}

```

# B、Print Check

## 题意

>在一个n*m的矩形中，初始矩形内的所有颜色都是0，现有n个操作，操作分两种，一是将一行涂一个颜色，二是将一列涂一个颜色，求最后矩形的颜色。

## 解题思路

>设置优先级，对每一行，先记录被覆盖的颜色和优先级，对于每一列也记录覆盖的颜色和优先级，然后对每一个小矩形，根据行和列的优先级判断该小矩形是被行覆盖还是被列覆盖。

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
struct Node{
	int col,val;
}L[5005],R[5005];
int main(){
	int n,m,k,op,x,y;
	cin>>n>>m>>k;
	for (int i=0;i<5005;i++){
		L[i].col=0,L[i].val=0;
		R[i].col=0,R[i].val=0;
	}
	for (int i=1;i<=k;i++){
		cin>>op>>x>>y;
		if (op==1){
			L[x].col=y;
			L[x].val=i;
		}
		else{
			R[x].col=y;
			R[x].val=i;
		}
	}
	for (int i=1;i<=n;i++){
		for (int j=1;j<m;j++){
			if (L[i].val>R[j].val)
				cout<<L[i].col<<" ";
			else
				cout<<R[j].col<<" ";
		}
		if (L[i].val>R[m].val)
			cout<<L[i].col<<endl;
		else
			cout<<R[m].col<<endl;
		
	}
	return 0;
}
```


