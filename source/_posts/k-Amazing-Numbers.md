---
title: k-Amazing Numbers
date: 2020-11-4
tags: 
    - 思维
    - 数学
categories: Codeforces
cover: https://dylolorz.cn/img/blog/5.jpg
---

# 题目来源<br/>
<font size="4">[https://codeforces.com/contest/1417/problem/C](https://codeforces.com/contest/1417/problem/C)</font>
<!-- more -->

# 题目原文
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201105184930453.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R5bG9sb3J6,size_16,color_FFFFFF,t_70#pic_center)

# 题目描述
<font size="3" > 给定一个序列，统计这个序列长度为1-n长度的连续子序列的分别公共最小值，不存在输出-1。</font>

# 题解思路

<font size="3" >首先统计相同的数在序列中的最大间隔，包括此数对序列头，序列尾的间隔（利用map记录此数字上一次出现的index下标即可）。此间隔就是能取到这个数字为贡献的最小序列长度。然后对于每个数字能做出贡献的最小代价长度进行更新，例如数字4，2都最小要长度3的子序列才可以取到，那么ans[3]就更新成最小的数字2。最后输出即可。（输出时注意当第一次 不为-1后，后面都要更新最小，因为假设长度为3的最小值为2。那后面的答案一定不会大于2）</font>

# 题解代码
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <string>
#include <algorithm>
#include <unordered_map>
using namespace std;
const int N=3*100010;
int ans[N],sz[N],st[N];
unordered_map<int,int>mp;
int main(void)
{
    int t;
    cin>>t;
    while(t--)
    {
        int n;
        cin>>n;
        mp.clear();
        memset(st,0,sizeof st);
        memset(ans,0x3f,sizeof ans);
        for(int i=1;i<=n;i++)
        {
            scanf("%d",&sz[i]);
        }
        for(int i=1;i<=n;i++)//求取每个数的最大间隔（已经包括序列首）
        {
            int x=sz[i];
            st[x]=max(st[x],i-mp[x]);
            mp[x]=i;
        }
        for(int i=1;i<=n;i++)//处理序列尾 例如 2 2 3 4 5 （2到序列尾最小间隔为4）
        {
            int x=sz[i];
            st[sz[i]]=max(st[sz[i]],n+1-mp[sz[i]]);
        }
        for(int i=1;i<=n;i++)//对每个数字所归属的间隔长度，取最小的数字
        {
            int x=sz[i],p=st[x];
            ans[p]=min(ans[p],x);
        }
        int res=0x3f3f3f3f;
        int flag=1;
        for(int i=1;i<=n;i++)//输出答案
        {
            if(flag&&ans[i]==0x3f3f3f3f)printf("-1 ");
            else
            {
                flag=0;//第一次走出-1后，后面更新最小输出。
                if(ans[i]!=-1)res=min(res,ans[i]);
                printf("%d ",res);
            }
        }
        printf("\n");
    }
    return 0;
}
```
