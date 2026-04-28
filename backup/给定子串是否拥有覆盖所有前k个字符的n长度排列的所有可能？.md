[[ 1924A - Did We Get Everything Covered?](https://codeforces.com/problemset/problem/1924/A)](https://codeforces.com/problemset/problem/1924/A)

## 思路：

- 通过贪心的方式寻找到字符串中最难以构成的串：

  > 尽量往后拖，即选择第一次出现的最晚的字符作为子串的一部分
  >
- 如果以这样最拖延的手法还是形成了完整的子串，那么答案无疑是YES
- 如果这样的手法没能形成完整的子串就补充最终后缀中没有的元素。