title: hiho1077 RMQ问题再临-线段树
date: 2016-02-16 15:33:53
categories: [ACM,hihoCoder]
tags: [hihoCoder,线段树]
---

# RMQ问题再临-线段树

## 描述

	上回说到：小Hi给小Ho出了这样一道问题：假设整个货架上从左到右摆放了N种商品，并且依次标号为1到N，每次小Hi都给出一段区间[L, R]，小Ho要做的是选出标号在这个区间内的所有商品重量最轻的一种，并且告诉小Hi这个商品的重量。但是在这个过程中，可能会因为其他人的各种行为，对某些位置上的商品的重量产生改变（如更换了其他种类的商品）。

	小Ho提出了两种非常简单的方法，但是都不能完美的解决。那么这一次，面对更大的数据规模，小Ho将如何是好呢？

<!--more-->

## 输入

	每个测试点（输入文件）有且仅有一组测试数据。

	每组测试数据的第1行为一个整数N，意义如前文所述。

	每组测试数据的第2行为N个整数，分别描述每种商品的重量，其中第i个整数表示标号为i的商品的重量weight_i。

	每组测试数据的第3行为一个整数Q，表示小Hi总共询问的次数与商品的重量被更改的次数之和。

	每组测试数据的第N+4~N+Q+3行，每行分别描述一次操作，每行的开头均为一个属于0或1的数字，分别表示该行描述一个询问和描述一次商品的重量的更改两种情况。对于第N+i+3行，如果该行描述一个询问，则接下来为两个整数Li, Ri，表示小Hi询问的一个区间[Li, Ri]；如果该行描述一次商品的重量的更改，则接下来为两个整数Pi，Wi，表示位置编号为Pi的商品的重量变更为Wi

	对于100%的数据，满足N<=10^6，Q<=10^6, 1<=Li<=Ri<=N，1<=Pi<=N, 0<weight_i, Wi<=10^4。

## 输出

	对于每组测试数据，对于每个小Hi的询问，按照在输入中出现的顺序，各输出一行，表示查询的结果：标号在区间[Li, Ri]中的所有商品中重量最轻的商品的重量。

## 样例输入

	10
	3655 5246 8991 5933 7474 7603 6098 6654 2414 884 
	6
	0 4 9
	0 2 10
	1 4 7009
	0 5 6
	1 3 7949
	1 3 1227

## 样例输出
	
	2414
	884
	7474

## 参考代码
```objc
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <math.h>
using namespace std;
const int MAXN = 1000000+10;
struct Node{
	int l,r;
	int w;
}tree[4*MAXN];
void build(int node,int l,int r){
	tree[node].l=l,tree[node].r=r;
	if (l==r){
		scanf("%d",&tree[node].w);
		return;
	}
	int mid=(l+r)/2;
	build(node*2,l,mid);
	build(node*2+1,mid+1,r);
	tree[node].w=min(tree[node*2].w,tree[node*2+1].w);
}
void update(int node,int x,int k){
	if (tree[node].l==x && x==tree[node].r){
		tree[node].w=k;
		return;
	}
	if (tree[node].l==tree[node].r)
		return;
	int mid=(tree[node].l+tree[node].r)/2;
	if (x<=mid)
		update(node*2,x,k);
	else
		update(node*2+1,x,k);
	tree[node].w=min(tree[node*2].w,tree[node*2+1].w);
}
int query(int node,int l,int r){
	if (l<=tree[node].l && tree[node].r<=r){
		return tree[node].w;
	}
	int mid=(tree[node].l+tree[node].r)/2;
	if (r<=mid)
		return query(node*2,l,r);
	else if (mid<l)
		return query(node*2+1,l,r);
	else
		return min(query(node*2,l,mid),query(node*2+1,mid+1,r));
}
int main(){
	int n,q;
	int p,L,R,x,v;
	while (~scanf("%d",&n)){
		build(1,1,n);
		scanf("%d",&q);
		while (q--){
			scanf("%d",&p);
			if (p==0){
				scanf("%d%d",&L,&R);
				printf("%d\n",query(1,L,R));
			}
			else{
				scanf("%d%d",&x,&v);
				update(1,x,v);
			}
		}
	}

	return 0;
}
```
