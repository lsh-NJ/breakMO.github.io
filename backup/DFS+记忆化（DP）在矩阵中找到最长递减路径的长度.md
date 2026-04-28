# DFS+记忆化（DP）

- 使用动态规划记录每个节点的最大长度，当再次搜索到该节点的时候就可以直接返回值了。将复杂度降为了O(n*m)

```cpp
// 在矩阵中找到最长递减路径的长度
#include<bits/stdc++.h>
using namespace std;
int res = 0;
int n, m;
vector<vector<int>> grid;
vector<vector<int>> dp;

int dir[][2] = {{1, 0},{0,1},{0,-1},{-1,0}};
int DFS(int x, int y) {
    if(dp[x][y] != 0) return dp[x][y];
    dp[x][y] = 1;
    for(int i = 0;i<4;i++) {
        int nx = x + dir[i][0];
        int ny = y + dir[i][1];
        if(nx >= 0 && nx < n && ny >= 0 && ny < m)
            if(grid[nx][ny] < grid[x][y]) 
                dp[x][y] = max(dp[x][y], DFS(nx, ny) + 1);
    }
    return dp[x][y];
}

int main() {
    cin >> n>>m;
    list<pair<int, int>> index;
    grid.assign(n, vector<int> (m));
    dp.assign(n, vector<int> (m));
    int x = 0, y = 0;
    for(int i = 0; i < n; i++) for(int j = 0;j<m;j++) 
        cin >> grid[i][j];
    for(int i = 0; i < n; i++) for(int j = 0;j<m;j++) 
        res = max(DFS(i, j), res);
    cout << res << endl;
}
```