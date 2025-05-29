---
Title | Hardware GPU iGPU ResizableBAR
-- | --
Created @ | `2025-05-29T02:33:26Z`
Updated @| `2025-05-29T02:33:26Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/313)

---
# Resizable BAR
- Resizable BAR(Base Address Register)：可调整大小的BAR（基地址寄存器）是一种PCIe功能，它能让PCIe设备（如独立显卡）协商BAR大小，从而优化系统资源，启用该功能可提升性能。



## 启用可调整大小的BAR的步骤

- **更新主板固件**：使用系统最新的支持Resizable BAR的主板固件。 
- **进入BIOS/UEFI配置菜单**：在系统启动时按DEL键进入（不同系统制造商的按键可能不同，必要时需向制造商查询具体说明）。
- **调整启动模式相关设置**：禁用兼容性支持模块（CSM）或传统模式，并启用UEFI启动模式。
- **开启特定设置**：确保“Above 4G Decoding”和“Re-Size BAR Support”设置为“Enabled”（若没有“Enabled”选项，则设为“Auto” ）。

## 确认是否启用成功

使用英特尔驱动和支持助手（Intel DSA）确认系统已启用Resizable BAR。该选项可能还有“Smart Access Memory”或“Clever Access Memory”等不同名称，具体可联系系统制造商了解。


## Reference
- [What Is Resizable BAR and How Do I Enable It?](https://www.intel.com/content/www/us/en/support/articles/000090831/graphics.html)
