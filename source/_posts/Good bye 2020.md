---
title: Codeforces - Good bye 2020
date: 2020-12-31
tags:
    - 数据结构
    - 思维
categories: Codeforces
cover: https://dylolorz.cn/img/blog/Goodbye2020cover.jpg
---

# Codeforces - Good Bye 2020

# 前言
>  A — E 题解
2020的最后一场Codeforces，也算有点纪念意义吧...
赛时差1分钟调出e，一直被1<<i爆int迷惑了。
也许这和我有遗憾的2020首尾呼应了吧..

# A. Bovine Dilemma

# 题目来源<br/>
<font size="4">[https://codeforces.com/contest/1466/problem/A](https://codeforces.com/contest/1466/problem/A)</font>
<!-- more -->

# 题目原文
![在这里插入图片描述](https://dylolorz.cn/img/blog/cf-bye2020-A.png)

# 题目描述
<font size="4">给n个从1开始严格递增的数xi，代表坐标轴上的（xi，0）点，统计所有的由(xi,0)，(xj,0)，(0,1)三个点组成的面积不同的三角形个数。</font>

# 题解思路
<font size="4">下标从1开始严格递增，不会有重复的点，把x轴的两个点当作底，可知三角形的高恒为1，因此只需判断三角形不同的底的个数，即xi-xj有多少个不同的值。</font>

# 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <string>
using namespace std;
const int N=100010;
typedef long long LL;
typedef pair <int,int> PII;
int n,m,sz[N],st[1010];
int main(void)
{
    int t;
    cin>>t;
    while(t--)
    {
        cin>>n;
        memset(st,0,sizeof st);
        for(int i=1;i<=n;i++)cin>>sz[i];
        int ans=0;
        for(int i=1;i<=n;i++)
        {
            for(int j=i+1;j<=n;j++)
            {
                if(!st[sz[j]-sz[i]])
                {
                    ans++;
                    st[sz[j]-sz[i]]=1;
                }
            }
        }
        cout<<ans<<endl;
    }
    //system("pause");
    return 0;
}
```
# B. Last minute enhancements

# 题目来源
[https://codeforces.com/contest/1466/problem/B](https://codeforces.com/contest/1466/problem/B)

# 题目原文
![](https://dylolorz.cn/img/blog/cf-bye2020-B.png)

# 题目描述
<font size="4">对于n个数的数组，对于每个数可以加1或者不变，求数组中不同的数的个数的最大值。</font>

# 题解思路
<font size="4">对于最后一个数，加1一定比不变更好。从这条路切入，从后往前考虑即可。</font>

# 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <string>
#include <unordered_map>
using namespace std;
const int N=200010;
typedef long long LL;
typedef pair <int,int> PII;
int n,m,sz[N],st[1010];
int main(void)
{
    int t;
    cin>>t;
    while(t--)
    {
        cin>>n;
        for(int i=1;i<=n;i++)cin>>sz[i];
        sort(sz+1,sz+n+1);
        int ans=1;
        sz[n]++;
        for(int i=n-1;i>=1;i--)
        {
            if(sz[i]+1==sz[i+1])
            {
                ans++;
                continue;
            }
            else if(sz[i]==sz[i+1])continue;
            else
            {
                sz[i]++,ans++;
            }
            
        }
        cout<<ans<<endl;
    }
    //system("pause");
    return 0;
}
```
# C. Canine poetry

# 题目来源
[https://codeforces.com/contest/1466/problem/C](https://codeforces.com/contest/1466/problem/C)

# 题目原文
![](https://dylolorz.cn/img/blog/cf-bye2020-C.png)

# 题目描述
<font size="4">对于一个只包含小写字母的字符串，每个操作可以将某个位置的字母改成任意字母，求使字符串的最大回文子串长度为1的最小操作数。</font>

# 题解思路
<font size="4">首先模拟一下，最终字符串一定要保证不可以存在类似aa这样长度为2的回文子串，同样，最终字符串也一定要保证不可以存在类似aba这样长度为3的回文子串，接着模拟，最终字符串要保证不可以存在类似abba这样的长度为4的回文子串，到这发现，abba在消除bb类的时候回文性质就被破坏了，因此只需要考虑长度为2和3的回文子串。对于长度为3的aba，可能出现aaa的情况，因此我们可以先模拟长度为3，如果出现aba则改变这两个a中的第2个a，因为后面的a可能对再后面会产生贡献，破坏掉他是最优的。如果出现aaa，3个a必须破坏2个a才可以破坏所有回文，而贪心的破坏后面两个是更优的。下面代码以‘A’表示已改变的字符，并且它不可能与其他任何产生回文。</font>

# 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <string>
#include <unordered_map>
#include <vector>
using namespace std;
const int N=100010;
typedef long long LL;
typedef pair <int,int> PII;
int n,m,sz[N],st[N];
int main(void)
{
    int t;
    cin>>t;
    while(t--)
    {
        string str;
        cin>>str;
        vector<int>v1,v2;
        int ans=0,len=str.size();
        for(int i=0;i<len-1;i++)
        {
            if(str[i]=='A')continue;
            if((i<len-2)&&(str[i]==str[i+2]))
            {
                str[i+2]='A';
                ans++;
            }
            if(str[i]==str[i+1])
            {
                str[i+1]='A';
                ans++;
            }
        }
        cout<<ans<<endl;
    }
    //system("pause");
    return 0;
}
```

# D. 13th Labour of Heracles

# 题目来源
[https://codeforces.com/contest/1466/problem/D](https://codeforces.com/contest/1466/problem/D)

# 题目原文
![](https://dylolorz.cn/img/blog/cf-bye2020-D.png)

# 题目描述
<font size="4">给定一颗n个顶点的树，每个顶点有权重，对于k染色含义是将这棵树的边用不超过k种颜色进行染色，对于染的每种颜色都有一个贡献要求，将树中染此颜色的边取出来，会变成一个或多个子图，而这种颜色的贡献即为多个子图中最大的贡献，对于一个子图的贡献为图的每个顶点的权重和。对每个k求k染色的贡献最大值。</font>

# 题解思路
<font size="4">一开始以为是图论题，看到k个值又以为1次dfs求子树贡献，后来发现是个隐藏的思维题。有两个性质需要挖掘，首先k染色下，可以看作所有结点的权重和加上某些延伸出去的边不是同种颜色的顶点的权重。因此刚好k种一定贡献最大，因为多染一种颜色，就可以多增加一些结点权重。第二个性质，同种颜色都在同一个子图下贡献最大，因为分开就取max的子图值，而另一些部分就被抛弃，如果可以把这些部分染色成和他们相连接的图的颜色，这部分的贡献值就可以被加上。一开始k=1时，即所有边染同色，贡献为权重和，k=2时，因为k=1已经染了一种颜色，所以对每个顶点必须留下一条边为原来的颜色，否则颜色就被覆盖了。因此接下去只能对于所有度数>=2的顶点操作，而每次增加的贡献即为顶点权重，所以只需要每次取出度数大于2并且权重最大的添加就行了。</font>

# 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <string>
#include <unordered_map>
#include <vector>
#include <queue>
using namespace std;
const int N=100010;
typedef long long LL;
typedef pair <LL,LL> PII;
LL n,m;
LL w[N],d[N];
PII sz[N];
int main(void)
{
    int t;
    cin>>t;
    while(t--)
    {
        cin>>n;
        LL ans=0;
        for(int i=1;i<=n;i++)cin>>w[i],ans+=w[i];
        for(int i=1;i<=n;i++)sz[i]={w[i],0};
        for(int i=1;i<n;i++)
        {
            LL a,b;
            cin>>a>>b;
            sz[a].second++;
            sz[b].second++;
        }
        priority_queue<PII>qe;
        for(int i=1;i<=n;i++)
        {
            if(sz[i].second>=2)qe.push(sz[i]);
        }
        cout<<ans<<" ";
        for(int i=1;i<n-1;i++)
        {
            PII u=qe.top();
            qe.pop();
            ans+=u.first;
            cout<<ans<<" ";
            if(u.second!=2)qe.push({u.first,u.second-1});
        }
        cout<<endl;
    }
    //system("pause");
    return 0;
}
```

# E. Apollo versus Pan

# 题目来源
[https://codeforces.com/contest/1466/problem/E](https://codeforces.com/contest/1466/problem/E)

# 题目原文
![](https://dylolorz.cn/img/blog/cf-bye2020-E.png)

# 题目描述
<font size="4">给n个数 求上图中的(xi&xj)*(xj|xk)的和</font>

# 题解思路
![](https://dylolorz.cn/img/blog/E-1.png)
![](https://dylolorz.cn/img/blog/E-2.png)
<font size="4">将x1...xn每位的贡献预处理，即可o(n)解决此问题</font>

# 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
#include <string>
#include <unordered_map>
#include <vector>
#include <cmath>
#include <queue>
using namespace std;
const int N=500010;
const long long mod=1e9+7;
typedef long long LL;
typedef pair <LL,LL> PII;
LL st1[100],st2[100],st3[100],sz[N],n;
int main(void)
{
    cin.tie(0);
    ios::sync_with_stdio(false);
    int t;
    cin>>t;
    while(t--)
    {
        cin>>n;
        for(int i=0;i<80;i++)st1[i]=0,st2[i]=0,st3[i]=0;
        for(int i=1;i<=n;i++)cin>>sz[i];
        LL now=1;
        for(int i=0;i<60;i++)
        {
            for(int j=1;j<=n;j++)
            {
                st1[i]=(st1[i]+((sz[j]>>i)&1)*now%mod)%mod;//and
                st2[i]=(st2[i]+now%mod)%mod;//or
                //st3[i]=(st3[i]+((sz[j]>>i)&1))
            }
            now=now*2%mod;
        }
        LL ans=0;
        for(int i=1;i<=n;i++)
        {
            LL p=0,q=0;
            for(int j=0;j<60;j++)
            {
                int u1=(sz[i]>>j)&1;
                if(u1==1)
                {
                    p=(p+st2[j])%mod;
                    q=(q+st1[j])%mod;
                }
                else p=(p+st1[j])%mod;
            }
            ans=(ans+(p*q)%mod)%mod;
            //cout<<ans<<endl;
        }
        cout<<ans%mod<<endl;
    }
    //system("pause");
    return 0;
}
```