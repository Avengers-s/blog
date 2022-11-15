---
title: Cyclic Permutations
date: 2020-8-10
tags:
    - 快速幂
    - 思维
    - 数学
categories: Codeforces
cover: https://dylolorz.cn/img/blog/2.jpg
---

# 题目来源<br/>
<font size="4">[https://codeforces.com/contest/1391/problem/C](https://codeforces.com/contest/1391/problem/C)</font>
<!-- more -->

# 题目原文

![原文图片](https://img-blog.csdnimg.cn/20200810125947604.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R5bG9sb3J6,size_16,color_FFFFFF,t_70)


<font size="3" >证明如下：

 - 首先存在上述情况的排列一定满足，对于a[i]和a[i+2]，如果a[i]>a[i+2]，则a[i+2]向左找第一个大于它的数则为a[i]，所以a[i]和a[i+2]相连，反之如果a[i]<a[i+2]同理。而对于a[i+1]，向左向右和a[i]，a[i+2]相连，因此三者形成了一个简单环
 - 不存在只含有不相邻的三个数满足上述关系的排列，且假设存在，由于简单环定义为v1...vk，为连续段，也不满足，下面给出不存在只含这样关系排列的证明。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200810134622378.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R5bG9sb3J6,size_16,color_FFFFFF,t_70)

 - 对于一个简单环中大于等于4个数且不存在其中3个数满足上述情况的排列，不会成立</font>

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/202008101402547.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R5bG9sb3J6,size_16,color_FFFFFF,t_70)


 <font size="3" >而在推算公式的时候，正面计算会出现大量重复，对于n-1个数分别当选三角关系中的最小值且在剩下的比它大的数中取出2个组成三角关系，将剩下的数进行全排列，假设剩下的数为x，则会出现x+1个空位，将此三角插入空位计算出满足的数量，而这种计算方法中剩余的全排列中可能会存在三角关系，因此会有重复出现，计算麻烦，而此也启示我们反向思考会很简单。
 
 对于反向思考，即一个三角关系也不存在的排列即为不合法排列，而这样的排列即为如下图的排列，任何三个数都不可能组成为上述三角关系。最大值n摆放好，剩下的n-1个可以选择放在n左边或者右边，而不论放在哪边，它在这一边的位置都是固定的，因为要满足单调。</font>

 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200810141545247.png)

 <font face="雅黑" size="3">而这样的排列公式则为全排列n！-2的n-1次。（2的n-1次运用快速幂可以得出）下面给出代码</font>

 ```cpp
#include <iostream>
#include <cstdio>
using namespace std;
typedef long long LL;
const LL mod=1e9+7;
LL qmi(LL a,int b,LL mod)
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
    int n;
    LL x=1;
    cin>>n;
    for(int i=1;i<=n;i++)x=x*i%mod;
    LL t=qmi(2,n-1,mod);
    cout<<((x-t)+mod)%mod;
    return 0;
}
 ```
