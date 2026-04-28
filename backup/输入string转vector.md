### C++中读取字符串为`vector<char>`的方法：

```cpp
string input;
getline(cin, input); // cin >> input
vector<char> charVector(input.begin(), input.end());
```