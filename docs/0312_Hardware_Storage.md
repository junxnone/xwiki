---
Title | Hardware Storage
-- | --
Created @ | `2025-01-09T06:14:46Z`
Updated @| `2025-01-09T06:14:46Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/312)

---
# 存储
- `穿孔卡片` ==> 
- **磁性介质:** `磁带(Magnetic Tape)` ==> `光盘 - CD(Compact Disc) - DVD(Digital Versatile Disc) - BD(Blu - ray Disc)`  ==> `硬盘 HDD(Hard Disk Drive)` 
- **半导体存储介质:** ==> `固态硬盘 SSD(Solid State Drive)`



## HDD 机械硬盘 
- 硬盘主要由盘片、磁头、电机、控制电路等部件组成。盘片是存储数据的介质，表面涂有磁性材料。磁头负责读写数据，电机带动盘片高速旋转，当磁头在高速旋转的盘片上方移动时，通过改变盘片磁性材料的磁极方向来写入数据，通过检测磁极方向来读取数据。
- **特点:** 存储容量大，常见的硬盘容量可以达到数 TB（1TB = 1024GB）。数据传输速度相对较快，特别是对于顺序读写操作。不过，由于内部有机械部件，它的读写速度会受到电机转速等因素的限制，而且在受到震动或撞击时，盘片和磁头可能会损坏，导致数据丢失。

## SSD 固态硬盘
- 利用闪存芯片来存储数据
- 闪存是一种非易失性的半导体存储技术，它通过在闪存芯片的浮栅晶体管中存储电子来表示数据。在写入数据时，通过向晶体管的控制极施加高电压，将电子注入浮栅，改变晶体管的阈值电压来存储数据；读取数据时，通过检测晶体管的阈值电压来判断存储的数据
- **特点**: 读写速度比硬盘快很多，特别是随机读写性能优异。数据存储具有非易失性，在断电后数据不会丢失。不过，闪存芯片有写入寿命限制（P/E Cycles），经过一定次数的写入 / 擦除操作后，存储单元可能会损坏


## 硬盘接口
- 通信协议
  - IDE (Integrated Drive Electronics) 也叫 ATA (Advanced Technology Attachment)
  - SCSI (Small Computer System Interface)
  - NVMe (Non - Volatile Memory Express) 
  - SATA
  - AHCI
  - SAS
  - FC
- 物理接口
  - IDE
  - SATA (Serial ATA)
  - SAS
  - SCSI
  - M.2 
  - PCIe
  - U.2
  - AIC
  - FC

### NVMe

专门针对 PCIe 总线定制的一种 SSD 协议，充分利用了 PCIe 通道的低延时和高带宽特性，大大提升了固态硬盘的读写性能。


### M.2
- M.2 是一种物理接口规范，用于连接计算机内部的各种组件，主要是存储设备（如固态硬盘）和无线通信模块（如 Wi - Fi、蓝牙）等。它规定了设备的物理尺寸（如常见的 2230、2242、2260、2280 等尺寸）
- 2280 即 22x80 mm


