1. #### 基本结构：

    `[capture](parameters) -> return_type { body }`

    * **`[capture]`** ：捕获列表，用于指定如何捕获外部变量（值捕获、引用捕获等）。

      捕获列表决定了 Lambda 如何访问外部作用域中的变量：

      * **值捕获**（`[var]`）：按值捕获变量 `var` 的副本。
      * **引用捕获**（`[&var]`）：按引用捕获变量 `var`。
      * **隐式捕获**：

        * `[=]`：按值捕获所有外部变量。
        * `[&]`：按引用捕获所有外部变量。
      * **混合捕获**：例如 `[&, a]`（按引用捕获所有变量，但 `a` 按值捕获）或 `[=, &b]`（按值捕获所有变量，但 `b` 按引用捕获）。
    *  **`(parameters)`** ：参数列表，类似于普通函数的参数。
    *  **`-> return_type`**：返回类型（可选），可省略并由编译器自动推导。
    *  **`{ body }`** ：函数体，包含具体的实现代码。
2. #### **Lambda 的本质**

    Lambda 表达式会被编译器转换为一个匿名的函数对象（即仿函数）。例如：

    ```cpp
    auto lambda = [](int x) { return x * 2; };
    // 等价于（简化版）：
    struct UnnamedFunctor {
        int operator()(int x) const { return x * 2; }
    };
    auto lambda = UnnamedFunctor{};
    ```
3. #### 经典使用场景：**自定义排序规则**

    ```cpp
    std::sort(nums.begin(), nums.end(),
              [](int a, int b) { return a > b; });  // 降序排序
    ```