title: TopCoder SRM 685 (DIV2)
categories: [ACM,TopCoder]
tags: [TopCoder]
date: 2016-05-15 22:13:27
---
# DoubleWeights

## 题意

>给一张有向图，每条边有两个值w1,w2，要求找一条从0→1的路径，使得∑w1∗∑w2最小。

<!--more-->

## 解题思路

>DFS暴力找出所有的路径，取答案的最小值。

## 参考代码
```objc
#include <bits/stdc++.h>
using namespace std;
int w1[30][30],w2[30][30];
bool used[30];
int ans,n;
void DFS(int i,int x,int y){
	if (i==1){
		ans=min(ans,x*y);
		return;
	}
	if (x*y>ans) return; //剪枝
	used[i]=true;
	for (int j=0;j<n;j++){
		if (w1[i][j] && used[j]==false){
			DFS(j,x+w1[i][j],y+w2[i][j]);
		}
	}
	used[i]=false;
}
class DoubleWeights{
	public:
	int minimalCost(vector <string> weight1, vector <string> weight2){
		n=weight1.size();
		memset(used,false,sizeof(used));
		for (int i=0;i<n;i++){
			for (int j=0;j<n;j++){
				if (weight1[i][j]=='.') w1[i][j]=0;
				else w1[i][j]=weight1[i][j]-'0';
			}
		}
		for (int i=0;i<n;i++){
			for (int j=0;j<n;j++){
				if (weight2[i][j]=='.') w2[i][j]=0;
				else w2[i][j]=weight2[i][j]-'0';
			}
		}
		ans=(1<<30);
		DFS(0,0,0);
		if (ans==(1<<30))
			return -1;
		return ans;
	}	
};
```

# MultiplicationTable2Easy

## 题意

>在一个矩形table[][]里面有一些数，一个数组t[]里面有一些数，如果在数组t里面任取两个数（可重复取）x,y，这两个数构成table[x][y]数在t[]内,那么返回“Good”，否则返回“Not Good”。

## 参考代码
```objc
#include <bits/stdc++.h>
using namespace std;
class MultiplicationTable2Easy{
	public:
	string isGoodSet(vector <int> table, vector <int> t){
		int n=sqrt(1.0*table.size());
		for (int i=1;i<=t.size();i++){
			for (int j=1;j<=t.size();j++){
				int x=(t[i]-1)*n+j;
				int flag=0;
				for (int k=0;k<t.size();k++){
					if (table[x]==t[k]){
						flag=1;
						break;
					}
				}
				if (flag==0)
					return "Not Good";
			}
		}
		return "Good";
	}
};
```

