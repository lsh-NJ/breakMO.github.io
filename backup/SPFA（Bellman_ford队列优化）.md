## 解析：

1. 相对于普通版优化掉了被`if(!minDist[start])`排除的无效松弛

    * 通过队列存储可以对周围进行有效松弛的点
2. 为什么队列中不能同时存在一个点但是队列中可以多次存在一个点？

    * 有可能先接触到的点的最短距离还可以进行松弛，那么之后的点位都需要继续进行松弛，通过队列的形式也恰巧可以再次发散松弛后续节点并排除已松弛到最佳的节点

## 注意：

* `queue`容器要使用`front()`
* `top()`函数用于`stack`\\`priority_queue`容器
* 依然对每个遍历到的点都要进行`minDist`最短距离的刷新
* 只在队列是否要插入点时判断点是否已经在队列中

## 优化 检查负权回路：

* 记录点进入队列的次数就相当于记录了松弛的次数

## 代码：

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n, m, s, e, val;
    cin >> n >> m;
    vector<list<pair<int, int>>> grid(n + 1);
    for(int i = 0; i < m; i++) {
        cin >> s >> e >> val;
        grid[s].push_back({e, val});
    }
    
    vector<int> minDist(n + 1, INT_MAX);
    vector<int> inQueue(n + 1, false);//记录已经在队列中的元素
    minDist[1] = 0;
    queue<int> q;
    q.push(1);
    inQueue[1] = true;
    vector<int> count(n + 1, 0);//记录节点加入队列的次数
    bool flag = false;//记录是否存在负权回路
    
    while (!q.empty())
    {
        int cur = q.front();
        q.pop();
        inQueue[cur] = false;
        for(pair<int, int> edge:grid[cur]) {
            int to = edge.first;
            int val = edge.second;
            if(val + minDist[cur] < minDist[to]) {
                minDist[to] = val + minDist[cur];
                //已经在队列中不用重复添加
                if(!inQueue[to]) {
                    inQueue[to] = true;
                    q.push(to);
                    count[to]++;
                    if(count[to] == n) {//松弛超过n - 1次
                        flag = true;
                        while(!q.empty()) q.pop();
                        break;
                    }
                }
            }
        }
    }
    
    if(flag) cout << "circle" << endl;
    else
        minDist[n] == INT_MAX? cout << "unconnected" << endl: cout << minDist[n] << endl;
    return 0;
}
```