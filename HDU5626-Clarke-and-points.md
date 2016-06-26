title: HDU5626 Clarke and points
date: 2016-02-14 16:43:31
categories: [ACM,HDU]
tags: [HDU]
---
<!--more-->
# Clarke and points

## Problem Description

	Clarke is a patient with multiple personality disorder. One day he turned into a learner of geometric. 
	He did a research on a interesting distance called Manhattan Distance. 
	The Manhattan Distance between point A(xA,yA) and point B(xB,yB) is |xA−xB|+|yA−yB|. 
	Now he wants to find the maximum distance between two points of n points.
 
<!--more-->

## Input

	The first line contains a integer T(1≤T≤5), the number of test case. 
	For each test case, a line followed, contains two integers n,seed(2≤n≤1000000,1≤seed≤109), 
	denotes the number of points and a random seed. 
	The coordinate of each point is generated by the followed code. 


```objc
long long seed;
inline long long rand(long long l, long long r) {
  static long long mo=1e9+7, g=78125;
  return l+((seed*=g)%=mo)%(r-l+1);
}

// ...

cin >> n >> seed;
for (int i = 0; i < n; i++)
  x[i] = rand(-1000000000, 1000000000),
  y[i] = rand(-1000000000, 1000000000);
```
 

## Output

	For each test case, print a line with an integer represented the maximum distance.
 

## Sample Input

	2
	3 233
	5 332

## Sample Output

	1557439953
	1423870062
 

## 参考代码
```objc
#include <bits/stdc++.h>
using namespace std;
#define MAXN 1000000
int n;
long long seed,x,y;
inline long long rand(long long l, long long r) {
	static long long mo=1e9+7, g=78125;
	return l+((seed*=g)%=mo)%(r-l+1);
}
void solve(){
	cin >> n >> seed;
	long long max_X = -1e17, max_Y = -1e17;
    long long min_X = 1e17,min_Y = 1e17;
	for (int i = 0; i < n; i++){
		x = rand(-1000000000, 1000000000);
		y = rand(-1000000000, 1000000000);
		max_X = max(max_X , x + y);
        max_Y = max(max_Y , x - y);
        min_X = min(min_X , x + y);
        min_Y = min(min_Y , x - y);
	}
	cout<<max(max_X - min_X, max_Y - min_Y)<<endl;
}
int main(){
	int t;
	scanf("%d",&t);
	while (t--){
		solve();
	}
	return 0;
}
```