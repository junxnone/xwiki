---
Title | Hardware PTAT
-- | --
Created @ | `2026-08-31T08:01:34Z`
Updated @| `2026-08-31T08:13:56Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/328)

---
# PTAT 

- Power and Thermal Analysis Tool


## Monitor

### Power


名称 | 全称 | 中文 | 说明 | 例 (W)
-- | -- | -- | -- | --
IA Power | Intel‑Architecture Power | CPU 核心功耗 | P‑Core+E‑Core 性能核 + 能效核的功耗，只算 CPU 计算核心，不含核显、缓存、I/O | 4.707635
GT Power | Graphics Power | 核显功耗 | 内置核芯显卡（GT 单元）的功耗；没有核显的 CPU，该数值≈0 | 26.35466
Rest of Package Power | Rest of Package Power | 封装其余部分功耗 | CPU 封装内除去 IA 核心、GT 核显之外的 Uncore 非核心模块功耗，包含环形总线、缓存等 | 6.348348
Package Power | CPU Package Power | CPU 封装总功耗 | 整颗 CPU 芯片总功耗 = IA 核心 + GT 核显 + Rest of Package，包含 SoC 全部模块，最能代表 CPU 真实耗电 | 37.41065
Effective EWMA PeciMmio | Effective EWMA PeciMmio | EWMA 平滑有效功耗 | EWMA 指数加权平均算法平滑后的 CPU 平均功耗，PECI/MMIO 通道读取，反映一段时间平均功耗 | 27.94534
MSR Psys Power | MSR Psys Power | MSR 读取平台功耗 | MSR 寄存器读取的 Psys 整机平台功耗，平台不支持读取则显示 0.000000 | 0.000000
Psys EWMA Power | Psys EWMA Power | 平台 EWMA 平均功耗 | Psys 整机平台功耗的 EWMA 平滑值，平台不支持读取则显示 0.000000 | 0.000000
PECI Psys Power | PECI Psys Power | PECI 读取平台功耗 | 通过 PECI 接口获取的整机平台功耗 | 3.360207
SA Power | System Agent Power | 系统代理功耗 | 系统代理模块功耗，包含内存控制器、PCIe 控制器、相关 I/O 模块 | 1.864793
Turbo Budget | Turbo Budget | 睿频功耗余量 | 当前系统剩余可用于睿频的功耗额度，余量越小越容易触发降频 | 17.12181


### Config TDP

名称 | 全称 | 中文 | 说明 | 数值
-- | -- | -- | -- | --
isConfigTDPSupported | is Config TDP Supported | 是否支持可配置 TDP | 该 CPU 是否支持 cTDP（Configurable TDP）可配置功耗档位特性；1 = 支持，0 = 不支持 | 1（支持）
numberOfConfigTDPLevels | Number of Config TDP Levels | TDP 档位数量 | 固件里预置的可切换功耗档位数 | 2
isConfigTDPLocked | is Config TDP Locked | 是否锁定档位 | 档位是否被锁死、不可切换；1 = 锁定，0 = 可切换 | 0（未锁定）
CurrentTDPLevel | Current TDP Level | 当前档位 | 当前正在使用的 TDP 档位编号 | 2
NominalTDPFrequency | Nominal TDP Frequency | 标称 TDP 频率 | 在标称 TDP 功耗下 CPU 全核能达到的频率 | 1900 MHz
Turbo Activation Ratio | Turbo Activation Ratio | 睿频激活倍频 | 触发睿频的倍频（×100MHz）；36 倍频≈3.6GHz | 36
Package TDP Power | Package TDP Power | 当前封装功耗设定 | 当前生效的 CPU 封装功耗档值 | 25 W
CTDP1-TDPFrequency | Config TDP Level1 Frequency | 档位 1 频率 | 低功耗档对应的频率 | 1000 MHz
CTDP1-PackageMinPower | CTDP1 Package Min Power | 档位 1 最小功耗 | 档位 1 的最小封装功耗设定 | 0 W
CTDP1-PackageMaxPower | CTDP1 Package Max Power | 档位 1 最大功耗 | 档位 1 的最大封装功耗设定 | 0 W
CTDP1-PackageTDP | CTDP1 Package TDP | 档位 1 TDP | 档位 1 的额定 TDP | 15 W
CTDP2-TDPFrequency | Config TDP Level2 Frequency | 档位 2 频率 | 高性能档对应的频率 | 3700 MHz
CTDP2-PackageMinPower | CTDP2 Package Min Power | 档位 2 最小功耗 | 档位 2 的最小封装功耗设定 | 0 W
CTDP2-PackageMaxPower | CTDP2 Package Max Power | 档位 2 最大功耗 | 档位 2 的最大封装功耗设定 | 0 W
CTDP2-PackageTDP | CTDP2 Package TDP | 档位 2 TDP | 档位 2 的额定 TDP | 65 W




