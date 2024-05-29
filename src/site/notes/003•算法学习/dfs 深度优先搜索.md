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
由起点到终点的最小步数问题(**最短路径**)
![003dfs1.png](/img/user/003dfs1.png)

### 代码
```c++
#include <bits/stdc++.h>
using namespace std;

int next1[4][2] = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};//按右下左上的顺序
int a[51][51];//记录图的信息
int book[51][51];//记录走过的坐标
int p, q, startx, starty;//终点坐标和起点坐标
int min1 = 99999; //记录最小步数
int m, n;//行列

void dfs(int x, int y, int step)//当前坐标和已走过步数
{
    if(x == p && y == q)
    {
        if(step < min1)
        {
            min1 = step;
        }
        return;
    }
    int tx = x, ty = y;
    for (int i = 0; i < 4;i++)
    {
        tx = x + next1[i][0];
        ty = y + next1[i][1];
        if(tx>=m ||tx<0 ||ty>=n ||ty<0 ||a[tx][ty] ==1 || book[tx][ty] == 1)//判断出界或者遇到障碍物或者走过
        {
            continue;
        }
        book[tx][ty] = 1;
        dfs(tx, ty, step + 1);
        book[tx][ty] = 0;
    }
    return;
}


int main()
{
    cin >> m >> n;
    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < n; j++)
        {
            cin >> a[i][j];
        }
    }
    cin >> startx >> starty;
    cin >> p >> q;
    book[startx][starty] = 1;
    dfs(startx, starty, 0);
    cout << min1;
    return 0;
}
```

### 运行示例
```
输入:
5 4
0 0 1 0
0 0 0 0
0 0 1 0
0 1 0 0
0 0 0 1
0 0 3 2


输出:
7
```