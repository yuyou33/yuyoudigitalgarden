---
{"dg-publish":true,"permalink":"/003/dfs/","tags":["算法","dfs","图论","最短路径"]}
---

### 题目
输出n的**全排列**
形象化:  将1到n的扑克牌投入到n个盒子中
### 代码
```c++
#include <bits/stdc++.h>
using namespace std;

int n;
int book[10001];//记录i号扑克牌是否在手中
int ans[10001];//记录第i个盒子投入的扑克牌

void dfs(int step)//step当前站在的盒子序号
{
    if(step == n+1)//如果盒子遍历完
    {
        for (int i = 1; i <= n;i++)
        {
            cout << ans[i];
        }
        cout << endl;
        return;//这层递归调用结束
    }
    for (int i = 1; i <= n;i++)
    {
        if(book[i]==0)
        {
            book[i] = 1;//标记
            ans[step] = i;//记录答案
            dfs(step + 1);
            book[i] = 0;//取消这一步的标记
        }
    }
}

int main()
{
    cin >> n;
    dfs(1);
    return 0;
}
```

### 运行示例
```
输入:
3

输出:
123
132
213
231
312
321
```

### 题目
