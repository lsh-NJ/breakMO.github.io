## prim三部曲：

1. 选择距离生成树最近的节点
2. 把最近节点加入生成树
3. 更新非生成树节点到生成树的距离

> 使用一维数组存储最小生成树

## 记录树的细节分析：

* 树的特点是入度为1，所以记录父节点不会出现链接关系被覆盖的情况

```cpp
#include <bits/stdc++.h>
using namespace std;
int main() {
    int n, m, s, e, val;
    cin >> n >> m;
    vector<vector<int>> graph(n + 1, vector<int>(n + 1, INT_MAX));
    //记录树+
    vector<int> parent(n + 1, -1);
    for(int i = 0; i < m; i++) {
        cin >> s >> e >> val;
        graph[s][e] = val;
        graph[e][s] = val;
    }

    vector<bool> visted(n + 1, false);
    vector<int> miniDist(n + 1, INT_MAX);
    miniDist[1] = 0;

    for(int i = 0; i < n; i++) {
        int cur = 0;
        //寻找最近距离的点
        for(int j = 1; j <= n; j++) {
            if(!visted[j] && miniDist[j] < miniDist[cur]) {
                cur = j;
            }
        }
        //将该标记为visited
        visted[cur] = true;
        //更新miniDist数组
        for(int j = 1; j <= n; j++) {
            if(!visted[j] && miniDist[j] > graph[cur][j]) {
                miniDist[j] = graph[cur][j];
                //记录点的连接关系+
                parent[j] = cur;
            }
        }
    }
    //输出 最小生成树
    int res = 0;
    for(int i = 1; i <= n; i++) {
        res += miniDist[i];
    }
    cout << res << endl;

    // 输出 最小生成树边的链接情况
    for (int i = 1; i <= v; i++) {
        cout << i << "->" << parent[i] << endl;
    }
    return 0;
}
```