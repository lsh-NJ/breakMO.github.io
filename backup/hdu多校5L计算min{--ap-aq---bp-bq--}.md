# L 最小值

- ## 思路：

  - 化简式子发现：

    1. 当$\left(a_{p}-a_{q}\right)\left(b_{p}-b_{q}\right)\ge0$时，原式等于$\left\vert\left(a_{p}-a_{q}\right)-\left(b_{p}-b_{q}\right)\right\vert$
    2. 反之，原式等于$\left\vert\left(a_{p}+a_{q}\right)-\left(b_{p}+b_{q}\right)\right\vert$
  - 为什么我们只需对原式的转换进行讨论就可以了?

    经过检查发现，当$\left(a_{p}-a_{q}\right)\left(b_{p}-b_{q}\right)\ge0$时，$\left\vert\left(a_{p}-a_{q}\right)-\left(b_{p}-bq\right)\right\vert$$<$$\left\vert\left(a_{p}+a_{q}\right)-\left(b_{p}+b_{q}\right)\right\vert$，也就是说当我们检查两种情况的最小值时，不合理的可能性恰好不可能是答案。

    反之亦然。