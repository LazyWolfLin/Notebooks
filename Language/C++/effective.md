# Effective C++

## Accustoming Yourself to C++

### View C++ as a federation of languages

C++ 是一种多范式编程语言（multiparadigm programming language），它支持过程（procedural）、面向对象（object-oriented）、函数（functional）、泛型（generic）和元编程（metaprogramming）。多编程范式分别组成了 C++ 不同的部分：

* C
* Object-Oriented C++
* Template C++
* STL

C++ 编程守则视情况而变，取决于你使用哪一部分的 C++。

### Perfer consts, enums, and inlines to #defines

使用宏意味着你与编译器看到的不是同样的代码，编译器在处理代码前宏就已经被预处理器移除了。同时，因为宏不在编译器生成的符号表中，那么当编译失败时，你在错误信息中也看不到宏。而且，宏是全局的，也就意味着某个犄角旮旯里可能藏着一个你不知道的宏。虽然 `C++` 中不可避免的需要使用某些宏，但优先使用 `const` 常量、`enum` 枚举常量和 `inline` 内联函数而非 `#define` 宏有助于避免上述情况。

### Use const whenever possible

`const` 意味着一种语义上的约束，虽然编译器很难区别真正的常量与只读别名并据此作出优化，但却能在编译期强制实施 `const` 约束。所以，尽量使用 `const`，让编译器在语义上检查你的代码。

`const` 出现在 `*` 左边意味着指针指向常量或只读别名，`const` 出现在 `*` 右边意味着指针本身是常量或只读别名，`const` 出现在 `*` 两边则指针本身及被指物两者都是常量或只读别名。

#### `const` 成员函数

关于 `const` 成员函数的语义有两个主流概念：
* "bitwise const": `const` 成员函数不能改变对象的任何成员变量。
* "logical const": `const` 成员函数可以进行一些对象外部无法发现的修改。

当 `const` 成员函数与 non-`const` 成员函数有等价实现时，让 non-`const` 成员函数调用 `const` 成员函数以避免重复实现。

### Make sure that objects are initialized before they're used