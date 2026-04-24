---
Title | Programing Python Tools pyspy
-- | --
Created @ | `2026-04-24T02:44:36Z`
Updated @| `2026-04-24T02:44:36Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/322)

---
# py-spy

py-spy 是一款轻量级、非侵入式、低开销的 Python 程序性能分析工具，无需修改代码、无需重启程序、不会影响业务运行，可实时查看 Python 程序的 CPU 耗时、函数调用栈、线程性能，快速定位代码性能瓶颈。

- **核心特点：**
  - 非侵入式：无需插桩、无需重启目标程序
  - 低开销：性能损耗极小，生产环境可安全使用
  - 跨平台：支持 Linux/macOS/Windows
  - 可视化：支持生成火焰图、实时采样展示
  - 支持分析：运行中进程、子进程、远程进程

## 用法

py-spy 提供三个子命令：

| 命令 | 用途 |
|------|------|
| `py-spy record` | 采样并生成火焰图（SVG）或 speedscope 文件 |
| `py-spy top` | 实时查看函数耗时排名（类似 `top`） |
| `py-spy dump` | 一次性打印所有线程的当前调用栈 |

```
 py-spy --help
py-spy 0.4.1
Sampling profiler for Python programs

USAGE:
    py-spy <SUBCOMMAND>

OPTIONS:
    -h, --help       Print help information
    -V, --version    Print version information

SUBCOMMANDS:
    record    Records stack trace information to a flamegraph, speedscope or raw file
    top       Displays a top like view of functions consuming CPU
    dump      Dumps stack traces for a target program to stdout
    help      Print this message or the help of the given subcommand(s)

```



### dump stacks

```
py-spy dump -PID xxx
```


一次性打印目标进程**所有线程**的当前调用栈，适合：

- 排查进程卡死/死锁
- 快速了解程序当前在做什么
- 脚本化监控

加 `-l` 参数可显示本地变量：

```bash
py-spy dump --pid <PID> -l
```



```
Process xxxx: python your_script.py
Python v3.12.3 (/usr/bin/python3.12)

Thread 109556 (active): "MainThread"
    normalize_image (torchvision/transforms/v2/functional/_misc.py:55)
    wrapper (torchvision/transforms/v2/functional/_utils.py:32)
    _call_kernel (torchvision/transforms/v2/_transform.py:49)
    transform (torchvision/transforms/v2/_misc.py:174)
    forward (torchvision/transforms/v2/_transform.py:69)
    _call_impl (torch/nn/modules/module.py:1790)
    _wrapped_call_impl (torch/nn/modules/module.py:1779)
    forward (torchvision/transforms/v2/_container.py:52)
    _call_impl (torch/nn/modules/module.py:1790)
    _wrapped_call_impl (torch/nn/modules/module.py:1779)
    on_predict_batch_start (anomalib/pre_processing/pre_processor.py:129)
    _call_callback_hooks (lightning/pytorch/trainer/call.py:228)
    _predict_step (lightning/pytorch/loops/prediction_loop.py:244)
    run (lightning/pytorch/loops/prediction_loop.py:125)
    _decorator (lightning/pytorch/loops/utilities.py:179)
    _run_stage (lightning/pytorch/trainer/trainer.py:1118)
    _run (lightning/pytorch/trainer/trainer.py:1079)
    _predict_impl (lightning/pytorch/trainer/trainer.py:990)
    _call_and_handle_interrupt (lightning/pytorch/trainer/call.py:49)
    predict (lightning/pytorch/trainer/trainer.py:941)
    predict (anomalib/engine/engine.py:687)
    predict (predict.py:208)
    <module> (predict.py:296)
Thread 109638 (idle): "Thread-2"
    run (lightning/pytorch/callbacks/progress/rich_progress.py:83)
    _bootstrap_inner (threading.py:1073)
    _bootstrap (threading.py:1030)
```

### record 生成火焰图


```
py-spy record -p xxx

py-spy record -o profile.svg -- python my_script.py --arg1 value1
```

<img width="1200" height="682" alt="Image" src="https://github.com/user-attachments/assets/5460edec-55fd-43f6-b3e6-c6378453b33e" />


### top  实时性能监控


```bash
# 附加到正在运行的进程
py-spy top --pid <PID>

# 启动新进程
py-spy top -- python my_script.py
```

<img width="944" height="429" alt="Image" src="https://github.com/user-attachments/assets/edf86dff-43a7-4be0-ac86-6b0437639262" />



## 常见使用场景

### 场景 1：分析训练脚本性能瓶颈

```bash
# 启动训练脚本并生成火焰图
py-spy record -o train_profile.svg -- python train_model.py -d datasets/pcb1_train -o models

# 浏览器打开 SVG 查看
# 宽度 = 采样次数（CPU 时间占比），越宽的函数越耗时
```

### 场景 2：分析已经在跑的长时间任务

```bash
# 找到 PID
ps aux | grep python

# 附加采样
py-spy record -o profile.svg --pid 12345

# 不中断进程，按 Ctrl+C 结束采样
```

### 场景 3：排查推理脚本卡住

```bash
# 打印所有线程调用栈
py-spy dump --pid 12345

# 如果是死锁，会看到多个线程阻塞在锁相关的调用上
```

### 场景 4：对比优化前后

```bash
# 优化前
py-spy record -o before.svg -d 60 -- python predict.py --input test_data

# 优化后
py-spy record -o after.svg -d 60 -- python predict.py --input test_data

# 对比两个 SVG 火焰图，看目标函数的宽度是否缩小
```

## 火焰图阅读方法

```
┌────────────────────────────────────────────┐
│                  main()                     │  ← 调用栈底部（入口）
├─────────────────────┬──────────────────────┤
│     train()         │     evaluate()       │  ← 宽度 ∝ CPU 时间
├──────────┬──────────┤                      │
│ forward()│backward()│                      │  ← 调用栈顶部（实际执行的函数）
└──────────┴──────────┴──────────────────────┘
```

- **Y 轴**：调用栈深度，底部是入口函数，顶部是叶子函数
- **X 轴**：宽度代表该函数在采样中出现的比例（**不是时间顺序**）
- **颜色**：无特殊含义，仅用于区分不同函数
- **关注点**：顶层宽的函数 = 实际消耗 CPU 最多的函数

---

## 权限问题

py-spy 需要 `ptrace` 权限来读取目标进程内存。如果遇到权限错误：

```bash
# 方法 1：使用 sudo
sudo py-spy record -o profile.svg --pid <PID>

# 方法 2：临时放开 ptrace 限制（推荐开发环境使用）
sudo sysctl kernel.yama.ptrace_scope=0

# 方法 3：给 py-spy 添加 cap_sys_ptrace 能力
sudo setcap cap_sys_ptrace+ep $(which py-spy)
```

---

## 注意事项

1. **采样分析器 vs 追踪分析器**：py-spy 是采样器，开销极低（通常 < 1%），适合在生产环境使用；但它基于统计采样，非常短暂的函数调用可能被遗漏
2. **GIL 的影响**：py-spy 采样的是实际 CPU 时间，多线程 Python 程序中 GIL 导致的等待不会被计入
3. **`-n` 参数**：使用 NumPy/OpenCV/OpenVINO 等 C 扩展时，加 `-n` 可以看到 native 层调用栈，帮助判断瓶颈是否在 C 扩展内部
4. **Docker 中使用**：需要 `--cap-add SYS_PTRACE` 启动容器
5. **不支持的场景**：py-spy 不能分析 I/O 等待时间，如果瓶颈在磁盘/网络 I/O，火焰图中不会体现




## Reference

- [github](https://github.com/benfred/py-spy/)
