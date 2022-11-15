---
title: 第八届“图灵杯”NEUQ-ACM程序设计竞赛个人赛（同步赛）
date: 2021-2-1
tags: 
    - 算法
    - 图灵杯
    - C++
categories: 图灵杯
cover: https://dylolorz.cn/img/blog/第八届“图灵杯”cover.jpg
---

# 第八届“图灵杯”NEUQ-ACM程序设计竞赛个人赛（同步赛）

> <font size='3'>没注意开始时间，结果开赛的时候还在和小伙伴快乐剧本杀?? </font>
> <font size='3'>不过补题体验还可以,难得的一场稍简单的比赛,好像除了博弈论基本都是模拟题了(bushi </font>

# A.切蛋糕
![](https://dylolorz.cn/img/blog/第八届“图灵杯”A.png)

## 简要题解
<font size='4'>由题可得，要求每个人分得的蛋糕与1/k的绝对值差值不能大于1/2^10,因为每次切蛋糕都是对半分，首先考虑最好算的特殊状态，如果存在一种分法是分给每一个人的蛋糕大小相等，且和1/k的差值满足题意，那这样就不再需要考虑最优拆分策略了，由于总操作限制是不大于6000，事实证明在这个操作限制下确实存在这样一种策略一定满足。</font>
<font size='4'>证明如下：</font>
![](https://dylolorz.cn/img/blog/第八届“图灵杯”A证明1.png)
![](https://dylolorz.cn/img/blog/第八届“图灵杯”A证明2.png)

## 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
using namespace std;
int main(void)
{
    int k;
    cin >> k;
    cout <<k+(1<<10)-1<< endl;
    for(int i=0;i<10;i++)
    {
        for(int j=0;j<(1<<i);j++)
        {
            cout<<1<<" "<<i<<endl;
        }
    }
    int num=1024/k;
    for(int i=1;i<=k;i++)
    {
        cout<<2<<" "<<num<<" ";
        for(int j=1;j<=num;j++)
        {
            cout<<"10 ";
        }
        cout<<"\n";
    }
     
    return 0;
}
```

# B.小宝的幸运数组
![](https://dylolorz.cn/img/blog/第八届“图灵杯”B.png)

## 简要题解
![](https://dylolorz.cn/img/blog/第八届“图灵杯”B证明.png)

## 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <cstring>
#include <string>
using namespace std;
typedef long long LL;
typedef pair<int,int>PII;
const int N=100010;
LL dp[N],sz[N];
unordered_map<LL,LL>mp;
int main(void)
{
    LL t;
    cin>>t;
    while(t--)
    {
        int n,k;
        cin>>n>>k;
        mp.clear();
        for(int i=1;i<=n;i++)cin>>sz[i],sz[i]%=k;
        mp[0]=0;
        LL num=0,ans=-1;
        for(int i=1;i<=n;i++)
        {
            num=(num+sz[i])%k;
            if(mp[num]||num==0)
            {
                ans=max(ans,i-mp[num]);
            }
            else mp[num]=i;
        }
        cout<<ans<<endl;
    }
    //system("pause");
    return 0;
}
```

# C.上进的凡凡
![](https://dylolorz.cn/img/blog/第八届“图灵杯”C.png)

## 简要题解
![](https://dylolorz.cn/img/blog/第八届“图灵杯”C证明.png)

## 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <cstring>
#include <string>
using namespace std;
typedef long long LL;
typedef pair<int,int>PII;
const int N=100010;
LL dp[N],sz[N];
int main(void)
{
    LL t;
    t=1;
    while(t--)
    {
        int n;
       cin>>n;
       for(int i=1;i<=n;i++)
       {
           cin>>sz[i];
       }
       LL ans=1;
       for(int i=1;i<=n;i++)
       {
           dp[i]=1;
           if(i==1)continue;
           if(sz[i]>=sz[i-1])dp[i]+=dp[i-1];
           ans+=dp[i];
       }
       cout<<ans<<endl;
    
    }
    //system("pause");
    return 0;
}
```

# D.Seek the Joker I
![](https://dylolorz.cn/img/blog/第八届“图灵杯”D.png)

## 简要题解
![](https://dylolorz.cn/img/blog/第八届“图灵杯”D证明.png)

## 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <cstring>
#include <string>
using namespace std;
typedef long long LL;
typedef pair<int,int>PII;
const int N=100010;
LL dp[N],sz[N];
int main(void)
{
    LL t;
    cin>>t;
    while(t--)
    {
       int n,k;
       cin>>n>>k;
       if((n-1)%(k+1)!=0) cout<<"yo xi no forever!\n";
       else cout<<"ma la se mi no.1!\n";
    }
    //system("pause");
    return 0;
}

```

# E.Seek the Joker II
![](https://dylolorz.cn/img/blog/第八届“图灵杯”E.png)

## 简要题解
![](https://dylolorz.cn/img/blog/第八届“图灵杯”E证明.png)

## 题解代码
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <unordered_map>
#include <cstdio>
#include <cmath>
using namespace std;
int main(void)
{
    int t;
    cin>>t;
    while(t--)
    {
        int n,m;
        cin>>n>>m;
        int a=m-1,b=n-m;
        if(a>b)swap(a,b);
        double now=(sqrt(5.0)+1)/2;
        if((int)(now*(b-a))==a)cout<<"ma la se mi no.1!"<<endl;
        else cout<<"yo xi no forever!"<<endl;

    }
    //system("pause");
    return 0;
}
```

# F.成绩查询ing
![](https://dylolorz.cn/img/blog/第八届“图灵杯”F.png)

## 简要题解
<font size='4'>纯模拟题，注意不要tle就行了</font>

## 题解代码
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <unordered_map>
#include <cstdio>
#include <vector>
using namespace std;
string a,b;
struct node
{
    string name;
    int grade;
    int sex;
    int id;
}sz[100010];
unordered_map<string,int>mp;
vector<string>v[110];
int main(void)
{
    ios::sync_with_stdio(false);
    int n,m;
    cin>>n;
    for(int i=1;i<=n;i++)
    {
        cin>>sz[i].name>>sz[i].grade>>sz[i].sex>>sz[i].id;
        v[sz[i].grade].push_back(sz[i].name);
        mp[sz[i].name]=i;
    }
    for(int i=0;i<=100;i++)sort(v[i].begin(),v[i].end());
    cin>>m;
    for(int i=1;i<=m;i++)
    {
        int op;
        cin>>op;
        if(op==1)
        {
            string str;
            cin>>str;
            int pos=mp[str];
            cout<<sz[pos].grade<<" "<<sz[pos].id<<" "<<sz[pos].sex<<endl;
        }
        else
        {
            int x;
            cin>>x;
            for(int j=0;j<v[x].size();j++)
            {
                cout<<v[x][j]<<"\n";
            }
        }
    }
    //system("pause");
    return 0;
}
```

# G.贪吃的派蒙
![](https://dylolorz.cn/img/blog/第八届“图灵杯”G.png)

## 简要题解
![](https://dylolorz.cn/img/blog/第八届“图灵杯”G证明.png)

## 题解代码
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <unordered_map>
#include <cstdio>
#include <cmath>
using namespace std;
typedef long long LL;
const int N=100010;
LL a[N];
int main(void)
{
    int t;
    cin>>t;
    while(t--)
    {
        LL n,k,maxi=0,mini=0,flag=0,pre=0,sum=0,pre_num=0;
        cin>>n>>k;
        for(int i=1;i<=n;i++)
        {
            cin>>a[i];
            sum+=a[i];
            flag=max(flag,a[i]);
        }
        for(int i=1;i<=n;i++)
        {
            if(a[i]==flag)break;
            pre+=a[i];
            pre_num++;
        }
        LL l=0,r=1e8;
        while(l<r)
        {
            LL mid=l+r+1>>1;
            if((mid*((n-1)+flag)+pre_num)<=k)l=mid;
            else r=mid-1;
        }
        if((l*((n-1)+flag)+pre_num<=k)&&(l*sum+pre>=k))cout<<"YES"<<endl;
        else cout<<"NO"<<endl;
    }
    //system("pause");
    return 0;
}
```

# H.数羊
![](https://dylolorz.cn/img/blog/第八届“图灵杯”H.png)

## 简要题解
![](https://dylolorz.cn/img/blog/第八届“图灵杯”H证明.png)
## 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <cstring>
#include <string>
using namespace std;
typedef long long LL;
typedef pair<int,int>PII;
const int N=100010,mod=998244353;
LL f[N],sz[N],ans,t;
LL qmi(LL a,LL b,LL mod)
{
    LL res=1;
    while(b)
    {
        if(b&1)res=res*a%mod;
        b>>=1;
        a=a*a%mod;
    }
    return res;
}
int main(void)
{
    cin>>t;
    while(t--)
    {
        LL n,m;
        cin>>n>>m;
        if(m==0)
        {
            if(n==1)cout<<2<<endl;
            else cout<<(n+2)%mod<<endl;
        }
        else if(m==1)cout<<n*2%mod<<endl;
        else
        {
            LL res=qmi(2,n,mod);
            cout<<res<<endl;
        }
         
    }
    return 0;
}
```

# I.买花
![](https://dylolorz.cn/img/blog/第八届“图灵杯”I.png)

## 简要题解
<font size='4'>签到题，预处理出2^1,2^2...2^15次,判断一下能否整除</font>

## 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <cstring>
#include <string>
using namespace std;
typedef long long LL;
typedef pair<int,int>PII;
int main(void)
{
    LL t;
    cin>>t;
    vector<LL>v;
    LL now=1,pd=1;
    for(int i=1;i<=15;i++)
    {
        if(i!=1)v.push_back(now);
        pd*=2;
        now+=pd;
    }
    while(t--)
    {
       LL n;
       cin>>n;
       int flag=0;
       for(int i=0;i<v.size();i++)
       {
           if(n%v[i]==0)
           {
               flag=1;
               break;
           }
       }
       if(flag)cout<<"YE5"<<endl;
       else cout<<"N0"<<endl;
    }
    //system("pause");
    return 0;
}
```

# J.这是一题简单的模拟
![](https://dylolorz.cn/img/blog/第八届“图灵杯”J.png)

## 简要题解
<font size='4'>模拟题,unordered_map处理一下就行了</font>

## 题解代码
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <unordered_map>
using namespace std;
const int N=330,M=330*330;
int mz[N][N];
int n,m,sz[N*2];
unordered_map<int,int>mp;
int main(void)
{
    cin>>n>>m;
    for(int i=1;i<=m;i++)
    {
        int x,y,z;
        cin>>x>>y>>z;
        x++,y++;
        mz[x][y]=z;
        mz[y][x]=z;
    }
    int q;
    cin>>q;
    int ans=-1;
    while(q--)
    {
        int cnt=0;
        cin>>cnt;
        mp.clear();
        sz[1]=1;
        for(int i=2;i<=cnt+1;i++)
        {
            cin>>sz[i];
            sz[i]++;
        }
        sz[cnt+2]=1;
        int flag=0,res=0;
        int tot=0;
        for(int i=2;i<=cnt+2;i++)
        {
            if(mz[sz[i-1]][sz[i]]==0)
            {
                flag=1;
                break;
            }
            res+=mz[sz[i-1]][sz[i]];
            if(i!=1&&mp[sz[i]])
            {
                flag=1;
                break;
            }
            mp[sz[i]]=1;
            if(sz[i]!=1)tot++;
        }
        if(flag)continue;
        if(tot!=n)continue;
        if(ans==-1)ans=res;
        else ans=min(ans,res);
    }
    cout<<ans;
   // system("pause");
    return 0;
}
```

# K.黑洞密码
![](https://dylolorz.cn/img/blog/第八届“图灵杯”K.png)

## 简要题解
<font size='4'>签到题，把字母和数字分开存储,字母为a[i],数字b[i],4个一轮考虑,a[i]后推b[i]个再反转就行</font>

## 题解代码
```cpp
#include <iostream>
#include <cstring>
#include <algorithm>
#include <unordered_map>
using namespace std;
const int N=330,M=330*330;
string a,b;
int main(void)
{
    string str;
    cin>>str;
    for(int i=0;i<str.size();i++)
    {
        if(str[i]>='0'&&str[i]<='9')b+=str[i];
        else a+=str[i];
    }
    string temp;
    for(int i=0;i<16;i++)
    {
        for(int j=0;j<(b[i]-'0');j++)
        {
            if(a[i]=='z')a[i]='B';
            else if(a[i]=='Z')a[i]='b';
            else a[i]+=1;
        }
        temp+=a[i];
        if(i%4==3)
        {
            for(int j=3;j>=0;j--)cout<<temp[j];
            temp="";
        }
    }
    //system("pause");
    return 0;
}
```

# L.建立火车站
![](https://dylolorz.cn/img/blog/第八届“图灵杯”L.png)

## 简要题解
![](https://dylolorz.cn/img/blog/第八届“图灵杯”L证明.png)

## 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <vector>
#include <unordered_map>
#include <algorithm>
#include <cstring>
#include <string>
#include <queue>
using namespace std;
typedef long long LL;
typedef pair<int,int>PII;
const int N=100010,mod=998244353;
LL sz[N];
struct node
{
    LL num,l,r,res;
};
struct cmp
{
    bool operator()(const node&A,const node&B)
    {
        return A.num<B.num;
    }
};
int main(void)
{
    LL t;
    t=1;
    while(t--)
    {
        int n,k;
        cin>>n>>k;
        priority_queue<node,vector<node>,cmp>q;
        int flag1=0;
        for(int i=1;i<=n;i++)
        {
            cin>>sz[i];
            if(i>=2&&sz[i]!=sz[i-1])flag1=1;
        }
        sort(sz+1,sz+n+1);
        for(int i=2;i<=n;i++)
        {
            if(sz[i]-sz[i-1]>1)q.push({sz[i]-sz[i-1],sz[i-1],sz[i],1});
        }
        int cnt=0;
        while(q.size())
        {
            if(cnt==k)break;
            cnt++;
            node u=q.top();
            q.pop();
            LL jg=u.r-u.l;
            LL po=(jg%(u.res+1))==0?jg/(u.res+1):jg/(u.res+1)+1;
            if(po==1)continue;
            q.push({po,u.l,u.r,u.res+1});
        }
        if(!q.size())cout<<1<<endl;
        else cout<<q.top().num<<endl;

    }
    //system("pause");
    return 0;
}
```