## 步骤:

1. 将给定的k进制字符串转换为10进制字符串

    ```cpp
    big_int res;
        for(int i = 0; i < len; i++) {
            res *= k;
            if(s[i] <= '9') res += s[i] - '0';
            else if(s[i] >= 'A') res += s[i] - 'A' + 10;
        }
    ```
2. 期间需要对结构体进行操作符重载
3. 最后通过余

```cpp
#include<bits/stdc++.h>
using namespace std;
constexpr int N = 4000 + 10;
struct big_int
{
    int a[N], n /*动态记录最高位,实际会比最高位多一位*/;
    big_int() {
        memset(a, 0, sizeof(a));
        n = 0;
    }

    big_int& operator += (int x) {
        a[0] += x;
        for(int i = 0; i <= n; i++) {
            // 动态拓展最高位
            if(i == n && a[i] > 0) n++;
            a[i + 1] += a[i] / 10;
            a[i] %= 10;
        }
        return *this;
    }

    big_int& operator *= (int x) {
        for(int i = 0; i <= n; i++) 
            a[i] *= x;
        for(int i = 0; i <= n; i++) {
            if(i == n && a[i] > 0) n++;
            a[i + 1] += a[i] / 10;
            a[i] %= 10;
        }
        return *this;
    }

    big_int& operator /= (int x) {
        int tmp = 0;
        for(int i = n - 1; i >= 0; i--) {
            tmp = tmp * 10 + a[i];
            a[i] = tmp / x;
            tmp %= x;
        }
        while(n > 0 && a[n - 1] == 0) n--;
        return *this;
    }

    int operator % (int x) {
        int res = 0;
        for(int i = n - 1; i >= 0; i--) {
            res = (res * 10 + a[i]) %  x;

        }
        return res;
    }

    string to_k (int k) const {
        if(n == 0) cout << 0 << endl;
        constexpr char digits[] = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        big_int tmp = *this;
        string s;
        while(tmp.n > 0) {
            s += digits[tmp % k];
            tmp /= k;
        }
        reverse(s.begin(), s.end());
        return s;
    }
};

int main() {
    int k, t; string s; cin >> k >> s >> t;
    int len = s.size();
    big_int res;
    for(int i = 0; i < len; i++) {
        res *= k;
        if(s[i] <= '9') res += s[i] - '0';
        else if(s[i] >= 'A') res += s[i] - 'A' + 10;
    }

    cout << res.to_k(t) << endl;
}
```