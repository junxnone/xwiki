---
Title | Build Cmake if
-- | --
Created @ | `2023-08-18T14:44:37Z`
Updated @| `2023-08-18T14:54:09Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/288)

---
# if
- 条件控制语句

```
if(<condition>)
  <commands>
elseif(<condition>) # optional block, can be repeated
  <commands>
else()              # optional block
  <commands>
endif()
```

## condition
- Basic Expressions
  - constant
  - variable
  - string
- Logic Operators(逻辑操作)
  - NOT
  - AND
  - OR
- Existence Checks(存在性检查)
  - **COMMAND**: 如果给定的命令、宏或函数是可以调用的，则为 True
  - **POLICY**: Policy 存在
  - **TARGET**: 如果 target 已经定义([add_executable()](https://cmake.org/cmake/help/latest/command/add_executable.html#command:add_executable)/ [add_library()](https://cmake.org/cmake/help/latest/command/add_library.html#command:add_library)/ [add_custom_target()](https://cmake.org/cmake/help/latest/command/add_custom_target.html#command:add_custom_target))
  - **TEST**: test 已经定义([add_test()](https://cmake.org/cmake/help/latest/command/add_test.html#command:add_test))
  - **DEFINED**: 变量被定义
  - **IN_LIST**: 给定值存在 list 变量中
- File Operations(文件操作)
  - EXISTS: 文件或目录存在
  - IS_NEWER_THAN: 比较文件时间戳
  - IS_DIRECTORY ：判断是否是目录
  - IS_SYMLINK ：是否是软连接
  - IS_ABSOLUTE ： 是否是绝对路径
- 比较
  - MATCHES
  - LESS
  - GREATER
  - EQUAL
  - LESS_EQUAL
  - GREATER_EQUAL
  - STRLESSSTRGREATER
  - STREQUAL
  - STRLESS_EQUAL
  - STRGREATER_EQUAL
- 版本比较
  - VERSION_LESS
  - VERSION_GREATER
  - VERSION_EQUAL
  - VERSION_LESS_EQUAL
  - VERSION_GREATER_EQUAL
- 路径比较
  - PATH_EQUAL


## Reference
- [Cmake command if](https://cmake.org/cmake/help/latest/command/if.html#command:if)
