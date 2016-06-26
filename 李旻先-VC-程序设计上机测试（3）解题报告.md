title: 李旻先-VC-程序设计上机测试（3）解题报告
date: 2015-12-31 22:11:04
categories: 李旻先VC++上机测试解题报告
tags: 解题报告
---
![](http://desk.fd.zol-img.com.cn/t_s1024x768c5/g5/M00/0A/05/ChMkJ1Zfr2GIPcUDAA4sge6qvA4AAFolQPYSd8ADiyZ655.jpg)
<!--more-->
李旻先-VC-程序设计上机测试（3）解题报告
A
```objc
#include <iostream> 
using namespace std; 
int main()
{ 
	int t,a,b;
	cin>>t; 
	for (int i=1;i<=t;i++)
	{
		cin>>a>>b; 
		cout<<a<<" + "<<b<<" = "<<a+b<<endl; 
	} 
	return 0; 
}
```
B
```objc
#include <iostream>
using namespace std;
int main(){
	int t,n;
        cin>>t;
	while (t--){
                cin>>n;
		int ans=0;
		int mul=1;
		for (int i=1;i<=n;i++){
			mul*=i;
			ans+=mul;
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
int main()
{
	int t,n;
    cin>>t;
	while (t--){
            cin>>n;
		int half=1;
		for (int i=0;i<n-1;i++)
			half=(half+1)*2;
		cout<<half<<endl;
	}
	return 0;
}
```
D
```objc
#include <iostream>
using namespace std;
int main(){
	int t,n;
    	cin>>t;
	while (t--){
        	cin>>n;
		for (int i=1;i<=2*n-1;i++){
			if (i<n){
				for (int j=1;j<=n-i;j++)	//打印空格
					cout<<" ";
				for (int k=1;k<=2*i-1;k++)	//打印*
					cout<<"*";
			}
			else if (i==n){
				for (int j=1;j<=2*n-1;j++)
					cout<<"*";
			}
			else{
				for (int j=1;j<=i-n;j++)	//打印空格
					cout<<" ";
				for (int k=1;k<(4*n-2*i);k++)	//打印*
					cout<<"*";
			}
			cout<<endl;
		}
	}
	return 0;
}
```
E
```objc
#include <iostream>
using namespace std;
int main(){
    int t,n,m;
    cin>>t;
    while (t--){
        cin>>n>>m;
        int ans=0;
        for (int i=0;i<n;i++){
            for (int j=0;j<m;j++){
                ans+=(n-i)*(m-j);
            }
        }
        cout<<ans<<endl;
    }
    return 0;
}
```