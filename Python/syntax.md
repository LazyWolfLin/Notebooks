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

## 流程控制

### if语句

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

### for语句

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

### while语句

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

### break语句

中断当前循环语句

``` Python
    break
```

### continue语句

跳过当前循环块中的剩余语句并继续循环的下一次迭代

``` Python
    continue
```

## 内建函数

## 函数

### 函数定义

``` Python
def function(arg...) :
    code
```
### 局部变量

在函数中定义的变量均为局部变量，它们的作用域是变量定义所在的块。

### global语句

在函数内声明目标变量为全局变量。

``` Python
    global value
```

### return语句

中断函数执行，同时还可以选择从函数中返回一个值。

``` Python
    return value
```

### 默认参数值

在函数定义时附加一个赋值运算符（`=`）来为参数指定默认参数值。

``` Python
def function(arg = value) :
    code
```

### 位置参数

在调用函数时，实参将会被传递到对应位置的形参中。

### 关键字参数

在调用函数时，可以通过使用形参名传递实参而非根据位置传递实参。

``` Python
function(arg = value)
```

### 可变参数

如果需要定义一个参数数量可变的参数，则可以通过使用星号来实现。参数`*arg`将位置参数存储到元组`arg`中，参数`**arg`将关键字参数存储到字典`arg`中，



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

列表由一系列有序元素组成。

Python使用方括号（`[]`）来表示列表，用逗号（`,`）分隔列表中元素。

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

## 字典

## 集合

## 模块

### import语句

import语句用于导入模块。

``` Python
import sys
```
