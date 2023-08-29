---
Title | Build Cmake CMD option
-- | --
Created @ | `2023-03-23T03:21:06Z`
Updated @| `2023-08-29T13:37:24Z`
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

## Tips

### List the build options
- 可以用来备份对比编译选项

CMD | Description
-- | --
`cmake -L` | print all options
`cmake -LH` | print all options with help message
`cmake -LA` | print all options including advanced

```
$cmake -L
BUILD_CUDA_STUBS:BOOL=OFF
CMAKE_BUILD_TYPE:STRING=Release
CMAKE_INSTALL_PREFIX:PATH=/usr/local
...
```

```
$cmake -LH
// Build CUDA modules stubs when no CUDA SDK
BUILD_CUDA_STUBS:BOOL=OFF

// Choose the type of build
CMAKE_BUILD_TYPE:STRING=Release

// Installation Directory
CMAKE_INSTALL_PREFIX:PATH=/usr/local

...
```


## Reference

- [Documentation->cmake-commands(7)->option](https://cmake.org/cmake/help/latest/command/option.html)
- [List non-advanced cached variables](https://cmake.org/cmake/help/latest/manual/cmake.1.html#cmdoption-cmake-L-A-H)
