title: 'Codeforces Round #343 (DIV2)'
categories: [ACM,Codeforces]
tags: [Codeforces]
date: 2016-05-15 21:23:02
---
# A、Far Relative’s Birthday Cake

## 题意

> n*n矩阵 每行每列 C两两配对 共有多少种

## 解题思路

> 遍历一遍 记录每行每列C的个数 求组合数 相加

<!--more-->

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
char a[200][200];

int main(){
	int n;
	scanf("%d",&n);
	for (int i=0;i<n;i++)
		cin>>a[i];
	ll ans=0;
	for (int i=0;i<n;i++){
		int num=0;
		for (int j=0;j<n;j++){
			if (a[i][j]=='C')
				num++;
		}
		ans+=(num*(num-1)/2);
	}
	for (int i=0;i<n;i++){
		int num=0;
		for (int j=0;j<n;j++){
			if (a[j][i]=='C')
				num++;
		}
		ans+=(num*(num-1)/2);
	}
	cout<<ans<<endl;
	return 0;
}
```

# B、Far Relative’s Problem

## 题意

> 输入性别以及能搞参加聚会的时间区间,选择一天使得能参加生日聚会的人最多（并且到会的男女人数相同）

## 解题思路

> 暴力枚举1到366天,判断能够满足多少人的区间 ,注意（区分性别）ans=max(ans,min(f,m));

## 参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
struct Pe{
	char s;
	int l,r;
}P[6000];
int main(){
	int n;
	cin>>n;
	for (int i=0;i<n;i++)
		cin>>P[i].s>>P[i].l>>P[i].r;
	int ans=0;
	for (int i=1;i<367;i++){
		int f=0,m=0;
		for (int j=0;j<n;j++){
			if (P[j].l<=i && i<=P[j].r){
				if (P[j].s=='F')
					f++;
				else
					m++;
			}
		}
		int k=min(f,m);
		ans=max(ans,k);
	}
	cout<<ans*2<<endl;
	return 0;
}
```

# C、Famil Door and Brackets

## 题意

> n长的字符串有‘（’和‘）’组成，现在已知其中m长的字串，问满足任意前缀字串‘（’数量不小于‘）’数量且最后两者数量相等的原字符串的方案数。

## 解题思路

> （’看作+1，‘（’看作-1。dp[i][j]表示前i个字符，和为j(j >= 0)的方案数，然后枚举m字符串前的字符个数p，那么m后q的个数也知道，根据总和为0可以得到前后组合，这里dp[n-m-i][j+now]用到对称思想。

##参考代码

```java
import java.util.*;
import java.io.*;
 
public class Main   {
    public static final int MOD = 1000000007;
    public static void main(String[] args)  {
        Scanner cin = new Scanner (new BufferedInputStream (System.in));
        Main ma = new Main ();
        int n = cin.nextInt ();
        int m = cin.nextInt ();
        char[] str = cin.next ().toCharArray ();
        long[][] dp = new long[2005][2005];
        dp[0][0] = 1;
        for (int i=1; i<=n-m; ++i)  {
            for (int j=0; j<=i; ++j)    {
                if (j > 0)  {
                    dp[i][j] = ma.add (dp[i][j], dp[i-1][j-1]);
                }
                dp[i][j] = ma.add (dp[i][j], dp[i-1][j+1]);
            }
        }
        int mn = 10000000;
        int now = 0;
        for (int i=0; i<m; ++i)    {
            if (str[i] == '(')  now++;
            else    now--;
            if (now < mn)   mn = now;
        }
        long ans = 0;
        for (int i=0; i<=n-m; ++i)  {
            for (int j=0; j<=i; ++j)    {
                if (j + mn >= 0 && j + now <= n - m - i)    {
                    ans = ma.add (ans, dp[i][j] * dp[n-m-i][j+now] % MOD);
                }
            }
        }
        System.out.println (ans);
    }
    public long add(long a, long b)  {
        a += b;
        if (a >= MOD)   a -= MOD;
        return a;
    }
}
```

# D、Babaei and Birthday Cake

## 题意

> 求最大上升序列和

## 解题思路

> dp[i]表示前i得到的最大上升序列和，dp[i] = dp[j] + vol[i] (vol[i] > vol[j])。用线段树优化动态统计前rk[i] - 1的最大值即dp[j]，rk[i]是vol[i]离散化后的排名。

```objc
#include <bits/stdc++.h>
using namespace std;
#define lson l, mid, o<<1
#define rson mid + 1, r, o<<1|1
const double PI = acos (-1.0);
const int N = 1e5 + 5;
struct Segment_Tree 
{
    double v[N<<2], mx[N<<2];
    void push_up(int o) {
        mx[o] = std::max (mx[o<<1], mx[o<<1|1]);
    }
    void build(int l, int r, int o) {
        if (l == r) {
            v[o] = mx[o] = 0;
            return ;
        }
        int mid = l + r >> 1;
        build (lson);   build (rson);
        push_up (o);
    }
    void updata(int p, double x, int l, int r, int o)   {
        if (l == r && l == p)   {
            v[o] = mx[o] = x;
            return ;
        }
        int mid = l + r >> 1;
        if (p <= mid)   updata (p, x, lson);
        else    updata (p, x, rson);
        push_up (o);
    }
    double query(int ql, int qr, int l, int r, int o)   {
        if (ql <= l && r <= qr) {
            return mx[o];
        }
        int mid = l + r >> 1;   double ret = 0;
        if (ql <= mid)  ret = std::max (ret, query (ql, qr, lson));
        if (qr > mid)   ret = std::max (ret, query (ql, qr, rson));
        return ret;
    }
};
double dp[N];
int r[N], h[N];
double vol[N], V[N];
 
int main(void)  {
    int n;  scanf ("%d", &n);
    for (int i=0; i<n; ++i) {
        scanf ("%d%d", r + i, h + i);
        vol[i] = PI * r[i] * r[i] * h[i];
        V[i] = vol[i];
    }
    std::sort (V, V+n);
    Segment_Tree st;
    st.build (1, n, 1);
    for (int i=0; i<n; ++i) {
        int pos = std::lower_bound (V, V+n, vol[i]) - V + 1;
        if (pos == 1)   dp[i] = vol[i];
        else    dp[i] = st.query (1, pos - 1, 1, n, 1) + vol[i];
        st.updata (pos, dp[i], 1, n, 1);
    }
    double ans = 0;
    for (int i=0; i<n; ++i) {
        if (ans < dp[i])    ans = dp[i];
    }
    printf ("%.10f\n", ans);
 
    return 0;
}
```
