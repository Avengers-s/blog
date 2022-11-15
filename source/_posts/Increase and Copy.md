---
title: Increase and Copy
date: 2020-11-1
tags: 
    - 思维
    - 数学
categories: Codeforces
cover: https://dylolorz.cn/img/blog/p1.jpg
---

# 题目来源<br/>
<font size="3">[https://codeforces.com/contest/1426/problem/C](https://codeforces.com/contest/1426/problem/C)</font>

<!-- more -->

# 题目原文
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201101165824116.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2R5bG9sb3J6,size_16,color_FFFFFF,t_70#pic_center)

# 题目描述
<font size="3" >T组数据，每组给一个n，原始序列为1,每次可以进行如下两个操作之一，问使序列和大于等于n，至少需要多少次操作。

1. 在序列中将一个数增加1

2. 选择序列中一个数将其添加到序列尾

</font>

# 题解思路
<font size="3" >
&emsp;首先明确一点，最优解一定是先将1加到某个数x，再将x不断添加到序列中直到和大于等于n，(因为假设出现先添加此数到序列中，再将此数加1的情况，我们将其操作顺序反转，得到的贡献值一定是变大的)。<br>
&emsp;那么我们的问题就变成了寻找到此界限x，使总操作数最小。(其实这里已经可以猜测为对勾函数)<br>
&emsp;首先，将1变到x，需要x-1步操作，其次，将x数复制y份直到总和≥n,因此此处需要的操作数简单推导为(n+(x-1))/x-1，与前面的步骤相加化简即为x+(n-1)/x-1，前面则为对勾函数，函数最小值在根号(n-1)处取到，但由于我们操作数为整数步，因此我们需要取x为(int)sqrt(n-1)和(int)sqrt(n-1)+1两个值取较小值。代入函数即为答案。
</font>

# 代码如下
```cpp
#include <iostream>
#include <cstring>
#include <string>
#include <cstdio>
#include <algorithm>
#include <cmath>
using namespace std;
int t,n;
int main(void)
{
    cin>>t;
    while(t--)
    {
        cin>>n;
        if(n==1)
        {
            cout<<0<<endl;
            continue;
        }
        int p1=sqrt(n-1);
        int p2=p1+1;
        int ans=min((p2+(n-1)/p2-1),(p1+(n-1)/p1-1));
        cout<<ans<<endl;
    }
    //system("pause");
    return 0;
}

```