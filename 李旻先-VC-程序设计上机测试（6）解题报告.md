title: 李旻先-VC-程序设计上机测试（6）解题报告
date: 2015-12-31 22:30:48
categories: 李旻先VC++上机测试解题报告
tags: 解题报告
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/0A/05/ChMkJ1Zfr2aIYxcgAAUGz0IjIB8AAFolgNFWgEABQbn563.jpg)
<!--more-->
李旻先-VC-程序设计上机测试（6）解题报告
A
```objc
#include <iostream>
using namespace std;
#define N 5
int Cal(int a[]){
     int sum=0;
for (int i=0;i<5;i++){
sum+=a[i];
}
return sum/5+(sum%5>2?1:0);
}
int main(){
	int t;
	int a[N];
	cin>>t;
	while (t--){
		for (int i=0;i<5;i++){
			cin>>a[i];
		}
        int ans=Cal(a);
        cout<<ans<<endl;
	}
	return 0;
}
```
B
```objc
#include <iostream>
#include <string.h>
using namespace std;
char s[10000];
int main(){
    int t;
    cin>>t;
    while (t--){
        cin>>s;
        int len=strlen(s);
        for (int i=0;i<len;i++)
            cout<<s[i]<<endl;

    }
    return 0;
}
```
C
```objc
#include <iostream>
#include <string.h>
using namespace std;
#define N 1000
int main(){
	int t;
	char s[N];
	cin>>t;
	cin.getline(s,N);
	while (t--){
		cin.getline(s,N);
		int len=strlen(s);
		for (int i=0;i<len;i++){
			if (s[i]==' ')
				s[i]='#';
		}
		cout<<s<<endl;
	}
	return 0;
}
```
D
```objc
#include <iostream>
using namespace std;
int a[101][101];
int main(){
	int x,y,t,n,m;
	cin>>t;
	while (t--){
		cin>>n>>m;
		int Max=-1;
		for (int i=0;i<n;i++){
			for (int j=0;j<m;j++){
				cin>>a[i][j];
				if (a[i][j]>Max){
					Max=a[i][j];
				}
			}
		}
		cout<<Max<<endl;
	}
	return 0;
}
```
E
```objc
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
using namespace std;
char str[1000];
int main(){
	char s[12]={'T','h','a','n','k','s','g','i','v',' ','D','y'};
	int a[20];
	int t;
	cin>>t;
	getchar();
	while (t--){
		cin.getline(str,1000);
		int len=strlen(str);
		memset(a,0,sizeof(a));
		for (int i=0;i<len;i++){
			for (int j=0;j<12;j++){
				if (s[j]==str[i]){
					a[j]++;
					break;
				}
			}
		}
		int ans=10000;
		for (int i=0;i<12;i++){
			ans=min(ans,a[i]);
		}
		cout<<ans<<endl;
	}
	return 0;
}
```