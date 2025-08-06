[[当我在构造的时候我会想什么](http://10.160.111.129/p/2684?tid=68920b24c9d615d80a10e864)](http://10.160.111.129/p/2684?tid=68920b24c9d615d80a10e864)

# 问题：

1. 使用优先队列的时间复杂度~~O(n)~~ 如何？

    优先队列的复杂度并非O(n),得到的数可以直接转字符串进行拼接
2. **如何高效在已知数组中查找一定位数的最大值**

    - 遵循高位数字越大越好的原理，可以通过大顶堆来实现。相比于普通的大顶堆，还需要考虑数字的位数，当满足删除数量时，就停止出栈操作。

```cpp
struct MyDeque {
    deque<int> dq;
    int m;

    void join(int x) {
        while(m > 0 && !dq.empty()/*防止back()是空*/ && dq.back() < x) {
            m--;
            dq.pop_back();
        }
        dq.push_back(x);
    }

    friend ostream& operator << (ostream& out, MyDeque& a) {
        // 删除多余位
        while(a.m > 0) {
            a.dq.pop_back();
            a.m--;
        }
        // 空则为0
        if(a.dq.empty()) {
            out << 0;
            return out;
        }
        while(!a.dq.empty()) {
            out << a.dq.front();
            a.dq.pop_front();
        }
        out << endl;
        return out;
    }
};
```