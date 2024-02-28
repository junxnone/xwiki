-----

| Title     | Build Cmake Install                                 |
| --------- | --------------------------------------------------- |
| Created @ | `2021-07-15T06:06:27Z`                              |
| Updated @ | `2024-02-28T01:50:08Z`                              |
| Labels    | \`\`                                                |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/54) |

-----

# Install CMake

## Linux

  - apt install
  - Download the prebuild files
  - install from source code

### Ubuntu 16.04 Install newer cmake 3.21.1

    wget https://cmake.org/files/v3.21/cmake-3.21.1-linux-x86_64.tar.gz
    tar zvxf cmake-3.21.1-Linux-x86_64.tar.gz
    vi ~/.bashrc

    export PATH="/your/cmake/path/bin:$PATH"

    source ~/.bashrc

    $ cmake --version
    cmake version 3.21.1

### Build from source code

    wget https://cmake.org/files/v3.16/cmake-3.16.9.tar.gz
    tar zvxf cmake-3.16.9.tar.gz
    cd cmake-3.16.9
    ./configure
    make
    sudo make install

## Windows

  - download the [msi](https://cmake.org/download/) and install the
    package

### Set Proxy

  - 适用 cmake 下载时需要配置 proxy 的情况

<!-- end list -->

    set HTTP_PROXY=<your-proxy-here>
    set HTTPS_PROXY=<your-proxy-here>
    cmake-gui

## Reference

  - [Downloads](https://cmake.org/files/)
