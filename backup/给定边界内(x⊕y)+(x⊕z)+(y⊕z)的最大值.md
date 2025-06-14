<html>
<body>
<!--StartFragment--><p id="20250614083727-ufbiwbf" updated="20250614083746"><a href="https://codeforces.com/contest/2057/problem/C">跳转题目</a></p>
<h2 id="思路-" updated="20250614083750">思路：</h2>
<ol id="20250614083751-2rkg9hg" updated="20250614083752">
<li id="20250614083752-mzh3glk" updated="20250614083752">
<h3 id="对于-x-y---x-z---y-z--要取得最大的结果-要求三个数的二进制表示尽可能有两个相同-即相同位置上两个1一个0或者两个0一个1-" updated="20250614090001">对于(x⊕y)+(x⊕z)+(y⊕z)，要取得最大的结果，要求三个数的二进制表示尽可能有两个相同，即相同位置上两个1一个0或者两个0一个1。</h3>
<p id="20250614092954-yli5ka5" updated="20250614092954">完全符合条件的值是<span data-type="inline-math" data-subtype="math" data-content="T=2\times\left(1+2+...+2^{k}\right)" contenteditable="false" class="render-node"></span>，对于本题而言k是l、r按位异或的最高位（这代表的是满足条件，即01分布规律的最大二进制位置，前面的01受到l、r的绝对限制，且也对结果没有任何影响）。</p>
<p id="20250614095435-q7rxm9v" updated="20250614095536">🔺<span data-type="strong u">按位异或的最高位获得的便捷方法</span>：<span data-type="code strong u">int k = 31 - __builtin_clz(l ^ r);</span>​</p>
<blockquote id="20250614095555-gcp1y8m" updated="20250614095556">
<p id="20250614095556-4htsrld" updated="20250614095708">​<span data-type="code strong u">__builtin_clz()</span>​用于计算整数的<span data-type="strong">前导零位数（Count Leading Zeros）</span></p>
</blockquote>
</li>
<li id="20250614084638-iwox636" updated="20250614084638">
<h3 id="我们要在l-r的区间中找到怎样的三个数-怎样符合这样的二进制分布规律-" updated="20250614085730">我们要在l、r的区间中找到怎样的三个数？怎样符合这样的二进制分布规律？</h3>
<p id="20250614092921-xn9z3nk" updated="20250614092921">仔细观察条件，其实可以只找到两个数，这两个数是l、r中相同位1、0差别最大的数。</p>
</li>
<li id="20250614085731-t8nsaw3" updated="20250614085731">
<p id="20250614085731-u9beylu" updated="20250614090521">由于已经了解，k的更高位对答案没有影响，且答案就是T，那么就直接开始构造这个k位的二进制数。</p>
</li>
<li id="20250614090526-b10y71p" updated="20250614090526">
<p id="20250614090526-k15fxff" updated="20250614090543">再引入一个概念：</p>

表示方式 | 能被  整除的数的特点
-- | --
十进制 | 末 k 位组成的数能被  整除
二进制 | 末尾有至少 k 个连续的 0
质因数分解 | 质因数中 2 的次数 ≥ k


<p id="20250614090642-b8tgv30" updated="20250614090856">看二进制部分，能被<span data-type="inline-math" data-subtype="math" data-content="2^{k}" contenteditable="false" class="render-node"></span>整除，那么减去1以后k位二进制都是不同的0和1，那么我们就可以找到l、r中最高位的k，以及一个<span data-type="inline-math" data-subtype="math" data-content="2^{k}" contenteditable="false" class="render-node"></span>的倍数，再-1就是另外一个结果，那么第三个结果就可以随便取得了</p>
</li>
<li id="20250614092524-ucr44z2" updated="20250614092524">
<h3 id="如何找到l-r之间能被整除的唯一数-" updated="20250614093400">如何找到l、r之间能被<span data-type="inline-math" data-subtype="math" data-content="2^{k}" contenteditable="false" class="render-node"></span>整除的唯一数？</h3>
<p id="20250614093017-cplgybc" updated="20250614095230">k被限制在l、r二进制按位异或的最高位（01不同的最高位），<span data-type="strong u">则这k 位可以是0开头后面全是1（将它与左边界进行按位或</span><span data-type="code u">|</span>​<span data-type="strong u">补全高位，这个数就是-1得到的另一个结果）</span>，显然右边界k位是1，那么这个数加一（第一个结果）也在右边界内，而且满足大于等于左边界。</p>
</li>
</ol>
<h2 id="代码-" updated="20250614090905">代码：</h2>
<pre><code class="language-cpp">#include&lt;bits/stdc++.h&gt;
using namespace std;
void work() {
    int l, r; cin &gt;&gt; l &gt;&gt; r;
    //k
    int k = 31 - __builtin_clz(l ^ r);
    //寻找l、r中的2的k次方
    int b = l | ((1 &lt;&lt; k) - 1), a = b + 1, c = (b == l ? r:l);
    cout &lt;&lt; a &lt;&lt; &quot; &quot; &lt;&lt; b &lt;&lt; &quot; &quot; &lt;&lt; c &lt;&lt;endl;

}
int main() {
    int t; cin &gt;&gt; t;
    while(t--) work();
    return 0;
}
</code></pre>
<p id="20250614090613-ke1rdp2" updated="20250614090613"></p>
<!--EndFragment-->
</body>
</html>