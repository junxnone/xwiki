---
Title | X Version
-- | --
Created @ | `2020-08-04T08:23:25Z`
Updated @| `2024-06-13T02:04:17Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/146)

---
# 版本号定义
- Semantic Versioning - `Major.Minor.Patch`
- 版本类型 - `先行版本号？`
  - Alpha
  - Beta
  - RC
  - Release

## Semantic Versioning 
- `Major.Minor.Patch`
  - **Major - 主版本号**：当你做了不兼容的 API 修改
  - **Minor - 次版本号**：当你做了向下兼容的功能性新增
  - **Patch - 修订号**：当你做了向下兼容的问题修正
- 主版本号为零（0.y.z）的软件处于开发初始阶段
- 先行版本号可以（MAY）被标注在修订版之后，先加上一个连接号再加上一连串以句点分隔的标识符来修饰。
  - 通常以"alpha"、"beta"或"rc"等标识符表示

```
<valid semver> ::= <version core>
                 | <version core> "-" <pre-release>
                 | <version core> "+" <build>
                 | <version core> "-" <pre-release> "+" <build>

<version core> ::= <major> "." <minor> "." <patch>

<major> ::= <numeric identifier>

<minor> ::= <numeric identifier>

<patch> ::= <numeric identifier>

<pre-release> ::= <dot-separated pre-release identifiers>

<dot-separated pre-release identifiers> ::= <pre-release identifier>
                                          | <pre-release identifier> "." <dot-separated pre-release identifiers>

<build> ::= <dot-separated build identifiers>

<dot-separated build identifiers> ::= <build identifier>
                                    | <build identifier> "." <dot-separated build identifiers>

<pre-release identifier> ::= <alphanumeric identifier>
                           | <numeric identifier>

<build identifier> ::= <alphanumeric identifier>
                     | <digits>

<alphanumeric identifier> ::= <non-digit>
                            | <non-digit> <identifier characters>
                            | <identifier characters> <non-digit>
                            | <identifier characters> <non-digit> <identifier characters>

<numeric identifier> ::= "0"
                       | <positive digit>
                       | <positive digit> <digits>

<identifier characters> ::= <identifier character>
                          | <identifier character> <identifier characters>

<identifier character> ::= <digit>
                         | <non-digit>

<non-digit> ::= <letter>
              | "-"

<digits> ::= <digit>
           | <digit> <digits>

<digit> ::= "0"
          | <positive digit>

<positive digit> ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

<letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J"
           | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T"
           | "U" | "V" | "W" | "X" | "Y" | "Z" | "a" | "b" | "c" | "d"
           | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n"
           | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x"
           | "y" | "z"

```



## 常见版本命名

Name | 开发阶段 | Description
-- | -- | --
Alpha | 开发期 | α是希腊字母的第一个，表示最早的版本，预览版，内部测试版，一般不向外部发布，bug会比较多，功能也不全，一般只有测试人员使用。
Beta | 开发期 | β是希腊字母的第二个，公开测试版，比alpha版本晚些，主要会有“粉丝用户”测试使用，该版本仍然存在很多bug，但比alpha版本稳定一些。这个阶段版本还会不断增加新功能。分为Beta1、Beta2等，直到逐渐稳定下来进入RC版本。
RC（Release Candidate） | 开发期 | 最终测试版本，发行候选版本，基本不再加入新的功能，主要修复bug。是最终发布成正式版的前一个版本，将bug修改完就可以发布成正式版了。多数开源软件会推出两个RC版本，最后的 RC2 则成为正式版本。
Release | 完成期 | 正式发布版，官方推荐使用的版本，有的用GA来表示。比如spring。
Final | 完成期 | 最终版，也是正式发布版的一种表示方法。比如Hibernate。
Stable | 完成期 | 稳定版，来自预览版本释出使用与改善而修正完成。
GA（General Availability）| 完成期 | 正式发布的版本；在国外都是用GA来说明release版本的。
RTM(Release to Manufacturing) | 完成期 | 给生产商的release版本；RTM版本并不一定意味着创作者解决了软件所有问题；仍有可能向公众发布前更新版本。另外一种RTM的称呼是RTW（Release To Web），表示正式版本的软件发布到Web网站上供客户免费下载。
RTL(Retail) | 完成期 | 零售版；是真正的正式版，正式上架零售版。 以Windows 7为例，RTM版与零售版的版本号是一样的。

## 其他

Name | Description
-- | -- 
Trial | 试用版 通常都有时间限制，有些试用版软件还在功能上做了一定的限制。可注册或购买成为正式版
Unregistered |  未注册版  通常没有时间限制，在功能上相对于正式版做了一定的限制。可注册或购买成为正式版。
Demo | 演示版  仅仅集成了正式版中的几个功能，不能升级成正式版 ，一般会有功能限制。
Lite | 精简版
Full version | 完整版  属于正式版。
Plus | 加强版
Delux | 豪华版 (deluxe: 豪华的，华丽的)
Enhance | 增强版或者加强版　属于正式版1
Free | 自由版
Upgrade | 升级版
Retail | 零售版
Cardware | 属共享软件的一种，只要给作者回复一封电邮或明信片即可。（有的作者并由此提供注册码等），目前这种形式已不多见。
Preview | 预览版
Corporation & Enterprise | 企业版
Standard | 标准版
Mini | 迷你版也叫精简版只有最基本的功能
Premium | 贵价版，旗舰版
Professional(Pro) | 专业版
Express| 特别版
Regged | 已注册版
Build | 内部标号
OEM | Original Equipment Manufacturer - 原始设备制造商；是给计算机厂商随着计算机贩卖的，也就是随机版；只能随机器出货，不能零售。只能全新安装，不能从旧有操作系统升级。包装不像零售版精美，通常只有一面CD和说明书(授权书)。
RVL | 号称是正式版，其实RVL根本不是版本的名称。它是中文版/英文版文档破解出来的。
EVAL | 而流通在网络上的EVAL版，与“评估版”类似，功能上和零售版没有区别。


## Reference
- [Alpha、Beta、RC、Release版本的区别](https://blog.csdn.net/lilongsy/article/details/83094977)
- [Semantic Versioning](https://semver.org/)
