## 思路：

- 本题的目的是找到所有可达路径中最大边权的最小值，已知的图论算法都无法完成这个任务，这个最小的最大值属实诡异
- 但是可以在道路的可达性上下手，比如找到了一个路径，他的边权最大值是max，我们只知道这是一条通路的一个答案，其他通路没有有效的方式查找。那就压缩max，使得能通过的最大边小于max，再次进行寻路就可以不走这条路，换一条最大边权更小的路。能通过就继续缩小这个值，直到再小就找不到可以通过的路为止。
- 这样的思路是否可以用来寻找很多个有效路径？

## 答案代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int INF = 1e9 + 11;//某条边的最大值（答案的最大值）都不可能超过这个数

struct edge {
    int t, w;
    edge(int t, int w) : t(t), w(w) {}
};

void solve() {
    int n, m;
    cin >> n >> m;
    vector<int> b(n);
    for (auto &x : b) {
        cin >> x;
    }
    vector<vector<edge>> graph(n);
    for (int i = 0; i < m; ++i) {
        int s, t, w;
        cin >> s >> t >> w;
        --s; --t;
        graph[s].push_back(edge(t, w));
    }

    //检查最大值为maxW是否可以走完全程
    auto check = [&](int maxW) {
        vector<int> best(n, 0);//记录i - 1节点处机器所能携带的最小电池数
        for (int i = 0; i < n; ++i) {
            if (i > 0 && best[i] == 0) {//best[i] = 0 表示该点无法到达，就直接跳过
                continue;
            }
            best[i] += b[i];//先让机器人在该节点获得该节点的全部电池，之后再进行优化
            best[i] = min(best[i], maxW);//携带的电池不能超过上限
            for (auto p : graph[i]) {//对当前节点可达的节点进行最小电池数量的更新
                if (p.w <= best[i]) {//只有可以到达的点进行更新，所以i > 0 && best[i] == 0的点不可达
                    best[p.t] = max(best[p.t], best[i]);//可以看出这里找到的是maxW之下的最大电池携带数量
                    //由此可以看出本题的大致思路是：不断调整maxW的值，直到找到最小的那个，就是能携带的最小的电池数量
                }
            }
        }
        return (best.back() > 0);
    };

    if (!check(INF)) {
        cout << -1 << endl;
        return;
    }
    //通过二分来逼近上限
    int l = 0, r = INF;
    while (r - l > 1) {
        int mid = (l + r) / 2;
        if (check(mid)) {
            r = mid;
        } else {
            l = mid;
        }
    }
    cout << r << endl;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);
    int t;
    cin >> t;
    while (t--) {
        solve();
    }
    return 0;
}
```