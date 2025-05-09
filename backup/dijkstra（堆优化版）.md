## 图的表示方式：

1. ### 邻接矩阵

    * #### 优点：

      * 检查任意两个顶点间是否存在边的操作非常快
      * 适合稠密图，在边数接近顶点数平方的图中，邻接矩阵是一种空间效率较高的表示方法。
    * #### 缺点：

      * 遇到稀疏图，会导致申请过大的二维数组造成空间浪费 且遍历 边 的时候需要遍历整个n \* n矩阵，造成时间浪费
2. ### 连接表

    * #### 优点：

      * 对于稀疏图的存储，只需要存储边，空间利用率高
      * 遍历节点链接情况相对容易
    * #### 缺点：

      * 检查任意两个节点间是否存在边，效率相对低，需要 O(V)时间，V表示某节点链接其他节点的数量。

## 细节处理：

1. 小顶堆实现：自定义比较器，返回值是前一个数大于后一个数
2. 小顶堆存储的和朴素版一致，是`miniDist`的值，即存储到达原点的最小距离的原理

## 代码实现：

```cpp
#include <bits/stdc++.h>
using namespace std;
/**
 * dijkstra堆优化版
 * 代码的模块：
 * 1.图的构造
 * 2.小顶堆的实现
 * 3.将起始位置进行初始化处理
 * 4.进行三部曲
 */

class Edge {
public:
    int to;
    int val;
    Edge(int t, int v) {
        to = t;
        val = v;
    }
};

class mycomparison {
public:
    bool operator()(const pair<int, int> &lhs, const pair<int, int> &rhs) {
        return lhs.second > rhs.second;//小顶堆返回做大于右
    }
};

int main() {
    int n, m, s, e, v;
    cin >> n >> m;

    //图构造
    vector<list<Edge>> grid(n + 1);
    for(int i = 0; i < m; i++) {
        cin >> s >> e >> v;
        Edge edge(e, v);
        grid[s].push_back(edge);
    }

    //小顶堆
    priority_queue<pair<int, int>, vector<pair<int, int>>, mycomparison> pq;
    int start = 1;
    int end = n;
    vector<int> miniDist(n + 1, INT_MAX);
    vector<bool> visited(n + 1, false);

    //处理初始位置
    pq.push(pair<int, int>(start, 0));
    miniDist[start] = 0;

    //开始寻找最小路
    while(!pq.empty()) {
        //选定当前点
        pair<int, int> cur = pq.top();
        pq.pop();
        if(visited[cur.first]) continue;
        visited[cur.first] = true;//标记为遍历过
        for(Edge edge : grid[cur.first]) {//遍历所有当前点可以到达的点来更新距离数据并将边加入小顶堆
            if(!visited[edge.to] && edge.val + miniDist[cur.first] < miniDist[edge.to]) {
                miniDist[edge.to] = edge.val + miniDist[cur.first];
                pq.push(pair<int, int>(edge.to, miniDist[edge.to]));
            }
        }
    }
    if(miniDist[end] == INT_MAX) cout << -1 << endl;
    else cout << miniDist[end] << endl;
    return 0;
}
```