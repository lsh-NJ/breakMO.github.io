# **[[A](http://10.160.111.129/p/2657?tid=687f5437c9d615d80a0f28ce)](http://10.160.111.129/p/2657?tid=687f5437c9d615d80a0f28ce)**[ [ pair pair int int pair int int](http://10.160.111.129/p/2657?tid=687f5437c9d615d80a0f28ce)](http://10.160.111.129/p/2657?tid=687f5437c9d615d80a0f28ce)

## 思路：

- 使用递归来进行“一对二”的操作，如果输入pair那么一定要有后续两个部分，没有后续两个部分就错误终止，如果所有的pair都已经有匹配项依然还有输入也要错误终止，其他就是正常输出结果就可以了。
- 输入流手动终止使用`Ctrl + Z`

```cpp
#include<bits/stdc++.h>
using namespace std;
vector<string> res;
void rec() {
    string s;
    if(cin >> s) {
        if(s == "pair") {
            res.push_back("pair<");
            rec();
            res.push_back(",");
            rec();
            res.push_back(">");
        }
        else {
            res.push_back("int");
        }
    }
// 缺少匹配项
    else {
        cout << "Syntax Error" << endl;
        exit(0);
    }
}

int main() {
    rec();
    string s;
// 多余匹配项
    if(cin >> s) {
        cout << "Syntax Error" << endl;
        exit(0);
    }
    for(size_t i = 0; i < res.size(); i++) {
        cout << res[i];
    }
    cout << endl;
}
```