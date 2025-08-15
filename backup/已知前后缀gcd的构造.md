[[E - G-C-D, Unlucky!](https://codeforces.com/contest/2126/problem/E)](https://codeforces.com/contest/2126/problem/E)

# 思路：

- 对前缀gcd和后缀gcd进行化简，同时除以所有数字的最大公约数（原数组也进行相同的操作）
- 对于每一个位置上的数字，满足$\operatorname{\mathrm{gcd}}\left(x_{i},p_{i-1}\right)=p_{i}$即$\operatorname{\mathrm{gcd}}\left(\frac{x_{i}}{p_{i}},\frac{p_{i-1}}{p_{i}}\right )=1$，对于后缀同理，那么只要将每一位上的数字改为$p_{i}$ $s_{i}$的最小公倍数再进行前后缀gcd的互素判断就可以了