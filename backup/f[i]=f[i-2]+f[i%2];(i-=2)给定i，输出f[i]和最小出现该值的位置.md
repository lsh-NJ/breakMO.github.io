<html>
<body>
<!--StartFragment--><h1 id="小q的数列" updated="20250714164549"><a href="https://ac.nowcoder.com/acm/problem/15979">小q的数列</a></h1>
<h4 id="思路-" updated="20250714180138">思路：</h4>
<ul id="20250714180141-jue799l" updated="20250714180142">
<li id="20250714180142-9niq7j4" updated="20250714180142">
<p id="20250714180142-hg2k2qr" updated="20250714180210">发现f(n)值只与二进制的1的个数有关：</p>
<pre><code class="language-cpp">while(n &gt; 0) {
    n -= (n &amp; -n);
    res++;
}
</code></pre>
</li>
<li id="20250714180714-757cpnu" updated="20250714180714">
<p id="20250714180714-lsct8aj" updated="20250714181002">位置肯定是由res推出的，发现:<span data-type="code">n = (1ll &lt;&lt; res) - 1;</span>​</p>

res | n
-- | --
0 | 0
1 | 1
2 | 3
3 | 7
4 | 15


</li>
</ul>
<p id="20250714164550-mk6nxvw" updated="20250714164550"></p>
<!--EndFragment-->
</body>
