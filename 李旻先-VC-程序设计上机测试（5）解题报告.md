title: 李旻先-VC-程序设计上机测试（5）解题报告
date: 2015-12-31 22:25:50
categories: 李旻先VC++上机测试解题报告
tags: 解题报告
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/0A/05/ChMkJlZfr2WIE60dAAPEYoVVOboAAFolgK4_hgAA8R6803.jpg)
<!--more-->
李旻先-VC-程序设计上机测试（5）解题报告
A
```objc
#include <iostream>
using namespace std;
int abs(int x){
	if (x<0)
		return -x;
	else
		return x;
}
int main(){
	int t,a,b;
	cin>>t;
	while (t--){
		cin>>a>>b;
		cout<<abs(a-b)<<endl;
	}
	return 0;
}
```
B
```objc
#include <iostream>
using namespace std;
#define N 10000
int main(){
	int t,n;
	int a[N];
	cin>>t;
	while (t--){
		cin>>n;
		for (int i=0;i<n;i++)
			cin>>a[i];
		int min=a[0];
		for (int i=1;i<n;i++){
			if (a[i]<min)
				min=a[i];
		}
		cout<<min<<endl;
	}
	return 0;
}
```
C
```objc
#include <iostream>
using namespace std;
int fib(int n){
	if (n==0)
		return 1;
	return 2*fib(n-1);
}
int main(){
	int t,n;
	cin>>t;
	while (t--){
		cin>>n;
		cout<<fib(n-1)<<endl;
	}
	return 0;
}
```
D
```objc
#include <iostream>
using namespace std;
bool isprime(int x){
	if (x<2)
		return false;
	if (x==2 || x==3 || x==5 || x==7)
		return true;
	for (int i=2;i*i<=x;i++){
		if (x%i==0){
			return false;
		}
	}
	return true;
}
int main(){
	
	int a,b,t;
	cin>>t;
	while (t--){
		cin>>a>>b;
		int ans=0;
		for (int i=a;i<=b;i++){
			if (isprime(i)==true){
				ans++;
			}
		}
		cout<<ans<<endl;
	}
	return 0;
}
```
E
```objc
#include <iostream>
#include <string.h>
using namespace std;
int a[1005];
int main(){
	int t,n,x;
	cin>>t;
	while (t--){
		cin>>n;
		memset(a,0,sizeof(a));
		for (int i=0;i<n;i++){
			cin>>x;
			a[x]++;
		}
		int ans=0;
		for (int i=0;i<1005;i++){
			ans=max(ans,a[i]);
		}
		cout<<ans<<endl;
	}
	return 0;
}
```
