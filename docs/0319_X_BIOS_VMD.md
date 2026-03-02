---
Title | X BIOS VMD
-- | --
Created @ | `2026-03-02T06:00:56Z`
Updated @| `2026-03-02T06:00:56Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/319)

---
# VMD 
- VMD = `Intel Volume Management Device`（卷管理设备）
- 英特尔 11 代酷睿及以后平台的PCIe/NVMe 存储管理技术
- **作用**：把多块 NVMe SSD 虚拟成统一存储池，支持CPU 级 RAID、热插拔、状态监控
- 常见于 Z690/Z790/B760 等新主板，出厂**默认常为 Enabled**



## 开启 vs 关闭：效果与场景
### ✅ 开启 VMD（Enabled）
- 适用：**多NVMe组RAID、服务器/工作站、需要热插拔**
- 优点：支持NVMe RAID 0/1/5/10、热插拔、状态监控、稳定性更好
- 缺点：
  - 原版Windows/PE**无驱动时找不到硬盘**
  - 装系统需**手动加载Intel RST VMD驱动**
  - 可能导致**蓝屏（INACCESSIBLE_BOOT_DEVICE）**

#### ❌ 关闭 VMD（Disabled）
- 适用：**单NVMe做系统盘、普通家用/游戏、重装系统找不到硬盘**
- 优点：
  - 系统/PE直接识别NVMe，**无需额外驱动**
  - 兼容性更好，**避免安装/启动蓝屏**
- 缺点：**无法使用NVMe RAID、热插拔、VMD管理功能**

---

## BIOS 里怎么找 VMD（常见路径）
1. 开机按 **Del / F2** 进BIOS
2. 按 **F7** 切到**高级模式（Advanced Mode）**
3. 常见路径：
   - 华硕：Advanced → VMD setup menu → Enable VMD Controller
   - 微星：Settings → Advanced → PCI Subsystem Settings → VMD Configuration
   - 技嘉：Settings → IO Ports → VMD Setup
   - 戴尔/惠普：System Configuration → Storage Options → Enable VMD Controller
4. 改为 **Disabled** → F10保存重启

---

## 最可能遇到的问题
### 1. 装系统找不到硬盘 / PE不认盘
→ 进BIOS **关闭VMD** 即可解决

### 2. 开机蓝屏 INACCESSIBLE_BOOT_DEVICE
→ 进BIOS **切换VMD状态**（开→关 或 关→开）

### 3. 想组NVMe RAID
→ 必须**开启VMD**，并在BIOS/Intel RST里配置RAID

