-----

| Title     | Hardware Board                                       |
| --------- | ---------------------------------------------------- |
| Created @ | `2026-04-29T06:03:26Z`                               |
| Updated @ | `2026-04-29T06:03:26Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/323) |

-----

# Board 完整板子层级

  - 从早到晚、从烂到稳 按芯片投产顺序排列，全套标准官方板卡类型如下，工控/服务器/桌面/移动端通用。

## 1\. EVB

**Evaluation Board 评估板**

  - 阶段：**最早，流片初版**
  - 用途：单纯点亮、基础寄存器调试、芯片基础功能 bringup
  - 特点： 线路简陋、供电阉割、无优化、**死机/掉电常态** 几乎不对外，只给IC原厂内部使用

## 2\. FCB / FHV

早期工程样片载板

  - 搭配 **FHL/FHV 裸片** 探针/软排座
  - 无标准插槽，纯底层调试，不会用作正常系统跑业务

-----

## 3\. **CRB** 【你已知道】

**Customer Reference Board**

  - 阶段：前期客户原型验证
  - 全功能拉满、预留大量测试点、Debug 接口、跳线
  - 供电/时序保守、未经稳定性优化
  - 典型问题：高负载硬死、随机重启、电源管理异常

-----

## 4\. **SVP**

**System Validation Platform** 介于 CRB 与 RVP 中间形态

  - 比 CRB 精简，比 RVP 更早
  - 用于整机基础兼容性、外设、存储、PCIe 验证
  - 稳定性中等，依旧**不适合长期满载**

-----

## 5\. **RVP** 【你已知道】

**Reference Validation Platform**

  - 阶段：量产前最终参考
  - 规格、供电、走线、散热**贴近零售主板**
  - 固件成熟、功耗/电源管理完善
  - 日常、满载、长时间运行稳定性远强于 CRB/SVP

-----

## 6\. CMB

**Customer Mother Board** 客户定制参考主板

  - Intel 给 ODM/OEM 的**定制化版型**
  - 在 RVP 基础上删减/扩展接口（多SATA、多网口、工控接口）
  - 接近品牌机/行业整机主板

-----

## 7\. MRB

**Mass Production Reference Board** 量产级参考板

  - 完全对齐零售/行业量产主板设计规范
  - 电气、散热、EMI、长期稳定性全部过规
  - 基本等同于正式商用主板

-----

## 8\. ERB / QRB（服务器/AI 平台常见）

  - **ERB：Enterprise Reference Board** 企业级参考板
  - **QRB：Quality Reference Board** 品质验证板 针对服务器、多CPU、多PCIe、AI加速卡场景
    供电冗余、VRM强化、长时间压力设计

-----

# 极简层级排序（稳定性从差→稳）

**EVB \< CRB \< SVP \< RVP \< CMB \< MRB \< ERB/QRB**
