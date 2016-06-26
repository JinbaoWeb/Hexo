title: 李旻先-VC-程序设计上机测试（7）解题报告
date: 2015-12-31 22:36:08
categories: 李旻先VC++上机测试解题报告
tags: 解题报告
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/05/05/ChMkJ1XVcveIfqz4AAbOF7LtbFoAAAVOAOsYaUABs4v473.jpg)
<!--more-->
李旻先-VC-程序设计上机测试（7）解题报告
A
```objc
#include <iostream>
using namespace std;
int main(){
    int t,a,b;
    cin>>t;
    while (t--){
        cin>>a>>b;
        int *pa=&a,*pb=&b;
        if (*pa>*pb)
            cout<<*pa<<" "<<*pb<<endl;
        else
            cout<<*pb<<" "<<*pa<<endl;
    }
    return 0;
}
```
B
```objc
#include <iostream>
using namespace std;
void solve(int *a){
    int Min=min(a[0],min(a[1],a[2]));
    int Max=max(a[0],max(a[1],a[2]));
    int Mid=a[0]+a[1]+a[2]-Min-Max;
    cout<<Max<<" "<<Mid<<" "<<Min<<endl;
}
int main(){
    int t,a[3];
    cin>>t;
    while (t--){
        for (int i=0;i<3;i++)
            cin>>a[i];
        solve(a);
    }
    return 0;
}
```
C
```objc
#include <iostream>
using namespace std;
void solve(int *a,int n){
    for (int i=n-1;i>0;i--)
        cout<<a[i]<<" ";
    cout<<a[0]<<endl;
}
int main(){
    int t,n,a[1000];
    cin>>t;
    while (t--){
        cin>>n;
        for (int i=0;i<n;i++)
            cin>>a[i];
        solve(a,n);
    }
    return 0;
}
```
D
```objc
#include <iostream>
using namespace std;
int Change(int n,int k){
	int a[10];
	int cnt=0;
	while (n){
		a[cnt++]=n%10;
		n/=10;
	}
	int ans=0;
	while (cnt--){
		ans=ans*k+a[cnt];
	}
	return ans;
}
int main(){
	int a,p,b,q,t;
	cin>>t;
	while (t--){
		cin>>a>>p>>b>>q;
		int x=Change(a,p),y=Change(b,q);
		int ans=x+y;
		cout<<ans<<endl;
	}
	return 0;
}
```
E
```objc
#include <iostream>
#include <algorithm>
using namespace std;
int a[1000];
int b[1000];
bool check(int n,int a[]){
	bool flag=true;
	for (int i=1;i<n;i++){
		if (a[i]<a[i-1]){
			flag=false;
			break;
		}
	}
	return flag;
}
int main(){
	int t,n;
	cin>>t;
	while (t--){
		cin>>n;
		for (int i=0;i<n;i++){
			cin>>a[i];
			b[i]=a[i];
		}
		int l=0,r=0;
		while (check(n,a)==false){
			l++;
			if (l%2==1)
				sort(a,a+n-1);
			else
				sort(a+1,a+n);
		}
		while (check(n,b)==false){
			r++;
			if (r%2==0)
				sort(b,b+n-1);
			else
				sort(b+1,b+n);
		}
		int ans=min(l,r);
		cout<<ans<<endl;
	}
	return 0;
}
```
