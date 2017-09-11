# Java

## 标识符

标识符是在Java中元素的名称的代码。在Java中的标识符有如下规定：
1. 标识符大小写敏感。
2. 标识符可以由字母和数字构成，字母可以来自任何Unicode字符。
3. 标识符只能以字母、下划线(`_`)或者美元符号(`$`)为开头。
4. 标识符不能等于保留关键字，空文字(null)或布尔文字(true, false)。

## Java关键字

|关键字|描述|
|---|---|
|abstract|抽象方法，抽象类的修饰符|
|assert|断言条件是否满足|
|boolean|布尔类型|
|break|退出当前循环体|
|byte|byte类型|
|case||
|catch||
|char|字符类型|
|class|类|
|const||
|continue|不执行循环体剩余部分|
|default|switch语句中的默认分支|
|do|循环语句，循环体至少会执行一次|
|double|64-bit双精度浮点数|
|else|if条件不成立时执行的分支|
|enum|枚举类型|
|extends|表示一个类是另一个类的子类|
|final|表示定义常量|
|finally|无论有没有异常发生都执行代码|
|float|32-bit单精度浮点数|
|for|for循环语句|
|goto|用于流程跳转（未使用）|
|if|条件语句|
|implements|表示一个类实现了接口|
|import|导入类|
|instanceof|测试一个对象是否是某个类的实例|
|int|32位整型数|
|interface|接口，一种抽象的类型，仅有方法和常量的定义|
|long|64位整型数|
|native|表示方法用非java代码实现|
|new|分配新的类实例|
|package|一系列相关类组成一个包|
|private|表示私有字段，或者方法等，只能从类内部访问|
|protected|表示保护类型字段|
|public|表示共有属性或者方法|
|return|方法返回值|
|short|16位数字|
|static|表示在类级别定义，所有实例共享的|
|strictfp|浮点数比较使用严格的规则|
|super|表示基类|
|switch|选择语句|
|synchronized|表示同一时间只能由一个线程访问的代码块|
|this|调用当前实例或者调用另一个构造函数|
|throw|抛出异常|
|throws|定义方法可能抛出的异常|
|transient|修饰不要序列化的字段|
|try|表示代码块要做异常处理|
|void|标记方法不返回任何值|
|volatile|标记字段可能会被多个线程同时访问，而不做同步|
|while|while循环|

## 基本数据类型

|数据类型|位数|取值范围|
|---|---|---|
|byte|8位|-128 ~ 127|
|short|16位|-32768 ~ 32767|
|int|32位|-2147483648 ~ 2147483647|
|long|64位|-9223372036854775808 ~ 9223372036854775807|
|float|32位|1.4E-45 ~ 3.4028235E38|
|double|64位|4.9E-45 ~ 1.7976931348623157E308|
|char|16位|'\u0000' (0) ~ '\uffff' (655335)|
|boolean|8位|true, false|

## 声明

### 变量声明

### 数组声明

## 运算符和表达式

## 流程控制

### 逻辑控制

if语句
``` Java
if (expression) {
    code;
}
```
if-else语句
``` Java
if (expression) {
    code;
}
else {
    code;
}
```

switch语句
``` Java
switch (expression) {
    case value:
        code;
        break;
    case value:
        code;
        break;
    default:
        code;
}
```

### 循环控制

while语句
``` Java
while (expression) {
    code;
}
```
do-while语句
``` Java
do {
    code;
}while (expression);
```

for语句
``` Java
for (begin expression; end expression; expression) {
    code;
}
```
