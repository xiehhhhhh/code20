# code20  
//贪心销售比赛
#include<queue>
#include<vector>
#include<cstdio>
#include<cstdlib>
#include<cstring>
#include<iostream>
#include<algorithm>
using namespace std;
long long int price[100010],t,n,res;
       
int main()
{
    ios::sync_with_stdio(false);
    cin>>t;
    while(t--)
    {
        cin>>n;
        priority_queue<long long int, vector<long long int>, greater<long long int> > q;
        res=0;
        for(int i=1;i<=n;i++)
        {
            cin>>price[i];
        }
        res-=price[1];
        res+=price[n];
        for(int i=2;i<=n-1;i=i+2)
        {
            long long int buy=min(price[i],price[i+1]);
            long long int sell=max(price[i],price[i+1]);
            if(!q.empty())
            {
                if(buy>q.top())
                {
                    res=res-2*q.top()+buy+sell;
                    q.pop();
                    q.push(buy);
                    q.push(sell);
                }
                else
                {
                    res=res-buy+sell;
                    q.push(sell);
                }
            }
            else
            {
                res=res-buy+sell;
                q.push(sell);
            }
        }     
        cout<<res<<endl;
    }
}
