---
Title | Hardware GPU iGPU Tools
-- | --
Created @ | `2021-12-13T11:35:31Z`
Last Modify @| `2022-12-22T07:29:08Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/153)

---
## Brief
- inxi
- lspci
- intel_gpu_top
- [Intel® GPU Occupancy Calculator](https://oneapi-src.github.io/oneAPI-samples/Tools/GPU-Occupancy-Calculator/index.html)

### 查看 iGPU info

```
inxi -G
```
```
ls -al /dev/dri
```

```
sudo lspci -v -s $(lspci | grep VGA | cut -d" " -f 1)
```
```
$ lspci |grep VGA
00:02.0 VGA compatible controller: Intel Corporation Device 9a49 (rev 01)
```


> 9a49 mean `Intel® Iris® Xe Graphics`, others you can found [here](https://dgpu-docs.intel.com/devices/hardware-table.html)


### 查看 iGPU 使用率

```
sudo apt install intel-gpu-tools
sudo intel_gpu_top
```

