## 核心思想：

- 动态规划

## 思路：

- 按照动态规划的基本步骤:

  1. 确定dp数组及其下标的意义：`grid[i][j][k] = m`，表示 节点`i`到 节点`j`以`[1...k]`集合中的一个节点为中间节点的最短距离为`m`。
  2. 确定递推公式的两种情况：

      1. 节点`i` 到 节点`j` 的最短路径经过节点`k`

          `grid[i][j][k] = grid[i][k][k - 1] + grid[k][j][k - 1]`

          > 为什么中间点集不能是`[k...n]`？
          >
          > 这里中间点只是在某一个集合中，只是`[1...k]`集合更符合动态规划的原理
          >
      2. 节点`i` 到 节点`j` 的最短路径不经过节点`k`

          `grid[i][j][k] = grid[i][j][k - 1]`

      那么最短路径就是以上两种情况的最小值，即`grid[i][j][k] = min(grid[i][k][k - 1] + grid[k][j][k - 1]， grid[i][j][k - 1])`
  3. 数组的初始化：

      `grid[i][j][0]`是两个点直接连接的路径长度
  4. 遍历顺序：

      `k`要在最外层遍历，方便进行数组从三位数组的最底层进行递推

## 注意：

- 图初始化值不能为`INT_MAX`，因为有求和的部分，`INT_MAX`遇到求和会出现很多问题

## 代码：

```cpp
#include<bits/stdc++.h>
using namespace std;


int main() {
    ios::sync_with_stdio(0);cin.tie(0);
    int n, m; cin >> n >> m;
    int s, e, val;
    //保存图以及各种最短路径，是多源最短路动态规划的dp数组
    vector<vector<vector<int>>> grid(n + 1, vector<vector<int>>(n + 1, vector<int>(n + 1, 10005)));
    for(int i = 0; i < m; i++) {
        cin >> s >> e >> val;
        grid[s][e][0] = val;
        grid[e][s][0] = val;
    }
    
    

    for(int k = 1; k <= n; k++) {
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= n; j++) {
                // cout << "k:" << k << "i:" << i << "j:" << j << endl;
                // cout << grid[i][j][k - 1] << " " << grid[i][k][k - 1] + grid[k][j][k - 1] << endl;
                //在“k不是i到j最短路径经过的节点”和“k是i到j最短路径经过的节点”之中取最小值
                grid[i][j][k] = min(grid[i][j][k - 1], grid[i][k][k - 1] + grid[k][j][k - 1]);
            }
        }
    }

    int q; cin >> q;
    for(int i = 0; i < q; i++) {
        cin >> s >> e;
        if(grid[s][e][n] == 10005) cout << -1 << endl;
        else cout << grid[s][e][n] << endl;
    }
}
```