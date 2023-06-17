---
Title | Build Cmake CMD option
-- | --
Created @ | `2023-03-23T03:21:06Z`
Updated @| `2023-06-17T14:45:39Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/228)

---
# 使用 option 添加编译选项

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
- 使用 `BUILD_SHARED_LIBS` 的[地方](https://github.com/google/googletest/blob/e9fb5c7bacc4a25b030569c92ff9f6925288f1c3/googletest/cmake/internal_utils.cmake#L38)
```
  if (BUILD_SHARED_LIBS OR type STREQUAL "SHARED")
    set_target_properties(${name}
      PROPERTIES
      COMPILE_DEFINITIONS "GTEST_CREATE_SHARED_LIBRARY=1")
    if (NOT "${CMAKE_VERSION}" VERSION_LESS "2.8.11")
      target_compile_definitions(${name} INTERFACE
        $<INSTALL_INTERFACE:GTEST_LINKED_AS_SHARED_LIBRARY=1>)
    endif()
  endif()
```


## Reference

- [Documentation->cmake-commands(7)->option](https://cmake.org/cmake/help/latest/command/option.html)
