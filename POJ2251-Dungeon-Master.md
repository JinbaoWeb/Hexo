title: POJ2251 Dungeon Master
date: 2016-01-01 22:59:33
categories: [ACM,POJ]
tags: [POJ,BFS]
---
# Dungeon Master

Time Limit: 1000MS		Memory Limit: 65536K

## Description

	You are trapped in a 3D dungeon and need to find the quickest way out! 
	The dungeon is composed of unit cubes which may or may not be filled with rock.
	It takes one minute to move one unit north, south, east, west, up or down. 
	You cannot move diagonally and the maze is surrounded by solid rock on all sides. 
	Is an escape possible? If yes, how long will it take? 

<!--more-->

## Input

	The input consists of a number of dungeons. Each dungeon description starts with a 
	line containing three integers L, R and C (all limited to 30 in size). 
	L is the number of levels making up the dungeon. 
	R and C are the number of rows and columns making up the plan of each level. 
	Then there will follow L blocks of R lines each containing C characters. 
	Each character describes one cell of the dungeon. A cell full of rock is indicated 
	by a '#' and empty cells are represented by a '.'. Your starting position is indicated 
	by 'S' and the exit by the letter 'E'. There's a single blank line after each level. 
	Input is terminated by three zeroes for L, R and C.

## Output

	Each maze generates one line of output. If it is possible to reach the exit, print a 
	line of the form 
						Escaped in x minute(s).
	where x is replaced by the shortest time it takes to escape. 
	If it is not possible to escape, print the line 
						Trapped!
## Sample Input

	3 4 5
	S....
	.###.
	.##..
	###.#

	#####
	#####
	##.##
	##...

	#####
	#####
	#.###
	####E

	1 3 3
	S##
	#E#
	###

	0 0 0

## Sample Output

	Escaped in 11 minute(s).
	Trapped!

## 解题思路：

>BFS

## 参考代码
```objc
#include <iostream>
#include <queue>
using namespace std;
struct Node{
	int x,y,z;
	int cnt;
};
char map[35][35][35];
bool used[35][35][35];
int dir[6][3]={1,0,0,-1,0,0,0,1,0,0,-1,0,0,0,1,0,0,-1};
Node s,e,temp,temp2;
int l,r,c;
int bfs(){
	queue<Node> q;
	q.push(s);
	while (!q.empty()){
		temp=q.front();
		for (int i=0;i<6;i++){
			temp2.x=temp.x+dir[i][0];
			temp2.y=temp.y+dir[i][1];
			temp2.z=temp.z+dir[i][2];
			temp2.cnt=temp.cnt+1;
			if (temp2.x>=0 && temp2.x<l && 
			temp2.y>=0 && temp2.y<r && 
			temp2.z>=0 && temp2.z<c && 
			used[temp2.x][temp2.y][temp2.z]==true){
				q.push(temp2);
				used[temp2.x][temp2.y][temp2.z]=false;
				if (temp2.x==e.x && temp2.y==e.y && temp2.z==e.z){
					return temp2.cnt;
				}
			}
		}
		q.pop();
	}
	return -1;
}
int main(){
	while (cin>>l>>r>>c){
		if (l==0 && r==0 && c==0)
			break;
		for (int i=0;i<l;i++){
			for (int j=0;j<r;j++)
				for (int k=0;k<c;k++){
					cin>>map[i][j][k];
					if (map[i][j][k]=='#')
						used[i][j][k]=false;
					else
						used[i][j][k]=true;
					if (map[i][j][k]=='S')
						s.x=i,s.y=j,s.z=k,s.cnt=0;
					if (map[i][j][k]=='E')
						e.x=i,e.y=j,e.z=k;
				}
		}
		int ans=bfs();
		if (ans>0)
			cout<<"Escaped in "<<ans<<" minute(s)."<<endl;
		else
			cout<<"Trapped!"<<endl;
	}
	
	return 0;
}
```
