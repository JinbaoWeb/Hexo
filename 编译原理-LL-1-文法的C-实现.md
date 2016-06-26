title: 编译原理 LL(1)文法的C++实现
categories: [编译原理]
tags: [编译原理,LL(1)文法]
date: 2016-05-27 18:47:48
---
# 一、题目

LL(1)文法的C++实现要求
针对二型文法实现LL(1)，对一个给定的输入串，给出分析结果。
```
S->aASb
S->aAc
A->Ad
A->e
```
输入串为`aeaecb`

<!--more-->

# 二、实现过程

## 2.1 需要用到的数据结构
- 非终结符和终结符都是单个的字符，因此我们以`char`作为非终结符和终结符的属性。非终结符用`vector`存储，而`terminals`用`set`存储是为了方便后来对求`First`集和`Follow`集的使用。
- `First`集和`Follow`集是一个字符对应多个字符，所以在使用`map`的同时，对后面的多个字符用`set`存储作为映射。
- 文法`rules`是一个字符对于多个字符串，所有在使用`map`的同时，对后面的多个字符用`vect`存储作为映射。
- 非终结符的`Epsilon`表是对每个非终结符判断能不能推出$\epsilon$，所以做`char`跟`bool`的映射。
- 预测分析表中存储的是文法，所以用`string`作为属性值。
- 非终结符对应表和终结符对应表是为了对非终结符和终结符做一个值对应，方便作为预测分析表的下标。
```
vector<char> nonTerminals; //非终结符集合
set<char> terminals;		//终结符集合
map< char,set<char> > firstSet;	//First集
map< char,set<char> > followSet;	//Follow集
map< char,vector<string> > rules;	//文法
map< char,bool> Epsilon;	//非终结符的Epsilon
string parsingTable[100][100];	//预测分析表
map<char,int> nonTer;	//非终结符对应表
map<char,int> Ter;	//终结符对应表
```

## 2.2 从文件中获取文法

我们把文法存放在`input_rule.txt`文件中，逐行逐行地读取文法，将文法加入`rules`集合中，同时也将非终结符加入到`nonTerminals`中。
```
void getGrammar()	//获取文法
{
	ifstream infile;
    string rule;
	vector<char>::iterator it;
	infile.open("input_rule.txt",ifstream::in);
	while (getline(infile,rule))
	{
		string s = "";
		for (int i = 3;i < rule.size(); i++)
			s += rule[i];
		rules[rule[0]].push_back(s);
		it = find(nonTerminals.begin(),nonTerminals.end(),rule[0]);
		if (it == nonTerminals.end()) nonTerminals.push_back(rule[0]);
	}
	infile.close();
}
```
### 2.2.1 消除直接左递归
```
void RemoveDirectLeftRecursion()	//消除直接左递归
{
	vector<string>::iterator it;
	vector<string> x,y;
	string temp,str;
	for (int i=0;i<nonTerminals.size();i++)
	{
		int flag=0;
		x.clear();
		y.clear();
		char ch=FindNewnonTerminals();	//获取新的非终结符
		for (int j=0;j<rules[nonTerminals[i]].size();j++)
		{
			int pos=rules[nonTerminals[i]][j].find(nonTerminals[i]);
			if (pos==0)
			{
				flag=1;
				temp=rules[nonTerminals[i]][j];	//需要删除的rule
				str = temp.substr(pos + 1);
				x.push_back(str);
				y.push_back(temp);
			}
		}
		if (flag)
		{
			for (int j=0;j<y.size();j++)	////删除需要消除直接左递归的rule
			{
				it = find(rules[nonTerminals[i]].begin(), rules[nonTerminals[i]].end(), y[j]);
				rules[nonTerminals[i]].erase(it);
			}
			for(int j = 0; j < rules[nonTerminals[i]].size(); j++)	//加入新的rule
			{
				rules[nonTerminals[i]][j] = rules[nonTerminals[i]][j] + ch;
			}
			for(int j = 0; j < x.size(); j++)	//加入新的rule
			{
				rules[ch].push_back(x[j] + ch);
			}
			rules[ch].push_back("$");
			nonTerminals.push_back(ch);
		}
	}
}
```
### 2.2.2 提取左公共因子
```
void leftFactoring()
{
	vector<string>::iterator it;
	bool flag=true;
	while (flag)
	{
		flag=false;
		for (int i=0;i<nonTerminals.size();i++)
		{
			for (int j=0;j<rules[nonTerminals[i]].size();i++)
			{
				for (int k=j+1;k<rules[nonTerminals[i]].size();k++)
				{
					string s1=rules[nonTerminals[i]][j],s2=rules[nonTerminals[i]][k];
					int p;
					for (p=0;p<s1.size()&&p<s2.size();p++)
						if (s1[p]!=s2[p]) break;
					if (p!=0)
					{
						flag=true;
						string s3="",s4="",s5="";
						for (int q=0;q<p;q++)
							s3+=s1[q];
						for (int q=p;q<s1.size();q++)
							s4+=s1[q];
						for (int q=p;q<s2.size();q++)
							s5+=s2[q];
						char ch=FindNewnonTerminals();
						s3+=ch;
						//cout<<s1<<" "<<s2<<" "<<s3<<" "<<s4<<" "<<s5<<endl;
						it = find(rules[nonTerminals[i]].begin(), rules[nonTerminals[i]].end(), s1);
						rules[nonTerminals[i]].erase(it);
						it = find(rules[nonTerminals[i]].begin(), rules[nonTerminals[i]].end(), s2);
						rules[nonTerminals[i]].erase(it);
						rules[nonTerminals[i]].push_back(s3);
						rules[ch].push_back(s4);
						rules[ch].push_back(s5);
						nonTerminals.push_back(ch);
					}

				}
			}
		}
	}
}
```



## 2.3 求出能推出$\epsilon$的非终结符
对于某个非终结符
（1）如果产生式为$\epsilon$，那么这个非终结符可以推出$\epsilon$
（2）对它的产生式从左到右扫描，如果遇到终结符，那么不可以推出$\epsilon$，如果遇到非终结符，那我们再递归这个非终结符，判断这个非终结符能否推出$\epsilon$，如果不能，那么该终结符不能推出$\epsilon$，如果能，继续找下一个终结符，直到找完所有非终结符，如果找完了最后一个终结符，而最后一个终结符也可以推出$\epsilon$，那么该非终结符可以推出$\epsilon$
```
bool produceEpsilon(char ch)
{
	vector<char>::iterator it;
	for (int i=0;i<rules[ch].size();i++)
	{
		if (rules[ch][i]=="$")
			return true;
		int flag=0;
		for (int j=0;j<rules[ch][i].size();j++)
		{
			flag=0;
			it = find(nonTerminals.begin(), nonTerminals.end(), rules[ch][i][j]);
			if (it!=nonTerminals.end())
			{
				if (produceEpsilon(rules[ch][i][j])==false) return false;
				else flag=1;
			}
			else break;
		}
		if (flag) return true;
	}
	return false;
}
void checkEpsilon()
{
	for (int i=0;i<nonTerminals.size();i++)
	{
		Epsilon[ nonTerminals[i] ]=produceEpsilon( nonTerminals[i] );
	}
}
```

## 2.4 计算First集
（1）首先，对于所有能推出$\espilon$的非终结符的First集加入$\espilon$。
（2）对每个非终结符对应的产生式，从左到右扫描，如果遇到终结符将终结符加入First集，然后对下一个产生式进行处理，如果遇到非终结符，将这个非终结符的First集加入该非终结符的First集，如果这个非终结符不能推出$\espilon$，则对下一个产生式进行处理，如果能，则继续向右扫描。
（3）如果对上述的操作（2）还能扩大一个非终结符的First集，那么继续执行操作（2），直到不能扩大First集为止。
```
void FindFirstSet()
{
	vector<char>::iterator it;
	set<char>::iterator scit;
	for (int i=0;i<nonTerminals.size();i++)
		if (Epsilon[ nonTerminals[i] ]==1) firstSet[nonTerminals[i]].insert('$');
	bool flag=true;
	while (flag)
	{
		flag=false;
		for (int i=0;i<nonTerminals.size();i++)
		{
			for (int j=0;j<rules[nonTerminals[i]].size();j++)
			{
				//cout << nonTerminals[i] << "->" << rules[nonTerminals[i]][j] << endl ; 
				for (int k=0;k<rules[nonTerminals[i]][j].size();k++)
				{
					it = find(nonTerminals.begin(), nonTerminals.end(), rules[nonTerminals[i]][j][k]);
					if (it!=nonTerminals.end())	//是非终结符
					{
						//将rules[nonTerminals[i]][j][k]的所有firstSet加入nonTerminals[i]]的firstSet
						if (firstSet.find(rules[nonTerminals[i]][j][k])!=firstSet.end())
						{
							for (scit=firstSet[rules[nonTerminals[i]][j][k]].begin();scit!=firstSet[rules[nonTerminals[i]][j][k]].end();scit++)
							{
								if (firstSet[nonTerminals[i]].find(*scit)==firstSet[nonTerminals[i]].end())
									flag=true;
								firstSet[nonTerminals[i]].insert(*scit);
							}
							if (Epsilon[rules[nonTerminals[i]][j][k]]==false)	//如果当前这个不是可以产生epsilon，则退出。
								break;
						}
					}
					else
					{
						if (firstSet[nonTerminals[i]].find(rules[nonTerminals[i]][j][k])==firstSet[nonTerminals[i]].end())
							flag=true;
						firstSet[nonTerminals[i]].insert(rules[nonTerminals[i]][j][k]);
						break;
					}
				}
			}
		}
	}
	for (int i=0;i<nonTerminals.size();i++)
	{
		if (Epsilon[ nonTerminals[i] ]==0)
		{
			if (firstSet[nonTerminals[i]].find('$')!=firstSet[nonTerminals[i]].end())
			{
				firstSet[nonTerminals[i]].erase('$');
			}
		}
	}
}
```
## 2.5 计算Follow集
（1）首先，计算所有非终结符后面跟着非终结符的Follow集（将后一个非终结符的Fist集加入前一个非终结符的Follow集）
（2）针对A$\rightarrow$...BC..，如果C..$\rightarrow\epsilon$，那么将A的Follow集也加入B的Follow集中。
（3）对所有非终结符，如果（2）可以使得任何一个非终结符的Follow集扩大，那么继续执行（2），直到不能扩大为止。
```objc
void FindFollowSet()
{
	set<char>::iterator it;
	vector<char>::iterator vcit;
	followSet[nonTerminals[0]].insert('#');
	//对每个非终结符将跟在其后面的非终结符的firstSet加入其followSet,跟着其后面的终结符直接加入followSet
	for(int i = 0; i < nonTerminals.size(); i++)
	{
		for(int j = 0; j < rules[nonTerminals[i]].size(); j++)
		{
			for (int k=0;k<rules[nonTerminals[i]][j].size()-1;k++)
			{
				vcit=find(nonTerminals.begin(),nonTerminals.end(),rules[nonTerminals[i]][j][k]);
				if (vcit==nonTerminals.end())
					continue;
				vcit=find(nonTerminals.begin(),nonTerminals.end(),rules[nonTerminals[i]][j][k+1]);
				if (vcit!=nonTerminals.end())
				{
					for (it=firstSet[rules[nonTerminals[i]][j][k+1]].begin();it!=firstSet[rules[nonTerminals[i]][j][k+1]].end();it++)
						if (*it!='$') followSet[rules[nonTerminals[i]][j][k]].insert(*it);
				}
				else	followSet[rules[nonTerminals[i]][j][k]].insert(rules[nonTerminals[i]][j][k+1]);
			}
		}
	}
	//printFollowSet();
	bool flag=true;
	while (flag)
	{
		//printFollowSet();
		flag=false;
		for(int i = 0; i < nonTerminals.size(); i++)
		{
			//cout<<nonTerminals[i]<<endl;
			for(int j = 0; j < rules[nonTerminals[i]].size(); j++)
			{
				//cout<<"\t"<<rules[nonTerminals[i]][j]<<endl;
				for (int k=0;k<rules[nonTerminals[i]][j].size()-1;k++)
				{
					vcit=find(nonTerminals.begin(),nonTerminals.end(),rules[nonTerminals[i]][j][k]);
					if (vcit==nonTerminals.end())
						continue;
					//cout<<rules[nonTerminals[i]][j][k]<<endl;
					int p=0;
					for (p=k+1;p<rules[nonTerminals[i]][j].size();p++)
					{
						vcit=find(nonTerminals.begin(),nonTerminals.end(),rules[nonTerminals[i]][j][p]);
						if (vcit==nonTerminals.end())
						{
							if (followSet[rules[nonTerminals[i]][j][k]].find(rules[nonTerminals[i]][j][p])==followSet[rules[nonTerminals[i]][j][k]].end())
								flag=true;
							followSet[rules[nonTerminals[i]][j][k]].insert(rules[nonTerminals[i]][j][p]);
							break;
						}
						for (it=firstSet[rules[nonTerminals[i]][j][p]].begin();it!=firstSet[rules[nonTerminals[i]][j][p]].end();it++)
						{
							if (*it=='$') continue;
							if (followSet[rules[nonTerminals[i]][j][k]].find(*it)==followSet[rules[nonTerminals[i]][j][k]].end())
								flag=true;
							followSet[rules[nonTerminals[i]][j][k]].insert(*it);
						}
						if (firstSet[rules[nonTerminals[i]][j][p]].find('$')==firstSet[rules[nonTerminals[i]][j][p]].end())
							break;
					}
					if (p==rules[nonTerminals[i]][j].size())
					{
						for (it=followSet[nonTerminals[i]].begin();it!=followSet[nonTerminals[i]].end();it++)
						{
							if (followSet[rules[nonTerminals[i]][j][k]].find(*it)==followSet[rules[nonTerminals[i]][j][k]].end())
								flag=true;
							followSet[rules[nonTerminals[i]][j][k]].insert(*it);
						}
					}
				}
				vcit=find(nonTerminals.begin(),nonTerminals.end(),rules[nonTerminals[i]][j][rules[nonTerminals[i]][j].size()-1]);
				if (vcit!=nonTerminals.end())
				{
					for (it=followSet[nonTerminals[i]].begin();it!=followSet[nonTerminals[i]].end();it++)
					{
						if (followSet[rules[nonTerminals[i]][j][rules[nonTerminals[i]][j].size()-1]].find(*it)==followSet[rules[nonTerminals[i]][j][rules[nonTerminals[i]][j].size()-1]].end())
							flag=true;
						followSet[rules[nonTerminals[i]][j][rules[nonTerminals[i]][j].size()-1]].insert(*it);
					}
				}
				
			}
		}
	}
	//printFollowSet();
}
```

## 2.6 计算Select集和预测分析表

对于$A\rightarrow B$，如果B可以推出$\epsilon$，那么$A\rightarrow B$的Select集为B的First集跟A的Follow集；如果B不能推出$\epsilon$，那$A\rightarrow B$的Select集为B的First集。
```objc
void GetParsingTable()
{
	vector<char> terminal;
	vector<char>::iterator it;
	set<char>::iterator scit;
	for (int i=0;i<nonTerminals.size();i++)
		nonTer[nonTerminals[i]]=i;
	int p;
	for (p=0,scit=terminals.begin();scit!=terminals.end();p++,scit++)
		Ter[*scit]=p;
	for (scit=terminals.begin();scit!=terminals.end();scit++)
		terminal.push_back(*scit);
	for (int i=0;i<nonTerminals.size();i++)
		for (int j=0;j<terminal.size();j++)
			parsingTable[i][j]="";
	for (int i=0;i<nonTerminals.size();i++)
	{
		for (int j=0;j<rules[nonTerminals[i]].size();j++)
		{
			cout<<nonTerminals[i]<<"->"<<rules[nonTerminals[i]][j]<<"\t";
			set<char> temp;
			temp.clear();
			int k;
			for (k=0;k<rules[nonTerminals[i]][j].size();k++)
			{
				it=find(nonTerminals.begin(),nonTerminals.end(),rules[nonTerminals[i]][j][k]);
				if (it==nonTerminals.end())
				{
					if (rules[nonTerminals[i]][j][k]!='$')
						temp.insert(rules[nonTerminals[i]][j][k]);
					else
						k++;
					break;
				}
				else
				{
					int flag=0;
					for (scit=firstSet[rules[nonTerminals[i]][j][k]].begin();scit!=firstSet[rules[nonTerminals[i]][j][k]].end();scit++)
					{
						if (*scit=='$')
						{
							flag=1;
							temp.insert('#');
						}
						else
							temp.insert(*scit);
					}
					if (flag==0) break;
				}
			}
			if (k==rules[nonTerminals[i]][j].size())
			{
				for (scit=followSet[nonTerminals[i]].begin();scit!=followSet[nonTerminals[i]].end();scit++)
				{
					temp.insert(*scit);
				}
			}
			for (scit=temp.begin();scit!=temp.end();scit++)
			{
				if (scit==temp.begin())
					cout<<*scit;
				else cout<<","<<*scit;
			}
			cout<<endl;
			for (scit=temp.begin();scit!=temp.end();scit++)
				parsingTable[nonTer[nonTerminals[i]]][Ter[*scit]]=rules[nonTerminals[i]][j];
		}
	}
}
```

## 2.7 输入串的分析
对输入的串进行分析。
```
void analysis()
{
	ifstream cin("input_s.txt");
	string str;
	vector<char>::iterator it;
	cout<<"Input string for analysis:  ";
	//getline(infile,str);
	cin>>str;
	cout<<str<<endl;
	str+="#";
	int step=1;
	stack<char> s;
	stack<char> ss;
	s.push('#');
	s.push(nonTerminals[0]);
	int i=0;
	cout<<"-----Forecast analysis process------------------>>"<<endl;
	cout<<"step"<<"\t"<<"stack"<<"\t"<<"input"<<"\t"<<"left"<<endl;
	while (i<str.size())
	{
		char temp=s.top();
		cout<<step<<"\t";
		while (s.empty()==false)
		{
			char temp=s.top();
			ss.push(temp);
			s.pop();
		}
		while (ss.empty()==false)
		{
			char temp=ss.top();
			cout<<temp;
			s.push(temp);
			ss.pop();
		}
		cout<<"\t"<<str[i]<<"\t";
		for (int p=0;p<str.size();p++)
		{
			if (p<i) cout<<" ";
			else cout<<str[p];
		}
		cout<<endl;
		step++;
		if (str[i]==temp)
		{
			s.pop();
			i++;
			continue;
		}
		it=find(nonTerminals.begin(),nonTerminals.end(),temp);
		if (it!=nonTerminals.end())
		{
			if (parsingTable[nonTer[temp]][Ter[str[i]]]=="")
			{
				cout<<"Error!"<<endl;
				break;
			}
			else
			{
				s.pop();
				string st=parsingTable[nonTer[temp]][Ter[str[i]]];
				if (st=="$") continue;
				int len=st.size()-1;
				while (len>=0)
				{
					s.push(st[len--]);
				}
			}
		}
	}
	cout<<"Analysis result:  ";
	if (s.empty()==true)
		cout<<"Yes"<<endl;
	else
		cout<<"No"<<endl;

}
```

# 三、结果显示

整个程序的结果如下：
```
-----Initial Grammar---------------------------->>
S->aASb
S->aAc
A->Ad
A->e
-----After Remove Direct Left Recursion Grammar->>
S->aASb
S->aAc
A->eB
B->dB
B->$
-----After Extract Left Factor Grammar->>
S->aAC
A->eB
B->dB
B->$
C->Sb
C->c
-----Check nonTerminals include Epsilon--------->>
S	A	B	C
No	No	Yes	No
-----FirstSet And FollowSet--------------------->>
nonTerminals	firstSet	followSet
S		a		#,b
A		e		a,c
B		$,d		a,c
C		a,c		#,b
-----SelectSet---------------------------------->>
S->aAC	a
A->eB	e
B->dB	d
B->$	a,c
C->Sb	a
C->c	c
-----Parsing Table------------------------------>>
	#	a	b	c	d	e
S		aAC				
A						eB
B		$		$	dB	
C		Sb		c		
Input string for analysis:  aeaecb
-----Forecast analysis process------------------>>
step	stack	input	left
1	#S	a	aeaecb#
2	#CAa	a	aeaecb#
3	#CA	e	 eaecb#
4	#CBe	e	 eaecb#
5	#CB	a	  aecb#
6	#C	a	  aecb#
7	#bS	a	  aecb#
8	#bCAa	a	  aecb#
9	#bCA	e	   ecb#
10	#bCBe	e	   ecb#
11	#bCB	c	    cb#
12	#bC	c	    cb#
13	#bc	c	    cb#
14	#b	b	     b#
15	#	#	      #
Analysis result:  Yes
```

[源码下载](http://pan.baidu.com/s/1eSyiBGu)