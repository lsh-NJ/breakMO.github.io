# [[1903B - StORage room](https://codeforces.com/problemset/problem/1903/B)](https://codeforces.com/problemset/problem/1903/B)

#### 思路:

- ai | aj = Mi,j ，则说明 Mi,j 二进制中的 1 分式中可能有 1 ，二进制中的 0 分式中不可能有 1 ，就想到可以让有关任意 i 的 Mi,j 进行“累&”操作，获得可以满足要求的 ai
- 之后再检查是否满足条件就可以了


#### 为什么要进行检查？

- 题目中明确说明存在无法构造的情况。以上的方法一定可以得到一个确切的结果，那么不根据数学推导也需要判断其合理性。
- 因为ai 和 aj 中相应位置只要有一个 1 就可以了，但我们不好根据这个要求进行构造，只能在所有数字都满足各自的要求以后再进行组合进行暴力判断合理性


这是一种**<u>暴力/贪心</u>**的方法
```cpp
vector<int> res(n + 1, (1 << 30) - 1);
        //拟合所有值
        for(int i = 1; i <= n; i++) for(int j = i + 1; j <= n; j++) {
            res[i] &= grid[i][j];
            res[j] &= grid[i][j];
        }

        //检查合理性
        bool flag = 1;
        for(int i = 1; i <= n; i++) for(int j = i + 1; j <= n; j++) {
            if(grid[i][j] != (res[i] | res[j])) {
                flag = 0;
                break;
            }
        }
```