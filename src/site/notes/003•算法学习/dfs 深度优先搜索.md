---
{"dg-publish":true,"permalink":"/003/dfs/","tags":["算法","dfs"]}
---


```c++
#include <bits/stdc++.h>
using namespace std;

int n;
int book[10001];
int ans[10001];

void dfs(int step)
{
    if(step == n+1)
    {
        for (int i = 1; i <= n;i++)
        {
            cout << ans[i];
        }
        cout << endl;
        return;
    }
    for (int i = 1; i <= n;i++)
    {
        if(book[i]==0)
        {
            book[i] = 1;
            ans[step] = i;
            dfs(step + 1);
            book[i] = 0;
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