# Pthon

## 注释

### 行注释

Python使用`#`号标识注释，`#`号右侧的任意内容均视为注释。

### DocStrings

## 标识符

Python标识符命名规则：
1. 变量名由字母、数字或下划线组成，以字母或下划线为开头。
2. 变量名不能与关键字或函数名相同。
3. 变量名大小写敏感。

## 变量

Python中的变量无需定义数据类型。

## 运算符

|运算符|作用|
|---|---|
|+|加|
|-|减|
|*|乘|
|**|乘方|
|/|除|
|//|整除|
|%|取模|
|<<|左移|
|>>|右移|
|&|按位与|
|\||按位或|
|^|按位异或|
|~|按位取反|
|<|小于|
|>|大于|
|<=|小于等于|
|>=|大于等于|
|==|等于|
|!=|不等于|
|not|非|
|and|与|
|or|或|

## 字符串

字符串的表示方法：
1. 使用单引号标识。如：`'string'`
2. 使用双引号标识。如：`"string"`
3. 使用三个引号标识多行字符串：如：`'''string'''`或者`"""string"""`

字符串的方法
|方法|功能|
|---|---|
|title|以标题的格式显示每个单词，即首字母大写显示每个单词|
|upper|全部大写显示每个字母|
|lower|全部小写显示每个字母|
|lstrip|删除字符串左端空白|
|rstrip|删除字符串右端空白|
|strip|删除字符串两端空白|
|replace|使用指定字符替换字符串中指定字符|
|format|字符串格式化|

运算符
|运算符|功能|
|---|---|
|+|连接两个字符串|
|[ ]|字符串索引|

## 列表

列表（`list`）由一系列有序元素组成。

Python使用方括号（`[]`）来表示列表，用逗号（`,`）分隔列表中的元素。

列表的方法
|方法|功能|
|---|---|
|append|在列表末尾添加新元素|
|insert|在列表中指定位置插入指定元素|
|pop|删除列表中指定位置上的元素，默认删除列表末尾元素|
|remove|根据元素值删除列表中指定元素|
|sort|对列表中元素进行排序|
|sorted|显示列表中元素排序结果|
|reverse|对列表中元素进行反转|
|len|显示列表长度|

运算符
|运算符|功能|
|---|---|
|[ ]|列表元素索引|
|del|删除列表中指定位置上的元素|

## 元组

元组(`tuple`)由多个不可更改的无序元素组成。

Python使用方括号（`()`）来表示元组，用逗号（`,`）分隔元组中的元素。

## 字典

字典(`dict`)由多个无序的键值对组成。

Python使用花括号（`{}`）来表示字典，用（`:`）组成键值对，用逗号（`,`）分隔字典中的键值对。

运算符
|运算符|功能|
|---|---|
|del|删除字典中指定键值对|

## 集合

集合（`set`）是简单对象的无序集合。

## 流程控制

### `if`语句

``` Python
if expression :
    code
```

``` Python
if expression :
    code
else :
    code
```

``` Python
if expression :
    code
elif expression :
    code
else :
    code
```

### `for`语句

``` Python
for value in set :
    code
```

``` Python
for value in set :
    code
else :
    code
```

### `while`语句

``` Python
while expression :
    code
```

``` Python
while expression :
    code
else :
    code
```

### `break`语句

中断当前循环语句

``` Python
    break
```

### `continue`语句

跳过当前循环块中的剩余语句并继续循环的下一次迭代

``` Python
    continue
```

## 内建函数

## 函数

### 函数定义

``` Python
def FunctionName(arg...) :
    code
```
### 局部变量

在函数中定义的变量均为局部变量，它们的作用域是变量定义所在的块。

### `global`语句

在函数内声明目标变量为全局变量。

``` Python
    global value
```

### `return`语句

中断函数执行，同时还可以选择从函数中返回一个值。

``` Python
    return value
```

### 默认参数值

在函数定义时附加一个赋值运算符（`=`）来为参数指定默认参数值。

``` Python
def FunctionName(arg = value) :
    code
```

### 位置参数

在调用函数时，实参将会被传递到对应位置的形参中。

### 关键字参数

在调用函数时，可以通过使用形参名传递实参而非根据位置传递实参。

``` Python
FunctionName(arg = value)
```

### 可变参数

如果需要定义一个参数数量可变的参数，则可以通过使用星号来实现。参数`*arg`将位置参数存储到元组`arg`中，参数`**arg`将关键字参数存储到字典`arg`中。

## 模块

### `import`语句

import语句用于导入模块。

``` Python
import module
```

``` Python
from module import var/method
```

### `__name__`

模块名称

## 类

### 类定义

``` Python
class ClassName :
    def __init__(self, arg...) :
        code
    
    def MethodName(self, arg...) :
        code
```

### `self`

### `__init__`方法

`__init__`方法会在创建类对象的实例时被调用，用于对实例进行初始化的方法。

### 类变量

类变量可以被该类的所有实例访问，是类的所有实例共同拥有的。

### 对象变量

对象变量是每个类实例独立拥有的，只能被所属实例访问。

### 私有变量

Python的类成员是公有的，除了使用双下划线作为名称前缀成为私有变量的数据成员。

### 继承派生

Python的继承和派生只需要在派生类的定义后面加上基类元组。Python的默认`__init__`方法会自动基类的`__init__`方法；而自定义的`__init__`方法则需显示调用基类的`__init__`方法。

``` Python
class Base :
    def __init__(self)
        code
class Derived(Base) :
    def __init__(self)
        Base.__init__(self)
        code
```

## 异常

### `raise`

使用`raise`语句可以抛出异常类`Exception`及其派生类作为一个异常。

### `try ... except`

``` Python
try :
    code
except :
    code
else :
    code
finally :
    code
```

### `with ... as`

`with`将自动调用`__enter__()`方法，并将结果传给`as`后的变量，在代码体运行完成后，`with`还将自动调用`__exit__()`方法，清理环境。
``` Python
with code as ValueName :
    code
```

### `assert`

`assert`用于断言表达式为真。若断言失败，将抛出一个`AssertionError`。
``` Python
assert expression 
```

## Lambda
