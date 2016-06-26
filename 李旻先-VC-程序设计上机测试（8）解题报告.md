title: 李旻先-VC-程序设计上机测试（8）解题报告
date: 2015-12-31 22:41:46
categories: 李旻先VC++上机测试解题报告
tags: 解题报告
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/05/05/ChMkJlXVcviIYiWBAARgwiVRfWYAAAVOQBfd4kABGDa618.jpg)
<!--more-->
李旻先-VC-程序设计上机测试（8）解题报告
A
```objc
#include <iostream>
using namespace std;
int a[1000];
void min(int &Min,int &x){
	if (x<Min)
		Min=x;
}
int main(){
	int n,t;
	cin>>t;
	while (t--){
		cin>>n;
		for (int i=0;i<n;i++){
			cin>>a[i];
		}
		int Min=a[0];
		for (int i=1;i<n;i++)
			min(Min,a[i]);
		cout<<Min<<endl;
	}
	return 0;
}
```
B
```objc
#include <iostream>
#include <string.h>
using namespace std;
int main(){
	int t;
	char str[1000];
	cin>>t;
	while (t--){
		cin>>str;
		int len=strlen(str);
		for (int i=0;i<len;i++){
			if ('A'<=str[i] && str[i]<='Z')
				str[i]=str[i]-'A'+'a';
		}
		cout<<str<<endl;
	}
	return 0;
}
```
C
```objc
#include <iostream>
#include <algorithm>
using namespace std;
int a[1000];
int main(){
	int n,t;
	cin>>t;
	while (t--){
		cin>>n;
		for (int i=0;i<n;i++){
			cin>>a[i];
		}
		sort(a,a+n);
		for (int i=0;i<n-1;i++)
			cout<<a[i]<<" ";
		cout<<a[n-1]<<endl;
	}
	return 0;
}
```
D
```objc
#include <iostream>
#include <string.h>
using namespace std;
int main(){
	int t;
	char str[1000];
	int b[1000];
	cin>>t;
	while (t--){
		cin>>str;
		int len=strlen(str);
		int cnt=0;
		int num=0;
		for (int i=0;i<len;i++){
			if ('0'<=str[i] && str[i]<='9')
				num=num*10+str[i]-'0';
			else{
				if (num)
					b[cnt++]=num;
				num=0;
			}
		}
		if (num)
			b[cnt++]=num;
		cout<<cnt<<endl;
		for (int i=0;i<cnt-1;i++)
			cout<<b[i]<<" ";
		cout<<b[cnt-1]<<endl;
	}
	return 0;
}
```
E
```objc
#include <iostream>
#include <string.h>
using namespace std;
struct Node{
	char name[20];
	int num;
}P[1000];
int main(){
	int t,n,m;
	cin>>t;
	while (t--){
		cin>>n;
		for (int i=0;i<n;i++)
			cin>>P[i].name>>P[i].num;
		cin>>m;
		while (m--){
			int a,b,c;
			char temp[20];
			cin>>a;
			if (a==1){
				cin>>temp;
				for (int i=0;i<n;i++){
					if (strcmp(temp,P[i].name)==0){
						cout<<P[i].num<<endl;
						break;
					}
				}
			}
			else{
				cin>>b>>c;
				int ans=0;
				for (int i=0;i<n;i++){
					if (P[i].num<=c && P[i].num>=b)
						ans++;
				}
				cout<<ans<<endl;
			}
		}
		
	}
	return 0;
}
```