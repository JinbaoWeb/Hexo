title: 李旻先-VC-程序设计上机测试（9）解题报告
date: 2015-12-31 23:24:57
categories: 李旻先VC++上机测试解题报告
tags: 解题报告
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/05/05/ChMkJlXVcvuIQAx3AAOoeosc8qkAAAVOQIHY9QAA6iS736.jpg)
<!--more-->
李旻先-VC-程序设计上机测试（9）解题报告
A
```objc
#include <iostream>
#include <string.h>
using namespace std;
void getSub(char *str,char *s,int a,int b)
{
	//从字符串str里面截取出s
	int j=0;
	for (int i=a;i<=b;i++)	
		s[j++]=str[i];
	s[j]=0;
}
int main()
{
	int t,a,b;
	cin>>t;
	while (t--){
		char *str=new char[100];
		char *s=new char[100];
		cin>>str;
		cin>>a>>b;
		getSub(str,s,a,b);
		cout<<s<<endl;
		delete str;
		delete s;
	}
	return 0;
}
```
B
```objc
#include <iostream>
#include <string.h>
using namespace std;
void decompose(char *str,char *a,char *b)
{
	//将字符串str还原成字符串a和字符串b	
	int len=strlen(str);
	int x=0,y=0;
	for (int i=0;i<len;i++){
		if (i%2==0)
			a[x++]=str[i];
		else
			b[len/2-1-y++]=str[i];
	}
	a[len/2]=b[len/2]=0;
}
int main(){
	int t;
	cin>>t;
	while (t--){
		char *str=new char[100];
		char *a=new char[100];
		char *b=new char[100];
		cin>>str;
		decompose(str,a,b);
		cout<<a<<endl<<b<<endl;
	}
	return 0;
}
```
C
```objc
#include <iostream>
using namespace std;
bool check(int *a,int n)
{
    //判断是否存在
    for (int i=0;i<n;i++){
    	for (int j=0;j<n;j++){
    		if (j==i) continue;
    		for (int k=0;k<n;k++){
    			if (k==i || k==j) continue;
    			if (a[i]-a[j]==a[k])
    				return true;
    		}
    	}
    }
    return false;
}
int main(){
	int t,n;
	cin>>t;
	while (t--){
		cin>>n;
		int *a=new int[n];
		for (int i=0;i<n;i++)
			cin>>a[i];
		if (check(a,n)==true)
			cout<<"YES"<<endl;
		else
			cout<<"NO"<<endl;
	}
	return 0;
}
```
D
```objc
#include <iostream>
#include <string.h>
using namespace std;
void encrypt(char *str, char *s) 
{ 
    //把原文字符串str加密后存入字符串s
    int len=strlen(str);
    int cnt=0;
    for (int i=0;i<len;i++){
        int ans=str[i]-24;
        int temp[32];
        int num=0;
        while (ans){
            temp[num++]=ans%10;
            ans/=10;
        }
        while (num--){
            s[cnt++]=temp[num]+'0';
        }
    }
    s[cnt]=0;
} 
int main(){
    int t;
    cin>>t;
    while (t--){
        char *str=new char[100];
        char *s=new char[200];
        cin>>str;
        encrypt(str,s);
        cout<<s<<endl;
    }
    return 0;
}
```
E
```objc
#include<iostream>
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
#include<math.h>
#include<algorithm>
using namespace std;
struct point
{
    int x;
    int y;
    int z;
}p[5];
int dis(point a,point b)
{
    return (a.x-b.x)*(a.x-b.x)+(a.y-b.y)*(a.y-b.y)+(a.z-b.z)*(a.z-b.z);
}
int cheng(point a,point b,point c)
{
    return (a.x-b.x)*(c.x-a.x)+(a.y-b.y)*(c.y-a.y)+(a.z-b.z)*(c.z-a.z);
}
int fun(int a,int b,int c)
{
    if((a==b&&a+b==c)||(a==c&&a+c==b)||(c==b&&c+b==a)) return 1;
    else return 0;
}
int judge()
{
    int a,b,c,a2,b2,c2,a3,b3,c3,t;
    a=dis(p[0],p[1]),b=dis(p[0],p[2]),c=dis(p[0],p[3]);
    a2=dis(p[1],p[0]),b2=dis(p[1],p[2]),c2=dis(p[1],p[3]);
    a3=dis(p[2],p[0]),b3=dis(p[2],p[1]),c3=dis(p[2],p[3]);
    if(fun(a,b,c)&&fun(a2,b2,c2)&&fun(a3,b3,c3))
    {
        int ab,bc,ac;
        ab=cheng(p[0],p[1],p[2]);
        bc=cheng(p[1],p[2],p[0]);
        ac=cheng(p[2],p[0],p[1]);
        if(ab==0||bc==0||ac==0) return 1;
    }
    return 0;
}
int main()
{
    int i,k,t;
    cin>>t;
    for(k=1;k<=t;k++)
    {
        for(i=0;i<4;i++) cin>>p[i].x>>p[i].y>>p[i].z;
        if (judge())
            cout<<"Yes"<<endl;
        else
            cout<<"No"<<endl;
    }
    return 0;
}
```
