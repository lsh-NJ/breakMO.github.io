# **[[H](http://10.160.111.129/p/2664?tid=687f5437c9d615d80a0f28ce)](http://10.160.111.129/p/2664?tid=687f5437c9d615d80a0f28ce)**[ [ 宫城](http://10.160.111.129/p/2664?tid=687f5437c9d615d80a0f28ce)](http://10.160.111.129/p/2664?tid=687f5437c9d615d80a0f28ce)

# 数学概念：

- 余的数学表达式$k\bmod i=k-\lfloor\frac{k}{\mathrm{i}}\rfloor\cdot\mathrm{i}$，则$\sum_{i=1}^{n}k\bmod i=n\cdot k-\sum_{i=1}^{n}i\cdot\lfloor\frac{k}{\mathrm{i}}\rfloor$
- 其中$\lfloor\frac{k}{\mathrm{i}}\rfloor$会出现多个连续的$i$对应相同的数值的情况，可以以此来减少算法的复杂度

- $\sum_{i=1}^{n}i\cdot\lfloor\frac{k}{\mathrm{i}}\rfloor$可以分为多个值相同的段，划定左右边界，左边界是$l $（当前位置），右边界$r$是和当前位置的$\lfloor\frac{k}{l}\rfloor $值相同的最大值，就是$r = \min\left( \left\lfloor \frac{k}{\left\lfloor \frac{k}{l} \right\rfloor} \right\rfloor, n \right)$
- 设这段连续的相同值为$v=\lfloor\frac{k}{\mathrm{i}}\rfloor$，就相当于当前值乘以一个等差数列
- 即总和为：$v\cdot\sum_{i=l}^{r}i=\frac{(v\cdot l+v\cdot r)\cdot(r-l+1)}{2}=v\cdot\frac{(l+r)\cdot(r-l+1)}{2}$

### 算法：

```cpp
ans += k * n;
for(ll l = 1, r; l <= n; l = r + 1) {
	r = min(n, k / (k / l));
	ans -= (l + r) * (r - l + 1) * (k / l) / 2;
}
```