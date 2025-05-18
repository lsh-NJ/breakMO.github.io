## 题目大意概述：

> 给定一个未知数`x(0<=x<=1e9)`， 本题作为一道交互题有如下的交互过程：
>
> - "add " Add some integer  `y` to .The jury will output "1" if  is within `[1, 1e18]` (successful), and "0" otherwise. If successful, update `x = x + y`
> - "mul " Multiply  by a positive integer  `y`.The jury will output "1" if  is within `[1, 1e18]` (successful), and "0" otherwise. If successful, update `x = x * y`
> - "div " Divide  by a positive integer  `y`.The jury will output "1" if  is a divisor of `[1, 1e18]` (successful), and "0" otherwise. If successful, update `x = x / y`
> - "digit" Make  equal to the sum of its digits.The jury will always output "1" and update `x = S(x)`（x的每一位数字之和：如S（123）= 1 + 2 + 3 = 6。
>
> 最后输入命令`!`告诉系统自己已经处理

## 思路:

1. ### 七步法初见杀：（已经坠机了）

    - 未知数不知道，但是可以通过命令使其在七步中变成固定的一个已知数
    - 通过两次`digit`命令使范围从`0<=x<=1e9`缩减到`[1,16]`
    - `add`命令可以看出可以对当前的范围进行缩减，一次减一半，如`add -8`就把范围缩减到了`[1,8]`，依次正好6步把`x`固定为`1`
    - 最后输入命令`add n - 1`然后`!`结束交互。
2. ### 四步法梅开二度：（仙术只需要最朴素的手法）

    - 依然是让未知数变成一个已知的确定的数
    - 这次是通过`mul`后`digit`来进行归并：

      > 定理：一个数的数位之和能被9整除是这个数能被9整除
      >
      > 逆定理：一个数乘以9，得到的数的数位之和能被9整除
      >

      而且这个乘以9然后进行数位和的结果在进行数位和一定等于9，这就构成了唯一确定的数

3. ### 最终展示神力：

    `S[(1ed−1)x]=9d ∀x∈[1,1ed]`