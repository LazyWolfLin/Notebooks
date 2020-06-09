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

所有多态基类（拥有任何 virtual 成员函数的基类）都需要一个 virtual 析构函数，否则 delete 一个指向派生类的基类指针将产生内存泄漏。

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

拷贝 RAII 对象必须考虑它所管理的资源的拷贝，常见的情况有：禁止拷贝 RAII 对象、禁止拷贝资源而对引用资源的 RAII 对象计数、禁止拷贝资源且转移资源的拥有权、拷贝 RAII 对象并拷贝资源。

### Provide access to raw resources in resource-managing classes

每个 RAII 类都会提供直接访问资源的方法，以满足某些 API 的需求。

### Use the same form in corresponding uses of new and delete

运算符 `new` 与运算符 `new []` 分配产生内存块上的内存布局并不一致。所以，使用运算符 `new []` 动态分配产生的对象数组内存块就必须使用运算符 `delete []` 释放。

### Store newed objects in smart pointers in standalone statements

资源创建与构造 RAII 对象需要在一条单独的语句中完成。否则由于编译器优化可能导致资源创建操作与使用资源构造 RAII 对象操作存在其他操作，一旦该操作产生异常很可能将导致难以察觉的资源泄漏。

## Designs and Declarations

所谓软件设计，是“令软件做出你希望它做的事情”的步骤和做法，通常以颇为一般性的构想开始，最终演变成十足的细节。

### Make interfaces easy to use correctly and hard to use incorrectly

接口应该清晰明了，能够帮助用户正确使用且防止用户错误使用。可以考虑的方法有：建立新类型，限制类型上的操作，与内置类型兼容，保证接口的一致性，限制对象值。

### Treat class design as type design

每次设计新的 class 或者新的 type 时需要先考虑以下问题：
* 如何构造和析构对象实例？
* 对象的初始化和对象的赋值有什么区别？
* 对象是否需要值传递，如何实现拷贝构造？
* 成员变量的合法值区间？
* 是否继承自其他 class 或 type，基类有哪些约束？
* 是否可以作为基类，是否需要虚析构函数？
* 需要哪些类型转换？
* 需要哪些运算符和成员函数？
* 哪些默认函数需要删除？
* 哪些成员变量会被哪个类调用？
* 异常安全吗？线程安全吗？
* 可以更一般化变成一个 class template 吗？
* 新类可以被 non-member 函数或者 templates 代替吗？

### Prefer pass-by-reference-to-const to pass-by-value

默认情况下，C++ 采用值传递，但是引用传递比值传递更为高效，而且可以避免对象切割问题（派生类对象通过值传递后被视为基类对象，切割了派生类成员）。

### Don't try to return a reference when you must return an object

必须返回对象时不要妄图返回其引用，否则可能返回一个空引用，也可能让等于运算恒成立。

### Declare data members private

将成员变量声明为 private，有利于数据访问的一致性和数据访问权限控制，并保证了成员变量的约束条件和封装性。而 protected 和 public 成员变量都不具有封装性。

### Prefer non-member non-friend functions to member functions

用 non-member 函数和 non-friend 函数代替 member 函数，可以增强类的封装性和可扩展性，减少编译依赖。

### Declare non-member functions when type conversions should apply to all parameters

如果某个函数的所有参数都需要支持类型转换，那么这个函数必定是一个 non-member 函数，只有 non-member 函数才能支持所有参数都进行隐式类型转换。

### Consider support for a non-throwing swap

C++ 不允许用户改变命名空间 std 内任何东西，除了特化 std 内的标准模板，比如 std::swap。

C++ 只允许对 class templates 进行偏特化，不允许对 function templates 进行偏特化。

如果特化的 std::swap 无法对成员变量进行操作，可以让类提供一个 public 成员函数 swap 来完成交换操作，并在特化的 std::swap 中调用它。

## Implementations

设计是优雅，实现则繁琐。

### Postpone variable definitions as long as possible

尽可能延后变量的定义，有利于代码的优雅和效率。

### Minimize casting

尽量避免转型操作。如果不能避免，那么将它们封装在函数中而非交由用户操作。同时尽量使用 C++ 风格的类型转换，因为它们更容易被发现。

### Avoid returning "handles" to object internals

返回指向对象内部的 handle 将有破坏对象封装、产生虚悬 handle 等风险。

### Strive for exception-safe code

异常安全函数意味着当异常抛出时不产生资源泄漏也不造成数据破坏。

异常安全函数有三个等级：
1. 基本（basic）异常保证：若函数抛出异常，则程序处于某个有效状态。不泄漏资源，也不会破坏对象和数据。
2. 强（strong）异常保证：若函数抛出异常，则程序状态不变，即会恰好地被回滚到该函数调用前的状态。虽然，强异常保证通常可以采用“copy and swap”的方法实现，但并非所有函数都具有实现的条件或者实现的意义。
3. 不抛出（nothrow）异常保证：函数绝不抛出异常。

### Understand the ins and outs of inlining

inline 函数能够节约函数调用的开销，但同时也可能导致代码膨胀、内存换页频繁以及 Cache 命中率低等问题。因此，慎重使用 inline 关键字，甚至将使用 inline 关键字的工作留到优化时。

### Minimize compilation dependencies between files

编译依赖是 C++ 编译时间的重要影响因素。编译器必须在编译期间知道对象大小，这导致 C++ 难以将类的声明和定义分离。为了使编译依赖最小化，需要在实现中让头文件尽量自我满足或者依赖于其他文件中的声明。可用的方法有：使用引用或指针代替对象、前置声明、声明与定义分离到不同的头文件。

## Inheritance and Object-Oriented Design

### Make sure public inheritance models "is-a"

public 继承意味着“is-a”的关系，即每一个派生类对象都是一个基类对象，所有适用于基类对象上的操作都应当适用于派生类对象。

### Avoid hiding inherited names

派生类的成员能够遮盖基类的成员，但这和继承关系相违背。

### Differentiate between inheritance of interface and inheritance of implementation

virtual 函数：
* 声明一个纯虚（pure virtual）函数是为了让派生类只继承函数的接口。
* 声明一个非纯虚（impure virtual）函数是为了让派生类继承函数的接口和默认实现。
* 声明一个非虚（non-virtual）函数是为了让派生类同时继承函数的接口和实现。

使用非纯虚（impure virtual）函数有忘记为新的派生类提供正确实现的风险，可以使用其他手法代替，比如使用纯虚函数强制派生类提供实现同时搭配一份默认实现或者一个非虚函数供派生类调用。

### Consider alternatives to virtual functions

virtual 函数的代替方案：
* 使用 Non-Virtual Interface 手法实现 Template Method 模式：使用一个 non-virtual 函数作为接口，并在它的实现中调用一个 private virtual 函数。
* 传统的 Strategy 模式：使用另一套类继承体系的 virtual 函数代替。
* 使用函数指针或者 std::function 完成 Strategy 模式

### Never redefine an inherited non-virtual function

绝对不要重定义继承来的 non-virtual 函数，否则派生类与基类将有不同的表现违背了继承关系。

### Never redefine a function's inherited default parameter value

绝对不要重定义继承来的默认参数值，否则派生类与基类将有不同的表现违背了继承关系。

### Model "has-a" or "is-implemented-in-terms-of" through composition

复合意味着“has-a”或者“is-implemented-in-terms-of”的关系。

### Use private inheritance judiciously

private 继承规则：
1. 编译器不会做派生类到基类的隐式转换。
2. 基类所有成员在派生类中都是 private 成员。

private 继承意味着“implemented-in-terms-of”的关系，即派生类根据基类对象进行实现，基类成员只是是派生类实现上的细节。private 继承仅是一种实现技术，其意义只在于实现层面，而无其他设计层面上的意义。

### Use multiple inheritance judiciously

多重继承是非常具有争议的问题。它带来复杂性、性能开销甚至还可能产生歧义，但它也有适用的情况。当需要 public 继承一个接口类同时 private 继承一个辅助类的情况下适合使用多重继承。

virtual 继承能够解决钻石型多重继承带来的重复基类变量问题，但需要付出性能代价，甚至可能导致初始化异常问题。

## Templates and Generic Programming

### Understand implicit interfaces and compile-time polymorphism

class 和 template 都支持接口（interfaces）和多态（polymorphism）。但 class 支持显式接口和运行期多态，而 template 支持隐式接口和编译期多态。

显式接口由函数签名构成，在 class 的声明中明确可见。隐式接口由有效表达式确定，由使用 template 的 class 提供具体实现。

运行期多态指在运行期时根据对象的动态类型决定具体的被调函数。编译期多态指在编译期时根据 template 参数实例化出不同的被调函数。

### Understand the two meanings of typename

当你想在 template 中使用一个嵌套从属类型名称时，需要在它前面使用关键字 typename，用以消除歧义表明该名称是类型名而非成员变量名。但 typename 不能出现在 base class list（基类列表）和 member initialization list（成员初始化列表）中。

### Know how to access names in templatized base classes

由于全特化的模板基类可能不提供模板基类全部的隐式接口，因此编译器无法在模板派生类中直接继承模板基类的隐式接口。为了在模板派生类中使用模板基类的隐式接口，需要使用 `this->method()` 再次隐式声明接口，或者使用 `using BaseClass::method()` 显式声明基类接口。

### Factor parameter-independent code out of templates

任何 templates 代码都不应当依赖于能够造成代码膨胀的 template 参数。

非类型 template 参数造成的代码膨胀通常可以消除，做法是以函数参数或类成员变量代替 template 参数。类型 template 参数造成的代码膨胀通常可以降低，做法是让具有完全相同二进制表示的具体类型共用具体实现代码。

### Use member function templates to accept "all compatible types"

当成员函数需要接受所有兼容类型的参数时，可以使用成员函数模板（member function templates）。

当使用成员函数模板声明了泛化的拷贝构造函数和泛化的赋值运算后，仍可以声明正常的拷贝构造函数和赋值运算符。

### Define non-member functions inside templates when type conversions are desired

在 temlates 的类型推导时，编译器不会考虑隐式类型转换。

当 non-member function templates 需要支持隐式类型转换时，可将其声明为相关 class templates 的 friend non-member function templates，以保证编译器在特化 class templates 时特化相关的 friend non-member function templates。

### Use traits classes for information about types

C++ STL 中有五种 Iterator：Input Iterator、Output Iterator、Forward Iterator、Bidirectional Iterator、Random Access Iterator。

Traits 并不是 C++ 的关键字也不是预先定义好的组件，而是一种技术，也是 C++ 程序员之间的协议。Traits 通过一个 template struct 和一组特化版本使得编译器在编译期获得类型相关信息。

### Be aware of template metaprogramming

template metaprogramming 有诸多好处：编译期类型检查、性能优化。

## Customizing new and delete

### Understand the behavior of the new-handler

在内存分配失败之后 `operator new` 抛出异常之前，`operator new` 会先调用一个客户指定的错误处理函数，一个所谓的 `new-handler`。

惯用法 CRTP（curiously recurring template pattern）：类型 T 继承自一个 templatized base class，而后者又以类型 T 作为模板类型参数，即：`Class T: public TemplatizedBaseClass<T>;`。

### Understand when it makes sense to replace new and delete

有些时候可能需要自定义运算符 `new` 和 `delete`，比如，检查错误时、收集数据时、优化性能时、聚集重要数据时。

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

## Deducing Types

### Understand template type deduction.

对于函数模板：

``` C++
template<typename T>
void f(ParamType param);

f(expr);
```

在编译期时，编译器会根据 `expr` 推导出两个类型：`T` 和 `ParamType`。由于 `ParamType` 可能包含一些类型限定符，所以两个类型往往不一致。类型推导时，首先根据 `expr` 推导出 `ParamType`，再由 `ParamType` 推导出 `T`。根据 `ParamType` 形式的不同可分为三种情况：

* `ParamType` 是指针或引用，但不是 Universal Reference
* `ParamType` 是 Universal Reference
* `ParamType` 不是指针也不是引用

### Understand auto type deduction.

通常情况下，`auto` 采用与模板相同的类型推导规则，除了 `auto` 类型推导时会假定初始化表达式 `{ value, ... }` 代表 `std::initializer_list`，而模板类型推导将失败。

### Understand decltype.

通常情况下，`decltype` 会得到变量或者表达式的类型而不作任何修改。

`decltype(auto)` 意味着像 `auto` 一样从初始化表达式出发来推导类型但采用 `decltype` 规则。

### Know how to view deduced types.

## auto

### Prefer auto to explicit type declarations.

使用 `auto` 的好处：
* 避免变量未初始化风险
* 无需人肉推导复杂冗长类型
* 可以使用闭包类型声明变量
* 代码可维护性更高

### Use the explicitly typed initializer idiom when auto deduces undesired types.

C++ 的隐式代理类，比如 `std::vector<bool>::reference`，会导致 `auto` 推导出不正确的类型，此时需要使用带显式类型转换的初始值帮助 `auto` 推导出正确的类型。

## Moving to Modern C++

### Distinguish between () and {} when creating objects.

### Prefer nullptr to 0 and NULL.

字面常量 0 和 NULL 在 C++ 中都不是指针类型，只是当 C++ 在只能使用指针的语境中发现它们才勉强将它们解释为指针。因此在指针类型和整型之间重载是一件有危险的事，毕竟总会有蠢货固执的使用 0 和 NULL 代替 `nullptr`。

### Prefer alias declarations to typedefs.

类型别名相比于 `typedef` 的好处不只在于更易阅读的函数指针类型，更在于别名模板。

### Prefer scoped enums to unscoped enuns.

在大括号中声明的名称，它的可见性被限定在括号的作用域内，但 C++98 风格的枚举类型是个例外。这种枚举量名称泄露到作用域外的枚举类型称为不限范围的枚举类型（Unscoped enumeration），C++11 中新增了限定作用域的枚举类型（Scoped enumerations）。限定作用域的枚举类型不仅能够降低名称空间污染，还能避免枚举量隐式转换到整型甚至浮点型。

### Prefer deleted functions to private undefined ones.
### Declare overriding functions overri.de.
### Prefer const_iterators to iterators.
### Declare functions noexcept ifthey won't emit exceptions.
### Use constexpr whenever possible.
### Make const member functions thread safe.
### Understand special member function generation.

## Smart Pointers
### Use std::unique_ptr for exclusive-ownership resource management.
### Use std::shared_ptr for shared-ownership resource management.
### Use std::weak_ptr for std::shared_ptr-like pointers that can dangle.
### Prefer std::make_unique and std::make_shared to direct use of new.
### When using the Pimpl Idiom, define special member functions in the implementation file.

## Rvalue References, Move Semantics, and Perfect Forwarding
### Understand std::move and std::forward.
### Distinguish universal references from rvalue references.
### Use std::move on rvalue references, std::forward on universal references.
### Avoid overloading on universal references.
### Familiarize yourself with alternatives to overloading on universal references.
### Understand reference collapsing.
### Assume that move operations are not present, not cheap, and not used.
### Familiarize yourself with perfect forwarding failure cases.

## Lambda Expressions
### Avoid default capture modes.
### Use init capture to move objects into closures.
### Use decltype on auto&& parameters to std::forward them.
### Prefer lambdas to std::bind.

## The Concurrency API
### Prefer task-based programming to thread-based.
### Specify std::launch::async ifasynchronicityis essential.
### Make std::threads unjoinable on all paths.
### Be aware of varying thread handle destructor behavior.
### Consider voi_d futures for one-shot event communication.
### Use std::atoni.c for concurrency, volatile for special memory.

## Tweaks
### Consider pass by value for copyable parameters that are cheap to move and always copied.
### Consider emplacement instead of insertion.
