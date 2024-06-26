-----

| Title     | Programing Python Tools psutil                      |
| --------- | --------------------------------------------------- |
| Created @ | `2021-03-10T05:45:34Z`                              |
| Updated @ | `2024-04-23T02:35:15Z`                              |
| Labels    | \`\`                                                |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/98) |

-----

# psutil

  - 获取系统信息
  - Support OS
      - Linux
      - Windows
      - macOS
      - FreeBSD, OpenBSD, NetBSD
      - Sun Solaris
      - AIX
  - Functions
      - System related functions
          - CPU
          - Memory
          - Disks
          - Network
          - Sensors
          - Other System Info
      - Processes
      - Windows Services
      - Constants
      - Recipes

## UseCase

### 统计信息

| UC                 | Func                                          |
| ------------------ | --------------------------------------------- |
| 获取 CPU 数量(逻辑核/超线程) | `psutil.cpu_count()`                          |
| 物理核数量              | `psutil.cpu_count(logical=False)`             |
| CPU time           | `psutil.cpu_times()`                          |
| 统计 CPU 使用率         | `psutil.cpu_percent(interval=1, percpu=True)` |
| 内存信息               | `psutil.virtual_memory()`                     |
| 硬盘信息               | `psutil.disk_partitions()`                    |
| 磁盘使用情况             | `psutil.disk_usage('/')`                      |
| 磁盘IO               | `psutil.disk_io_counters()`                   |
| 获取网络读写字节／包的个数      | `psutil.net_io_counters()`                    |
| 获取网络接口信息           | `psutil.net_if_addrs()`                       |
| 获取网络接口状态           | `psutil.net_if_stats()`                       |
| 网络连接信息             | `psutil.net_connections()`                    |
| 进程信息               | `psutil.pids()`                               |

### Processes

  - 绑定进程到 CPU

## Reference

  - [Docs](https://psutil.readthedocs.io/en/latest/)
  - [Code](https://github.com/giampaolo/psutil)
