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

对于内置对象，在使用之前手工初始化它，因为 C++ 并保证进行初始化。而其他对象则由构造函数负责初始化，构造函数需要保证对象的每一个成员的初始化工作。

在构造函数中使用成员初值列表（member initialization list）初始化成员优于在构造函数中使用赋值操作。

C++ 有固定的成员初始化序列：基类初始化早于派生类，成员变量则总是以声明次序进行初始化。

C++ 不保证跨编译单元对象（non-local static object）的初始化次序，但保证 local static object 在被调用前初始化。使用 reference-returning 函数可以将 non-local static object 转化为 local static object，函数的首次调用时会初始化该对象。

## Constructors, Destructors, and Assignment Operators

### Know what functions C++ silently writes and calls

C++ 可以暗自创建：默认构造函数、复制构造函数、移动构造函数、复制赋值运算符、移动赋值运算符、默认析构函数。

### Explicitly disallow the use of compiler-generated functions you do not want

如果要阻止 C++ 自动创建成员函数，则应在成员函数定义中使用 `delete` 关键字显式弃置它。

### Declare destructors virtual in polymorohic base classes
### Prevent exceptions from leaving destructors
### Never call virtual functions during construction or destruction
### Have assignment operators return a reference to *this
### Handle assignment to self in operator=
### Copy all parts of an object
## Resource Management
## Designs and Declarations
## Implementations
## Inheritance and Object-Oriented Design
## Templates and Generic Programming
## Customizing new and delete
## Miscellany