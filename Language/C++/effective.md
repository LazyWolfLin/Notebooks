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

任何拥有 virtual 成员函数的基类都需要一个 virtual 析构函数，否则 delete 一个指向派生类的基类指针将产生内存泄漏。

一般而言，每一个带有 virtual 成员函数的类都有一个 vptr(virtual table pointer) 指向一个函数指针数组 vtbl(virtual table)，用于运行时获得正确的函数指针。

### Prevent exceptions from leaving destructors

如果在析构函数中抛出异常，那么程序将可能提前结束或出现不明确行为。所以，析构函数绝对不能抛出异常，如果析构函数中被调函数抛出异常，那析构函数就应该捕捉并处理。

如果用户需要对某一操作可能抛出的异常做处理，那么就应当提供一个普通函数执行该操作。

### Never call virtual functions during construction or destruction

不要在构造和析构函数中调用虚函数，因为无法调用到派生类版本的虚函数。

### Have assignment operators return a reference to *this

赋值运算符需要返回一个指向 `*this` 的引用，这是一个惯例。

### Handle assignment to self in operator=

赋值运算符应当保证自我赋值操作的安全性，可用方法包括“证同测试”和“copy and swap”。

### Copy all parts of an object

编译器不会注意到自定义的拷贝操作没有完全拷贝每个成员变量，需要用户自行保证。所以添加新成员变量或者新派生类时，需要检查拷贝操作是否对新成员变量进行拷贝或者调用了基类的拷贝操作。

拷贝构造和赋值操作往往有相似的代码，但它们不能相互调用，只能将相同代码打包到第三个函数中共同调用。

## Resource Management

资源就是使用后必须释放的东西。C++ 常见的资源如：动态分配的内存、文件描述器、互斥锁、图形界面中的字体和笔刷、数据库的连接和网络 sockets。

### use objects to manage resources

为防止资源泄漏，可以使用 RAII(Resource Acquisition Is Initialization)对象，它们在构造时获取资源并在析构时释放资源。常见的 RAII 对象有 std::unique_ptr、std::shared_ptr 和 std::weak_ptr。

### Think carefully about copying behavior in resource-managing classes
### Provide access to raw resources in resource-managing classes
### Use the same form in corresponding uses of new and delete
### Store newed objects in smart pointers in standalone statements

## Designs and Declarations

### Make interfaces easy to use correctly and hard to use incorrectly
### Treat class design as type design
### Prefer pass-by-reference-to-const to pass-by-value
### Don't try to return a reference when you must return an object
### Declare data members private
### Prefer non-member non-friend functions to member functions
### Declare non-member functions when type conversions should apply to all parameters
### Consider support for a non-throwing swap

## Implementations

### Postpone variable definitions as long as possible
### Minimize casting
### Avoid returning "handles" to object internals
### Strive for exception-safe code
### Understand the ins and outs of inlining
### Minimize compilation dependencies between files

## Inheritance and Object-Oriented Design

### Make sure public inheritance models "is-a"
### Avoid hiding inherited names
### Differentiate between inheritance of interface and inheritance of implementation
### Consider alternatives to virtual functions
### Never redefine an inherited non-virtual function
### Never redefine a function's inherited default parameter value
### Model "has-a" or "is-implemented-in-terms-of" through composition
### Use private inheritance judiciously
### Use multiple inheritance judiciously

## Templates and Generic Programming

### Understand implicit interfaces and compile-time polymorphism
### Understand the two meanings of typename
### Know how to access names in templatized base classes
### Factor parameter-independent code out of templates
### Use member function templates to accept "all compatible types"
### Define non-member functions inside templates when type conversions are desired
### Use traits classes for information about types
### Be aware of template metaprogramming

## Customizing new and delete

### Understand the behavior of the new-handler
### Understand when it makes sense to replace new and delete
### Adhere to convention when writing new and delete
### Write placement delete if you write placement new

## Miscellany

### Pay attention to compiler warnings
### Familiarize yourself with the standard library, including TR1
### Familiarize yourself with Boost

## Basics

### Distinguish between pointers and references
### Prefer C++ style casts
### Never treat arrays polymorphically
### Avoid gratuitous default constructors

## Operators

### Be wary of user-defined conversion functions
### Distinguish between prefix and postfix forms of increment and decrement operators
### Never overload `&&`, `||`, or `,`
### Understand the different meanings of new and delet

## Exceptions

### Use destructors to prevent resource leaks
### Prevent resource leaks in constructors
### Prevent exceptions from leaving destructors
### Understand how throwing an exception differs from passing a parameter or calling a virtual function
### Catch exceptions by reference
### Use exception specifications judiciously
### Understand the costs of exception handling

## Efficiency

### Remember the 80-20 rule
### Consider using lazy evaluation
### Amortize the cost of expected computations
### Understand the origin of temporary objects
### Facilitate the return value optimization
### Overload to avoid implicit type conversions
### Consider using op= instead of stand-alone op
### Consider alternative libraries
### Understand the costs of virtual functions, multiple inheritance,virtual base classes, and RTTI

## Techniques, Idioms, Patterns

### Virtualizing constructors and non-member functions
### Limiting the number of objects of a class
### Requiring or prohibiting heap-based objects
### Making functions virtual with respect to more than one object

## Miscellany

### Program in the future tense
### Make non-leaf classes abstract
### Understand how to combine C++ and C in the same program
### Familiarize yourself with the language standard