# BUS-RESERVATION-SYSTEM-USING-CPP-STL
This project is made using C++ language.
#include<bits/stdc++.h>
#include<stack>
#include<unordered_set>
using namespace std;
bool helper(vector<int> *edge,int n)
{
	unordered_set<int> set[2];//create the 2(two) box ,which contain the different color
	queue<int> pendingnode;
	pendingnode.push(0);
	set[0].insert(0);
	while(pendingnode.size()!=0)
	{
		int curr_ele=pendingnode.front();
		
		pendingnode.pop();
		int ele=(set[0].count(curr_ele)>0?0:1);
		for(int i=0;i<edge[curr_ele].size();i++)
		{
			int neighbour=edge[curr_ele][i];//here ,use of adjancy list
		
			if(set[0].count(neighbour)==0&&set[1].count(neighbour)==0)
			{
				//ele not present in both of the container(set)
				set[1-ele].insert(neighbour);
				pendingnode.push(neighbour);
			}
			else if(set[ele].count(neighbour)>0)
			{
				//ele present in same container(set)
				return false;
			}
		}
	}
	return true;
}
int main()
{
	int n;//number of node in graph
	cin>>n;
	vector<int> *edge=new vector<int>[n];
	int m;//number of connection between the node
	cin>>m;
	for(int i=0;i<m;i++)
	{
		int x,y;
//		cout<<"enter the co-ordinate of x and y"<<endl;
		cin>>x>>y;
		edge[x-1].push_back(y-1);
		edge[y-1].push_back(x-1);
	}
	
	bool ans=helper(edge,n);
	if(ans==1)
	{
		cout<<"BIPARTITE"<<endl;
	}
	else
	{
		cout<<"NOT BIPARTITE"<<endl;
	}
}
