## 思路：

- 数学推导：$\operatorname{\mathrm{gcd}}\left(a^{b},c^{d}\right)=\operatorname{\mathrm{gcd}}\left (x^{b}\operatorname{\mathrm{gcd}}\left(a,c\right)^{b},y^{d}\operatorname{\mathrm{gcd}} \left(a,c\right)^{d}\right)=\operatorname{\mathrm{gcd}}\left(a,c\right)\cdot\operatorname{\mathrm{gcd}} \left(x^{b},y^{d}\operatorname{\mathrm{gcd}}\left(a,c\right)^{b-d}\right)$

  其中$\operatorname{\mathrm{gcd}}\left(x,y\right)=1$（两个数的最大公因数是所有相同的质因数的最小质数部分，则刨除这一部分的剩余部分一定没有公共质因数）

  通过递归的过程逐渐减少d、b-d的大小，或者当a、b互质时后面部分都是1。

```cpp
#define ll  long long
const ll m = 998244353;
ll fast_pow(ll a, ll b) {
	a %= m;
	ll res = 1;
	while(b) {
		if(b & 1) res = res * a % m;
		a = a * a % m;
		b >>= 1;
	}
	return res;
}

ll work(ll a, ll b, ll c, ll d) {
	ll x = gcd(a, c);
	if(x == 1 || b == 0 || d == 0) return 1;
	if(b > d) swap(a, c), swap(b, d);
	return fast_pow(x, b) * work(a / x, b, x, d - b) % m;
}

signed main() {
	int t; cin >> t;
	while(t--) {
		ll a, b, c, d; cin >> a >> b >> c >> d;
		cout << work(a, b, c, d) << endl;
	}
}
```