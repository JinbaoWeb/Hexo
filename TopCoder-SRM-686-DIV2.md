title: TopCoder SRM 686 (DIV2)
categories: [ACM,TopCoder]
tags: [TopCoder]
date: 2016-05-15 22:17:21
---
# SegmentsAndPoints

## 题意

>有n条线段和n个点，每个点要在一条线段内，一条线段只能被一个点使用，问n条线段和n个点能不能匹配？

<!--more-->

## 解题思路

>对线段按照右端点升序排序，点按照升序排序，然后对每个点寻找是否存在线段包含点，如果有一个不存在，输出“Impossible”，如果都存在，输出“Possible”。

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
int n;
struct Node
{
	int l,r;
}P[105];
bool cmp(Node x,Node y)
{
	if (x.r!=y.r)
		return x.r<y.r;
	return x.l<y.l;
}
bool used[105];
class SegmentsAndPoints
{
	public:
	string isPossible(vector <int> p, vector <int> l, vector <int> r)
	{
		n=p.size();
		for (int i=0;i<n;i++)
			P[i].l=l[i],P[i].r=r[i];
		sort(P,P+n,cmp);
		sort(p.begin(),p.end());
		memset(used,false,sizeof(used));
		for (int i=0;i<n;i++)
		{
			int flag=0;
			for (int j=0;j<n;j++)
			{
				if (used[j]==true) continue;
				if (P[j].l<=p[i] && p[i]<=P[j].r)
				{
					used[j]=true;
					flag=1;
					break;
				}
			}
			if (flag==0)
				return "Impossible";
		}
		return "Possible";
	}	
};
```

# TreeAndVertex

## 题意

>一个有n个点n-1条边的树，你从这n个点中去除一个点，问最多可以构成几颗树？

## 解题思路

>并查集，枚举每个点，计算去除每个点后构成树的数量，取最大值。

## 参考代码
```objc
#include <bits/stdc++.h>
using namespace std;
const int MAXN = 1000;
int father[MAXN];
int n;
void Init()
{
    for (int i = 0; i <= n; ++i){
        father[i] = i;
    }
}

int getfather(const int &i)
{
    int r = i;
    while(r != father[r]) r = father[r];
    return r;
}

void merge(const int &i, const int &j)
{
    int x = getfather(i);
    int y = getfather(j);

    if (x != y)
        father[x] = y;
}
bool used[100];
class TreeAndVertex
{
	public:
	int get(vector <int> tree)
	{
		n=tree.size();
		int ans=0;
		for (int i=0;i<=n;i++)
		{
			Init();
			for (int j=1;j<=n;j++)
			{
				if (tree[j-1]==i || j==i)
					continue;
				merge(tree[j-1],j);
			}
			memset(used,false,sizeof(used));
			int k=0;
			for (int j=0;j<=n;j++)
			{
				father[j]=getfather(j);
				if (used[father[j]]==false){
					k++;
					used[father[j]]=1;
				}
			}
			k--;
			ans=max(ans,k);
		}
		return ans;
	}
};
```
