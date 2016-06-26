title: ZOJ3486 Judge Internal Error
categories: [ACM,ZOJ]
tags: [ZOJ,模拟]
date: 2016-03-26 19:24:16
---
Judge Internal Error

	he online judge system developed by Zhejiang University ACM/ICPC team 
	(that is the system used during this contest) is designed to be robust. 
	It can execute all kinds of user-submitted programs, including unsafe or 
	malicious ones, and remain working and stable. However, it does report 
	mysterious "Judge Internal Error" ("JIE" in short), occasionally.

	JIE happens due to various reasons, such as crashes of special judge 
	programs, poor network conditions, incredible large test data, extremely 
	high system load, failures of hard disks, bugs of online judge system, 
	cosmic radiation and so on. In our experience, real world JIE often 
	reflects one or more problematic problems. Every time JIE happens, the 
	corresponding problem ID is written to a special system log. Given the 
	system log, your task is to find out the ID of the most problematic problem.

<!--more-->

Input

	The first line contains an integer T (T ≈ 10), the number of test cases. 
	The following are test cases, separated by one blank line.

	For each test case, the first line contains an integer N (1 ≤ N ≤ 1000), 
	the size of system log. Following N lines, each line contains an integer 
	Pi (1001 ≤ Pi ≤ 9999), which is the problem ID causing JIE.

Output

	For each test case, output one integer in one line, which is the ID of the 
	most problematic problem (that is, this ID occurs the most frequently in 
	the log). When multiple IDs occur with a same frequency, prefer the largest ID.

Sample Input

	2
	4
	1001
	1003
	1003
	1002

	2
	1001
	1003

Sample Output

	1003
	1003

参考代码

```objc
#include <bits/stdc++.h>
using namespace std;
const int MAX_N = 1000 + 100;
int arr[MAX_N];
int main()
{
	int T;
    cin>>T;
    while(T--)
    {
        int n;
        cin>>n;
        for(int i = 0; i < n; i++)
            cin>>arr[i];
        sort(arr, arr + n);
        int _max = 1, temp = 1, k = 0;
        for(int i = 1; i < n; i++)
        {
            if(arr[i] == arr[i - 1])
            {
                temp++;
                if(i == n - 1)
                {
                    if(_max <= temp)
                    {
                        _max = temp;
                        k = i;
                    }
                }
            }
            else
            {
                if(_max <= temp)
                {
                    _max = temp;
                    k = i - 1;
                    if(i == n - 1)
                        k = i;
                }
                temp = 1;
            }
        }
        cout<<arr[k]<<endl;
    }
	return 0;
}
```

	