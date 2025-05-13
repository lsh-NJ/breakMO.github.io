> 思路特别像prim

## 过程：

* 对`m`条边进行`n - 1`（点数-1）次松弛，更新每个点到原点的最短距离`minDist[to] = min(minDist[to], minDist[start] + val);`
* 理论上，i次松弛使相应节点有距离i条边的最短距离（有也就是说大于i次松弛可能会找到距离边数更多但更短的距离）

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, m, s, e, val;
    cin >> n >> m;

	//用来存放边与其权值的数组
    vector<vector<int>> grid;
    for(int i = 0; i < m; i++) {
        cin >> s >> e >> val;
        grid.push_back({s, e, val});
    }

	//存放距离原点的最短总距离
    vector<int> minDist(n + 1, INT_MAX);
    minDist[1] = 0;

    //n - 1次松弛
    for(int i = 0; i < n - 1; i++) {
        //对每一条边进行松弛
        for(int j = 0; j < m; j++) {
            int start = grid[j][0];
            int to = grid[j][1];
            int val = grid[j][2];
			//松弛的过程
            if(minDist[start] != INT_MAX && minDist[start] + val < minDist[to]) {
                minDist[to] = minDist[start] + val;
            }
        }
    }

    minDist[n] == INT_MAX? cout << "unconnected" << endl: cout << minDist[n] << endl;
}
```