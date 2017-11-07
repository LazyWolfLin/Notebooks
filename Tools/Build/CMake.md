# `CMake`

## Syntax

### `PROJECT`

``` CMake
PROJECT(projectname [CXX] [C] [Java])
```

`PROJECT`指令用于定义项目名称，并制定项目支持的语言，默认支持所有语言。

### `SET`

```
SET(VAR [VALUE] [CACHE TYPE DOCSTRING [FORCE]])
```

`SET`指令用于显式定义变量。

### `MESSAGE`

```
MESSAGE([SEND_ERROR|STATUS|FATAL_ERROR] "message to display" ... )
```

`MESSAGE`指令用于向终端输出用户定义的消息，包含了三种类型：
`SEND_ERROR`：产生错误，构建过程被跳过。
`STATUS`：输出前缀为`--`的消息。
`FATAL_ERROR`：立即终止所以`CMake`的构建过程。

### `ADD_EXECUTABLE`

```
ADD_EXECUTABLE(executable_file sourse_file_list)
```

`ADD_EXECUTABLE`指令用于定义生成的可执行文件名和相关的源文件。