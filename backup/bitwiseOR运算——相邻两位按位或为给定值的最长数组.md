# [[1988C - Increasing Sequence with Fixed OR](https://codeforces.com/problemset/problem/1988/C)](https://codeforces.com/problemset/problem/1988/C)

- C++的`long long`类型可以接受最多**<u>63</u>**次`<<`运算！！！
- 对$2^{n}$进行移位运算时1要是`long long`类型，防止数值循环导致错误
- `1 << -1`虽然未定义，但可以认为结果是0

#### 解题：

- 第一个数不能占用最高位
- 每相邻的两个数`|`，意味着`n`的每个二进制1至少需要一个数具有，且要满足递增的条件，可以想到对n的所有二进制1进行挖空，要使符合要求的数组最长，每次只挖一个空可以使得梯度最小

  且需要注意当n为$2^{n}$时挖空会得到不是正整数的0，因此要`(x != n)`避免这种情况

  ```cpp
  	vector<long long> res;
          for(int i = 62; i >= -1; i--) {
              long long x = (long long)1 << i;
              if((x & n) == x && (x != n)) {
                  res.push_back(n - x);
              }
          }
  ```