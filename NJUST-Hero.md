title: NJUST Hero
date: 2016-03-05 22:52:44
categories: [ACM,NJUST]
tags: [NJUST,dp,状态压缩]
---

## Description

	There are N*N heroes standing in N rows and N columns. Everyone has a value of his ability 
	(As they are all heroes, their ability values are positive.). You are to choose some of them 
	to make a team. Of course you want to maximize the sum of their ability values. Unfortunately 
	you should not choose two heroes if they are in the same row or column, because both of them 
	see this as an insult. Now the problem comes. What’s the maximum sum of their ability values 
	you can choose?

<!--more-->

## Input

	First line contains an integer T, means there are T test cases. T will not exceed 100.
	For each case, first line contains an integer N, means there are N rows and N columns. Next 
	comes N lines, each line contains N numbers, means the ability value of each hero. The values 
	will not exceed 1000.
	For 80% of the cases, N will not exceed 5.
	For 100% of the cases, N will not exceed 16.

## Output

	For each case, print one line, containing one integer, which shows the maximum sum of ability values.

## Sample Input

	2
	2
	1 2
	2 1
	3
	1 2 3
	2 3 1
	3 1 2

## Sample Output

	4
	9

## 题意

	在n*n的矩阵中选n个数，这n个数必须保证任意两个数不在同一行且不在同一列，求这n个数的和最大。

## 解题思路

	状态压缩dp。
	状态转移方程：dp[i][s]=max(dp[i-1][s1]+a[i][j1],dp[i-1][s2]+a[i][j2],...,dp[i-1][sn]+a[i][jn]);
	dp[i][s]表示前i行，状态为s的最大值。s和s1,s2,..,sn在二进制中只有一位不同，j1,j2,...,jn表示值不同的位置
	我们用0表示列未被占，1表示列被占，那么
	第n行的状态是dp[n][111...1],
	第n-1行的状态是dp[n-1][011..1],dp[n-1][101..1],...,dp[n-1][111...0]，
	我们可以知道第n-1行的状态就可以直接转换到第n行的状态。

## 参考代码
```objc
#include <bits/stdc++.h>
using namespace std;
int t,n;
int a[20][20];
int dp[20][1<<17];
int f(int x){
	int ans=0;
	while (x){
		if (x%2==1)
			ans++;
		x/=2;
	}
	return ans;
}
int main(){
	scanf("%d",&t);
	while (t--){
		scanf("%d",&n);
		for (int i=0;i<n;i++)
			for (int j=0;j<n;j++)
				scanf("%d",&a[i][j]);
		memset(dp,0,sizeof(dp));
		for (int i=0;i<n;i++)
			dp[0][1<<i]=a[0][i];
		for (int i=1;i<n;i++){
			for (int j=0;j<(1<<n);j++){
				if (f(j)==i+1){
					int Max=-1,in=0;
					for (int k=0;k<n;k++){
						if ((j&(1<<k))>0){
							if (Max<dp[i-1][j^(1<<k)]+a[i][k]){
								Max=dp[i-1][j^(1<<k)]+a[i][k];
							}
						}
					}
					dp[i][j]=Max;
				}
			}
		}
		cout<<dp[n-1][(1<<n)-1]<<endl;
	}
	return 0;
}

```
