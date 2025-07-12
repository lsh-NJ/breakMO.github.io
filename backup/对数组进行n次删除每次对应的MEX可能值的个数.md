# [[ E - MEX Count](https://codeforces.com/contest/2123/problem/E)](https://codeforces.com/contest/2123/problem/E)

- #### 思路一:

  1. MEX是连续的从零开始的数的第一个未出现的数，则要得到相应k下的MEX可能值需要一个连续的数组。0，1，2，3......i -1,......总长度为n-k，令MEX为i，共有i个从零开始的连续的数。
  2. 这里的i一定小于等于n-k，这是总长度所决定的。
  3. 这里的i一定小于等于最初的MEX，因为最初的MEX已经确定了最大的从零开始的连续序列。
  4. 以上内容还没有考虑剩余n-k-i个数。这些数中不应该出现i，因为我们想要得到这个数列的MEX为i，（探索n-k长度的数组所有MEX的可能值），那么删去的k个元素必须把所有i元素全部包含进去，就需要满足i的频率小于等于k。
  5. 因此我们得到了三个最基本的关系式。我们可以维护一个k的MEX可能值的集合，并且发现某一个k值的集合可以由上一个集合推出，意味着并不需要对每个k进行独立的分析，可以减少复杂度。

      k从零开始，集合中只存在最初的MEX。当k+1以后，MEX可能会因为长度不够而变成不可能，因此需要对集合中的n-k-1进行移除（管它有没有都直接扬了），这是思路2.中条件的启示。除了移除可能值，还要考虑可能值的增加，随着k的增大，可能会有更多的元素变成了可移除，也就是当其频率等于k以后就有了被取到的可能（为什么不考虑小于k的呢？显然k是每次加一，小于k的频率对应的数都在之前有过了判定），这时还要注意他要满足其他条件，i一定要小于最初的MEX，并且要小于n-k。也就是`i <= min(MEX, n-k);`
- #### 代码实现中的操作:

  1. 求MEX：（序列中第一个没有被排除的元素，排除所有序列中存在的元素，利用了set的插入排序）

      ```cpp
      for(int i = 0; i <= n; i++) excl.insert(i);

      for(int i = 0; i < n; i++) {
              cin >> a[i];
              excl.erase(a[i]);
          }
      int MEX = *excl.begin();
      ```
  2. map反转：（正向创建map，反转以后根据键值查找键）

      ```cpp
      unordered_map<int, int> freq;
      。。。。。。
      unordered_map<int, vector<int>> invfreq;
      for(pair<int, int> part:freq) {
          invfreq[part.second].push_back(part.first);
      }
      ```


- #### 思路二：

  - 思路一是从k的依次取值入手的，我们还可以尝试从MEX的取值入手，因为我们发现每一个可能的MEX值对应的k值是一个区间，对于这样的区间我们可以尝试使用差分数组来降低复杂度（不用差分数组就超时了）
  - 对于我们的MEX值对象，肯定是要小于等于k=0时的MEX的，这是基础连续性所规定的。
  - 要想取到一个MEX值，使一个MEX值成为可能，首先就是k的值要大于等于这个目标数的频率。这就是“下界”。接下来我们来寻找上界：

    对于k次操作以后的数组，长度为n-k，刨除所有重复的数（这样k更大），剩下连续的从0~MEX-1的序列。则`MEX <= n-k`即`k<=n-MEX`；
  - res数组存储每一个k对应的可能的MEX值的数量。那么`res[0] = 1, diff[0] = res[0] = 1;`
  - 边界也已经知晓，`diff[l]++`,`diff[r + 1]++`就是对差分数组的维护了。之后`res[i] = res[i - 1] + diff[i]`就是最终的结果了

- #### 代码:

  ```cpp
  vector<int> a(n), res(n + 1), diff(n + 2);
      map<int, int> freq;
      for(int i = 0; i < n; i++) {
          cin >> a[i];
          freq[a[i]]++;
      }
      //遍历可能的MEX值
      for(int i = 0; i <= n; i++) {
          diff[freq[i]]++;
          diff[n - i + 1]--;
          if(!freq[i]) break;//使得i不可能突破不连续的限制，即i<=MEX
      }

      for(int i = 0; i <= n; i++) {
          if(i == 0) {
              res[0] = diff[0];
              cout << diff[0] << " ";
          }
          else {
              res[i] = diff[i] + res[i - 1];
              cout << res[i] << " \n"[i == n];
          }
      }
  ```