title: 李旻先-VC-程序设计上机测试（4）解题报告
date: 2015-12-31 22:20:13
categories: 李旻先VC++上机测试解题报告
tags: 解题报告
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/0A/05/ChMkJlZfr16IKRGvAAFsfX9-kp8AAFolQJQNKcAAWyV391.jpg)
<!--more-->
李旻先-VC-程序设计上机测试（4）解题报告
A
```objc
#include <iostream>
using namespace std;
int main(){
	int t,a,b,c;
	cin>>t;
	for (int i=0;i<t;i++){
		cin>>a>>b>>c;
		if (b*b<4*a*c){
			cout<<"NO"<<endl;
		}
		else{
			cout<<"YES"<<endl;
		}
	}
	return 0;
}
```
B
```objc
#include <iostream>
#include <fstream>
using namespace std;
int main(){
	int t,a,b;
	cin>>t;
	while (t--){
		cin>>a>>b;
		int ans=0;
		for (int j=a;j<=b;j++){
			int i=j;
			int temp=0;
			while (i){
				temp+=i%10;
				i/=10;
			}
			ans+=temp;
		}
		cout<<ans<<endl;
	}
	return 0;
}
```
C
```objc
#include <iostream>
using namespace std;
int main(){
	int t,n,m;
	cin>>t;
	while (t--){
		cin>>n>>m;
		int ans=0;
		for (int i=1;i<=n;i++){
			if (i%m!=0)
				ans+=i;
		}
		cout<<ans<<endl;
	}
	return 0;
}
```
D
```objc
#include <iostream>
#include <fstream>
using namespace std;
int main(){
	int a,b;
	int t;
	cin>>t;
	while (t--){
		cin>>a>>b;
		if (a>b)
			swap(a,b);
		int flag=0;
		for (int i=b-a;i<=a+b;i++){
			if (i==0)
				continue;
			if (a*a+i*i==b*b || a*a+b*b==i*i)
			{
				flag=1;
				cout<<i<<endl;
				break;
			}
		}
		if (flag==0)
			cout<<"NO"<<endl;
	}
	return 0;
}
```
E
```objc
#include <iostream>
#include <fstream>
using namespace std;
int f(int x){
	if (x==1 || x==0)
		return 1;
	return f(x-1)+3*f(x-2);
}
int main(){
	int t,n,m;
	cin>>t;
	while (t--){
		cin>>n;
		cout<<f(n)<<endl;
	}
	return 0;
}
```



