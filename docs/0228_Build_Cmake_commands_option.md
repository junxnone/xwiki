---
Title | Build Cmake commands option
-- | --
Created @ | `2023-03-23T03:21:06Z`
Updated @| `2023-03-23T03:25:21Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/228)

---
# option

- 提供一个 `Boolean` 类型的选项
- 可以在 命令行中 `cmake ..` 时使用

## 用法

```
option(<variable> "<help_text>" [value])
```
- 默认值 `OFF`


### Examples
- 编译 gtest 时想要编译动态库

```
cmake .. -DBUILD_SHARED_LIBS=ON
```

- 对应 [CmakeLIsts.txt](https://github.com/google/googletest/blob/5fce13091d223069436ad7a5aad53f026b0f2041/googletest/CMakeLists.txt#L66)

```
  # BUILD_SHARED_LIBS is a standard CMake variable, but we declare it here to
  # make it prominent in the GUI.
  option(BUILD_SHARED_LIBS "Build shared libraries (DLLs)." OFF)
```


## Reference

- [Documentation->cmake-commands(7)->option](https://cmake.org/cmake/help/latest/command/option.html)
