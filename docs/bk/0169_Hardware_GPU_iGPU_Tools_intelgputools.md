-----

| Title     | Hardware GPU iGPU Tools intelgputools                |
| --------- | ---------------------------------------------------- |
| Created @ | `2018-09-28T06:21:47Z`                               |
| Updated @ | `2024-09-03T02:09:46Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/169) |

-----

# intel-gpu-tools

  - 显示 Intel iGPU/dGPU 相关信息

## Install

    sudo apt install intel-gpu-tools

## UseCase

    sudo intel_gpu_top

``` 
intel-gpu-top: Intel Alderlake_s (Gen12) @ /dev/dri/card0 -    0/   0 MHz; 100% RC6;  0.00/33.32 W;        0 irqs/s

         ENGINES     BUSY                                      MI_SEMA MI_WAIT
       Render/3D    0.00% |                                      |      0%      0%
         Blitter    0.00% |                                      |      0%      0%
           Video    0.00% |                                      |      0%      0%
    VideoEnhance    0.00% |                                      |      0%      0%


```

### 查看特定 GPU

    intel_gpu_top -d drm:/dev/dri/card0
    intel_gpu_top -d drm:/dev/dri/card1

### 不用 sudo 执行 intel\_gpu\_top

    setcap cap_perfmon=+ep /usr/bin/intel_gpu_top
    sudo sh -c 'echo 2 >/proc/sys/kernel/perf_event_paranoid'

## Reference

  - [intel-gpu-tools](https://cgit.freedesktop.org/xorg/app/intel-gpu-tools/)
