[[跳转题目](https://codeforces.com/contest/2118/problem/B)](https://codeforces.com/contest/2118/problem/B)

## 思路：

1. 要想构造一个排列皆为全排列的`n * n`矩阵，考虑使其变成循环的形式：

    > 1 2 3 4
    >
    > 2 3 4 1
    >
    > 3 4 1 2
    >
    > 4 1 2 3
    >
2. 该如何通过反转构造出这样的矩阵呢？

    不好构造，想一想类似的更容易构造的循环形式

    > 1 4 3 2
    >
    > 2 1 4 3
    >
    > 3 2 1 4
    >
    > 4 3 2 1
    >

    （话说简单试一试就能试出来好吧？一个小时没发现这样的构造有点糖了吧？）

    按照层序递进的进行反转（`swap(1, i);swap(i + 1, n)`）可以看出是一种逆序的循环，可以满足`2n`操作数要求

## 代码:

```cpp
#include<bits/stdc++.h>
using namespace std;

void work() {
    int n; cin >> n;
    vector<vector<int>> res;
    for(int i = 1; i <= n; i++) {
        if(1 < i) {
            res.push_back({i, 1, i});
        }
        if(i + 1 < n) {
            res.push_back({i, i + 1, n});
        }
    }
    cout << res.size() <<endl;
    for(vector<int> r : res) {
        cout << r[0] << " " << r[1] << " " << r[2] << endl;
    }
}

int main() {
    int t; cin >> t;
    while(t--) work();
    return 0;
}
```