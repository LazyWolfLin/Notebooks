# `ProtoBuf`

`ProtoBuf`是一种语言无关，平台无关的可扩展的序列化工具。

## A simple example

这是一个简单例子

```
syntax = "proto3";

message example {
  int32 Message_Type = 1;
  string Message_Data = 2;
}
```

使用`proto3`编写一份`.proto`文件时，必须在文件的第一个非空且非注释行声明此文件使用`proto3`语法，否则`ProtoBuf`编译器将认为这是一份`proto2`文件。

## `Message`

每个`Message`类型由多个字段`field`构成。每个`field`由可选的`Rule`和必选的`Type`、`Name`和`tag`组成，即`[Rule] Type Name = tag;`。

## `Type`

## `Default Value`

|Type|Default Value|
|---|---|
|strings|empty string|
|bytes|empty bytes|
|bools|false|
|numeric|zero|
|enum|first defined enum value(zero)|
|message|no set|

Tips：根据个人开发经验，`Default Value`代表错误值方便开发升级。