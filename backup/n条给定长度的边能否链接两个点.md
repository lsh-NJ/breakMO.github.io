# [[ B - Line Segments](https://codeforces.com/contest/2119/problem/B)](https://codeforces.com/contest/2119/problem/B)

# 关键：

将问题转化为n + 1条边是否能组成多边形或退化多边形的问题（拿三角形分析最简单）

并且并不需要拿出具体的方案，只需要判断存在性，这n+1条边中的最大值只要不大于其余所有边的和就一定能组成多边形或退化多边形。