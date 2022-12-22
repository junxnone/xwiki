---
Title | Hardware GPU iGPU Tools telemetry
-- | --
Created @ | `2018-09-27T02:18:25Z`
Last Modify @| `2022-12-22T07:58:09Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/171)

---
# intel-telemetry-tool


## Reference
- [intel-telemetry-tool](https://github.com/Xiaogang-Li/intel-telemetry-tool)

## Brief
- CPU/GPU evaluate calculation capability Tool Kit

## Build & Install

```
git clone https://github.com/Xiaogang-Li/intel-telemetry-tool.git
cd intel-telemetry-tool/build
./prebuild.sh
cd ..
./build.sh
sudo cp telemetry /usr/bin/
```


## UseCase

```
sudo telemetry
```
 - s : show statistics

![image](https://user-images.githubusercontent.com/2216970/61400059-09259f00-a902-11e9-8162-a1f2f7aa5cd3.png)


