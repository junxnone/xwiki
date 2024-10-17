-----

| Title     | Programing Python os                                 |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-02-18T15:36:59Z`                               |
| Updated @ | `2024-10-17T08:20:18Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/311) |

-----

# os package

  - Python 标准库中的一个模块，用于与操作系统进行交互
  - 包含内容
      - 文件和目录操作
      - 路径操作
      - 环境变量操作
      - 系统命令执行
      - 进程相关操作

## 1\. 文件和目录操作

  - **`os.getcwd()`**
  - 获取当前工作目录的路径。
  - **`os.chdir(path)`**
  - 改变当前工作目录到指定的路径。
  - **`os.listdir(path)`**
  - 返回指定目录下的所有文件和子目录的名称列表。如果不指定路径，则返回当前工作目录下的列表。
  - **`os.mkdir(path)`**
  - 创建一个新的目录。如果目录已经存在，则会抛出`FileExistsError`异常。
  - **`os.makedirs(path)`**
  - 递归地创建多层目录。如果目录已经存在，则不会抛出异常。
  - **`os.remove(path)`**
  - 删除指定的文件。如果文件不存在，则会抛出`FileNotFoundError`异常。
  - **`os.rmdir(path)`**
  - 删除指定的空目录。如果目录不为空或不存在，则会抛出异常。
  - **`os.removedirs(path)`**
  - 递归地删除多层空目录。如果目录不为空或不存在，则会抛出异常。
  - **`os.path.cwd()`**
      - 获取当前脚本的所在路径

## 2\. 路径操作

  - **`os.path.join(path1, path2,...)`**
  - 将多个路径组合成一个路径，会根据操作系统自动使用正确的路径分隔符。
  - **`os.path.split(path)`**
  - 将路径分割为目录部分和文件名部分，并以元组形式返回。
  - **`os.path.dirname(path)`**
  - 返回路径中的目录部分。
  - **`os.path.basename(path)`**
  - 返回路径中的文件名部分。
  - **`os.path.exists(path)`**
  - 检查指定的路径是否存在。
  - **`os.path.isfile(path)`**
  - 检查指定的路径是否是一个文件。
  - **`os.path.isdir(path)`**
  - 检查指定的路径是否是一个目录。
  - **`os.path.getsize(path)`**
  - 获取指定文件的大小（以字节为单位）。
  - **`os.path.realpath`**
      - 获取当前执行脚本的绝对路径。
  - **`os.stat(path)`**
      - 获取path指定的路径的信息，功能等同于C API中的stat()系统调用。

## 3\. 环境变量操作

  - **`os.environ`**
      - 获取系统环境变量的字典。可以通过键值对的方式访问和修改环境变量。
  - **`os.getenv(key)`**
      - 获取指定环境变量的值。如果环境变量不存在，则返回`None`或指定的默认值。
  - **`os.putenv(key, value)`**
      - 设置指定环境变量的值。这种方式在某些情况下可能不被推荐，更推荐使用`os.environ[key] = value`的方式。

## 4\. 执行系统命令

  - **`os.system(command)`**
      - 在系统
        shell中执行指定的命令，并返回命令的退出码。例如`os.system("ls")`会执行`ls`命令并显示当前目录下的文件和目录列表。

## 5\. 进程相关操作

  - **`os.fork()`**
      - 创建一个新的进程。在Unix/Linux系统中常用，返回值为0表示子进程，返回值为子进程的PID表示父进程。
  - **`os.wait()`**
      - 等待子进程结束，并获取子进程的退出状态。
  - **`os.getpid()`**
      - 获取当前进程的PID。
  - **`os.getppid()`**
      - 获取当前进程的父进程的PID。

## Reference

  - [os module](https://www.programcreek.com/python/index/1/os)
