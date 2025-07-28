[[D - Match, Mod, Minimize 2](https://atcoder.jp/contests/abc416/tasks/abc416_d)](https://atcoder.jp/contests/abc416/tasks/abc416_d)

# 思路：

- 要求$\sum_{i=1}^{N}\left(\left(A_{i}+B_{i}\right)\bmod M\right)$，可以通过讨论转化问题：

  1. $A_{i}+B_{i}<M$:

      $\sum_{i=1}^{N}\left(\left(A_{i}+B_{i}\right)\bmod M\right)=\sum_{i=1}^{N}\left(A _{i}+B_{i}\right)$
  2. $A_{i}+B_{i}\ge M$:

      令$\left(A_{i}+B_{i}\right)\bmod M=\left(A_{i}+B_{i}\right)-M$（题目限制$A_i$、$B_i$都小于M）
  3. 综上:

      $\sum_{i=1}^{N}\left(\left(A_{i}+B_{i}\right)\bmod M\right)=\sum_{i=1}^{N}\left(A _{i}+B_{i}\right)-CM$（C为第二类中AB和超过M的数量）

      > 将原方程的变量与不变量分离，将问题转化为寻找C的最大值。
      >