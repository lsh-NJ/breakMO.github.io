[[B - Informatics in MAC](https://codeforces.com/contest/1935/problem/B)](https://codeforces.com/contest/1935/problem/B)

# 思路：

- 要分为至少两段子段（只是将原数组分为了n个连续的段），要求每一段的MEX值相同，那么可以考虑分成两段（合并无论多少段MEX值相同的子段MEX不会发生改变，所以遵循**最简构造原则**）
- 这两个子段的构造可以通过前后缀MEX来实现，找到$\operatorname{\mathrm{MEX}}\left(1,i\right)=\operatorname{\mathrm{MEX}}\left(i+1 ,n\right)$，就可以分为这两段。

# 新知：

- 前后缀$\operatorname{\mathrm{MEX}}$

  ```cpp
  // 先获得MEX(1,n)，方便维护mex2
      int mex1 = 0, mex2 = 0;
      while(num2[mex2]) {
          mex2++;
      }

      // 同时获得获得前后缀MEX
      for(int i = 0; i < n; i++) {
          // 前缀增加元素，后缀减小元素
          num1[a[i]]++;
          num2[a[i]]--;
          // 检查后缀MEX
          if(num2[a[i]] == 0 && mex2 > a[i]) mex2 = a[i];
          // 检查前缀MEX
          while(num1[mex1]) mex1++;
          if(mex1 == mex2) {
              cout << 2 << endl;
              // 注意下标从0开始，i + 1是有效坐标
              cout << 1 << " " << i + 1 << endl;
              cout << i + 2 << " " << n << endl;
              return;
          }
      }
  ```

# 桎梏:

- 没有想到可以简化构造为两段