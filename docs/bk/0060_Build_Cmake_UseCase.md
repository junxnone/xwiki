-----

| Title     | Build Cmake UseCase                                 |
| --------- | --------------------------------------------------- |
| Created @ | `2021-07-15T06:05:14Z`                              |
| Updated @ | `2023-08-29T13:25:09Z`                              |
| Labels    | \`\`                                                |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/60) |

-----

# CMake UseCase

  - command-line mode
  - Generate Makefiles
  - Generate Visual Studio Solution

-----

  - Files
      - CMakeLists.txt
      - `<script>.cmake`
      - `<module>.cmake`

## UseCase

### 简单demo

    cmake_minimum_required (VERSION 2.6) # 兼容的 cmake  最小版本
    project(demo)  # 项目名称
    add_executable(demo demo.cxx) # 使用 demo.cxx 生成可执行文件 demo

### 设置版本号

    set(PROJECT_VERSION 1.0.1.1) # 单独设置版本号

    project(Tutorial VERSION 1.0) # 设置项目名称时设置版本号

    project(demo VERSION <major>[.<minor>[.<patch>[.<tweak>]]])

## CMDLine Usecase

| Description | CMDLine args `cmake [xxx]`                   |
| ----------- | -------------------------------------------- |
| 指定安装位置      | `-D CMAKE_INSTALL_PREFIX=/your/install/path` |

## Reference

  - [wiki](https://gitlab.kitware.com/cmake/community/-/wikis/home)
  - [Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html)
