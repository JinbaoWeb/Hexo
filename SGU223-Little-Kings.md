title: SGU223 Little Kings
categories: [ACM,SGU]
tags: [SGU,dp,状态压缩]
date: 2016-03-15 15:34:29
---

	After solving nice problems about bishops and rooks, Petya decided that he would like to learn to 
	play chess. 
	He started to learn the rules and found out that the most important piece 
	in the game is the king. 
	The king can move to any adjacent cell (there are up to eight such cells). 
	Thus, two kings are in the attacking position, if they are located on the adjacent cells. 
	Of course, the first thing Petya wants to know is the number of ways one 
	can position k kings on a chessboard of 
	size n × n so that no two of them are in the attacking position. Help him! 

<!--more-->

## Input

	The input file contains two integers n (1 ≤ n ≤ 10) and k (0 ≤ k ≤ n2). 

## Output

	Print a line containing the total number of ways one can put the given number of kings on a chessboard of 
	the given size so that no two of them are in attacking positions. 

## Sample test(s)

## Input
Test #1 

	3 2 

Test #2 

	4 4 

## Output
Test #1 

	16 

Test #2 

	79 

## 题意

	一个尺寸为n×n的棋盘，上面放k个国王。每个国王的攻击范围为周围一圈的8个格。
	现在问你尺寸n×n的棋盘放k个国王有多少种放置方法？(1 ≤ n ≤ 10，k<=n*n)

## 解题思路

	状态转移方程：dp[i][curstate][k]=sum(dp[i-1][prestatue][k-c[curstate]])
	我们用0和1表示格子内不放和放国王，那么对于同一行我们可以DFS出所有的符合条件的状态（即10001001、10010010等），
	然后我们从上往下递推，只要满足所有的1互不攻击，例如
	10001001 （s1状态）
	00100000 （s2状态）
	这两个状态是互不攻击的，我们可以通过(s1&s2)、(s1&(s2<<1))和(s1&(s2>>1)来判断状态是否相容。
	我们对于每一行枚举所有符合条件的状态s1，然后再枚举所有和s1相容的状态s1即可。

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define MAXN 11
int s[1<<MAXN],c[1<<MAXN];
ll dp[MAXN][1<<MAXN][MAXN*MAXN];
int n,k,cnt;
void DFS(int r,int st,int v)
{
	if (r==n)
	{
		s[++cnt]=st;
		c[cnt]=v;
		return;
	}
	DFS(r+1,st<<1,v);
	if (!(st&1))
		DFS(r+1,st<<1|1,v+1);
}
bool check(int s1,int s2)
{
	if ((s1&s2) || (s1&(s2<<1)) || (s1&(s2>>1))) 
		return false;
	return true;
}
int main()
{
	while (~scanf("%d%d",&n,&k))
	{
		memset(dp,0,sizeof(dp));
		cnt=0;
		DFS(0,0,0);
		dp[0][1][0]=1;
		for (int r=1;r<=n;r++)
			for (int i=1;i<=cnt;i++)
				for (int j=1;j<=cnt;j++)
					for (int q=0;q<=k;q++)
						if ((q-c[i]>=0) && check(s[i],s[j]))
							dp[r][i][q]+=dp[r-1][j][q-c[i]];
		ll ans=0;
		for (int i=1;i<=cnt;i++)
			ans+=dp[n][i][k];
		cout<<ans<<endl;
	}
	return 0;
}
```
	

