title: Educational Codeforces Round 10
categories: [ACM,Codeforces]
tags: [Codeforces]
date: 2016-05-15 21:40:35
---
# A、Gabriel and Caterpillar

## 题意

>在一棵树上，虫子要吃苹果，虫子在h1的高度，苹果在h2的高度，虫子白天可以往上爬a米/小时，晚上会以b米/小时后退问虫子要几天才能吃到苹果。白天的时间为10am-10pm,虫子从第0天2pm开始爬。

## 解题思路

>我们可以找到这几个时间,其高度对应为：
>2pm --- 10pm --- 10am --- 2pm --- 10pm --- 10am --- 2pm...
>x1  ---  x2  ---  x3  --- x4  ---  x5  ---  x6  --- x7...
>x1=h1;
>x2=x1+8*a;
>x3=x2-12*b;
>x4=x3+4*a;
>x5=x4+8*a;
>x6=x5-12*b;
>x7=x6+4*a;
>...
>所以在一天内x2为最高位置，我们只需要对x2的增量进行判断就行。

<!--more-->

## 参考代码
```objc
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int main(){
	int h1,h2,a,b;
	while (cin>>h1>>h2){
		cin>>a>>b;
		int x1=h1;
		int x2=x1+8*a;
		int x3=x2-12*b;
		int x4=x3+4*a;
		if (h2>=h1){
			if (x1>=x4 && x2<h2){
				cout<<-1<<endl;
				continue;
			}
			if (x2>=h2){
				cout<<0<<endl;
				continue;
			}
			int h=12*(a-b);
			int ans=(h2-x2)/h+((h2-x2)%h==0?0:1);
			cout<<ans<<endl;
		}
		else{
			if (x3>h2 && x4>=x1){
				cout<<-1<<endl;
				continue;
			}
			if (x3<=h2){
				cout<<0<<endl;
				continue;
			}
			int h=12*(b-a);
			int ans=(x3-h2)/h+((x3-h2)%h==0?0:1);
			cout<<ans<<endl;
		}
	}

	return 0;
}
```

# B、z-sort

## 题意

>z-sorted必须满足i为偶数，a[i]>=a[i-1],i为奇数，a[i]<=a[i-1]。将一个数组组成这个z-sorted数组。

## 解题思路

>将数组排序，第一个数跟最后一个数结合，第二个数根倒数第二个数结合，...，输出即可。

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int a[2000];
int main(){
	int n;
	while (cin>>n){
		for (int i=0;i<n;i++){
			cin>>a[i];
		}
		sort(a,a+n);
		for (int i=0;i*2<n;i++){
			if (n%2==1 && i==n/2)
				cout<<a[i]<<endl;
			else if (n%2==0 && i==n/2)
				cout<<a[i]<<" "<<a[n-1-i]<<endl;
			else
				cout<<a[i]<<" "<<a[n-1-i]<<" ";
		}

	}

	return 0;
}
```

# C、Foe Pairs

## 题意

>在一个数组[0...n]里面，有一些集合{x,y}，你可以从数组[0...n]里面选出一些子数组[a...b],使得子数组里面不包含这些集合，问a和b的选择有多少种选法？

## 解题思路

>预处理出这些集合所在的位置x和y，那么在[0...x]和[y...n]分别取一个a和一个b，这些选法都会包含集合.于是问题就转换为矩形的左下角[0,y],右上角[x,n]的面积。每个集合都对应一个矩形，即求所有矩形的面积并。
>线段树+扫描线+离散化

## 参考代码

```objc
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;
typedef long long ll;
#define lz 2*u,l,mid
#define rz 2*u+1,mid+1,r
const int maxn=3000010;
int sum[2*maxn];
int flag[2*maxn];
int X[2*maxn];
int a[maxn];
int b[maxn];
struct Node
{
    int lx, rx, y;
    int s;
    Node(){};
    Node(int lx_, int rx_, int y_, int s_)
    {
        lx=lx_, rx=rx_, y=y_, s=s_;
    }
    bool operator <(const Node &S) const
    {
        return y<S.y;
    }
}line[maxn];
int find(int tmp, int n)
{
    int l=1, r=n, mid;
    while(l<=r)
    {
        mid=(l+r)>>1;
        if(X[mid]==tmp) return mid;
        else if(X[mid]<tmp) l=mid+1;
        else r=mid-1;
    }
}
void push_up(int u, int l, int r)
{
    if(flag[u]) sum[u]=X[r+1]-X[l];
    else if(l==r) sum[u]=0;
    else sum[u]=sum[2*u]+sum[2*u+1];
}
void Update(int u, int l, int r, int tl, int tr, int c)
{
    if(tl<=l&&r<=tr)
    {
        flag[u]+=c;
        push_up(u,l,r);
        return ;
    }
    int mid=(l+r)>>1;
    if(tr<=mid) Update(lz,tl,tr,c);
    else if(tl>mid) Update(rz,tl,tr,c);
    else
    {
        Update(lz,tl,mid,c);
        Update(rz,mid+1,tr,c);
    }
    push_up(u,l,r);
}
int main()
{
    int n,m; 
    while (~scanf("%d%d",&n,&m)){
        int num=0;
        memset(flag,0,sizeof(flag));
        memset(sum,0,sizeof(sum));
        for (int i=1;i<=n;i++){
            scanf("%d",&a[i]);
            b[a[i]]=i;
        }
        for (int i=0;i<m;i++){
            int x,y;
            scanf("%d%d",&x,&y);
            int ix=b[x],iy=b[y];
            if (ix>iy) swap(ix,iy);
            int x1=0,x2=ix,y1=iy-1,y2=n;
            line[++num]=Node(x1,x2,y1,1);
            X[num]=x1;
            line[++num]=Node(x1,x2,y2,-1);
            X[num]=x2;
        }
        sort(X+1,X+num+1);
        sort(line+1,line+num+1);
        int k=1;
        for(int i=2; i<=num; i++)
            if(X[i]!=X[i+1]) X[++k]=X[i];
        ll ans=0;
        for(int i=1; i<num; i++)
        {
            int l=find(line[i].lx,k);
            int r=find(line[i].rx,k)-1;
            Update(1,1,k,l,r,line[i].s);
            ans+=1LL*sum[1]*(line[i+1].y-line[i].y);
        }
        ll temp=1LL*n*(n+1)/2;
        ans=temp-ans;
        cout<<ans<<endl;
    }
    return 0;
}
```

# D、Nested Segments

## 题意

>有一些线段，求每个线段包含了几个其他的线段

## 解题思路

>将线段的头尾坐标转换为二维坐标，求在它右下方的点有多少个？按y轴升序排序，依次更新x坐标的值。

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
#define N 400000+10
struct Node{
	int x,y;
	int id;
}P[N];
int ans[N];
int a[N];
int b[N];
int c[N];
bool cmp(Node s1,Node s2){
	if (s1.y!=s2.y)
		return s1.y<s2.y;
	return s1.x<s2.x;
}
int lowbit(int x)
{
    return x & (-x);
}
void modify(int x,int add)//一维
{  
    while(x<=N)  
    {      
        c[x]+=add;    
        x+=lowbit(x); 
    }
}
int get_sum(int x)
{  
    int ret=0; 
    while(x!=0)  
    {       
        ret+=c[x];   
        x-=lowbit(x);   
    }  
    return ret;
}
int main(){
	int n;
	while (~scanf("%d",&n)){
		memset(c,0,sizeof(c));
		for (int i=0;i<2*n;i++){
			cin>>a[i];
			b[i]=a[i];
		}
		sort(b,b+n*2);
		int cnt=unique(b,b+n*2)-b;
		for (int i=0;i<2*n;i+=2){
			int x=lower_bound(b,b+cnt,a[i])-b+1;
			int y=lower_bound(b,b+cnt,a[i+1])-b+1;
			P[i/2].x=x,P[i/2].y=y,P[i/2].id=i/2;
		}
		sort(P,P+n,cmp);
		for (int i=0;i<n;i++){
			ans[P[i].id]=get_sum(N)-get_sum(P[i].x-1);
			modify(P[i].x,1);
		}
		for (int i=0;i<n;i++){
			cout<<ans[i]<<endl;
		}
		cout<<endl;
	}
	return 0;
}
```