-----

| Title     | Hardware GPU iGPU Tools                              |
| --------- | ---------------------------------------------------- |
| Created @ | `2021-12-13T11:35:31Z`                               |
| Updated @ | `2023-05-24T15:09:38Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/153) |

-----

# Intel iGPU Tools

  - inxi
  - lspci
  - intel\_gpu\_top
  - [Intel® GPU Occupancy
    Calculator](https://oneapi-src.github.io/oneAPI-samples/Tools/GPU-Occupancy-Calculator/index.html)
  - [Intel(R) XPU Manager and XPU System Management
    Interface](https://github.com/intel/xpumanager/tree/master)

### 查看 iGPU info

    inxi -G

    ls -al /dev/dri

    sudo lspci -v -s $(lspci | grep VGA | cut -d" " -f 1)

    $ lspci |grep VGA
    00:02.0 VGA compatible controller: Intel Corporation Device 9a49 (rev 01)

> 9a49 mean `Intel® Iris® Xe Graphics`, others you can found
> [here](https://dgpu-docs.intel.com/devices/hardware-table.html)

### 查看 iGPU 使用率

    sudo apt install intel-gpu-tools
    sudo intel_gpu_top