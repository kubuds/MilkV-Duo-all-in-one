# Milk-V Duo 系列资源总汇（Duo · Duo 256M · Duo S）

Milk-V Duo 系列所有能找到的资源，尽量都收在这一页：官方文档与数据手册、可直接下载的镜像、SDK 与工具链、GitHub 与 Gitee 上的开源项目，以及 B 站和 YouTube 上真的用了这块板子的视频。

这一页不复制、不镜像任何固件和文档本体，只给出处和维护者。**社区镜像与项目未经 Milk-V 测试或背书**，烧录前请自己核对板型、SoC、内存、存储介质与发行说明。

> **先确认你手里是哪块板。** 三代产品并不是同一个东西：Duo 用 CV1800B（64 MB 内存），Duo 256M 用 SG2002（256 MB，多一个 Cortex-A53），Duo S 用 SG2000（512 MB，可选 Wi-Fi 6 / BT5 与可选 eMMC）。**原版 Duo 已被官方标记为停产（EOL）**，新项目建议直接上 256M 或 Duo S。

---

## 1. 板型与变体

| 型号 | SoC | 内存 | 存储 | 无线 | 以太网 | TPU | 状态 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Duo** | CVITEK CV1800B | 64 MB | microSD 或板载 SD NAND | 无 | 100M（PHY） | 0.5 TOPS@INT8 | 停产 EOL |
| **Duo 256M** | SG2002 | 256 MB | microSD 或板载 SD NAND | 无 | 100M（PHY） | 1.0 TOPS@INT8 | 在售 |
| **Duo S** | SG2000 | 512 MB | microSD + 板上 eMMC 位 | **可选** Wi-Fi 6 / BT5 | 100M（RJ45，支持 PoE HAT） | 0.5 TOPS@INT8 | 在售 |
| **Duo Module 01**（核心板 + 评估板） | SG2000 | 512 MB | 8 GB eMMC 板载 | Wi-Fi 6 / BT5.4 板载 | 2× 100M | 0.5 TOPS@INT8 | 在售 |

**Duo S 的四种组合**：eMMC 焊不焊 × Wi-Fi 模块焊不焊，共四种 SKU。买的时候看清楚商品页写的是哪一种。

镜像**只按启动介质区分**（`-sd` / `-emmc`），不按 Wi-Fi 区分 —— 官方 v2.0.1 的七个资产里没有任何带 wifi 字样的镜像（见下表）。所以：

- 有 / 无 Wi-Fi 的 Duo S 刷同一份镜像，无线功能靠的是板上有没有那颗模块
- 有 eMMC 的板子既可以刷 `-sd` 从 TF 卡启动，也可以刷 `-emmc` 烧到板载存储
- **没有** eMMC 的板子只能走 TF 卡

---

## 2. 购买渠道

淘宝「苦芽企业店」在售以下三款（商品页需登录淘宝才能看到详情，链接本身实测返回 200）：

- **Milk-V Duo 256M**（SG2002，256 MB，无 Wi-Fi）：https://item.taobao.com/item.htm?id=842972320584&skuId=5661357677549
- **Milk-V Duo S 基础版**（SG2000，512 MB，无 Wi-Fi、无 eMMC）：https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544644
- **Milk-V Duo S Wi-Fi 版**（SG2000，512 MB，带 Wi-Fi 6 / BT，无 eMMC）：https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544645

Duo S 那两个是**同一个商品的两个 SKU**（`id` 相同、`skuId` 不同），下单时看清 SKU 名称里有没有 Wi-Fi；两款都没有 eMMC，要板载存储得另找带 eMMC 的版本。原版 Duo（CV1800B）已停产，不放购买链接。

这是全页唯一带商业性质的部分，其余内容只指向上游出处。

---

## 3. 官方文档、数据手册与硬件资料

**文档站：挨页索引**

- 起点：[Duo 系列概览与规格对比](https://milkv.io/docs/duo/overview)（四款产品完整规格表，也是 EOL 声明的出处） · [文档站首页](https://milkv.io/docs/duo/getting-started)
- 各板指南：[Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos) · [Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- 上电与烧录：[启动系统](https://milkv.io/docs/duo/getting-started/boot) · [首次连接与 USB 网络](https://milkv.io/docs/duo/getting-started/setup) · [镜像下载总表](https://milkv.io/docs/duo/getting-started/download) · [Buildroot SDK 构建](https://milkv.io/docs/duo/getting-started/buildroot-sdk)
- 双核与低层：[辅助核 8051 开发](https://milkv.io/docs/duo/getting-started/8051core) · [RTOS 小核开发](https://milkv.io/docs/duo/getting-started/rtoscore) · [Arduino 支持](https://milkv.io/docs/duo/getting-started/arduino) · [低层开发](https://milkv.io/docs/duo/low-level-dev)（[MIPI DSI](https://milkv.io/docs/duo/low-level-dev/mipi-dsi)）
- 应用开发：[总览](https://milkv.io/docs/duo/application-development) · [GPIO sysfs](https://milkv.io/docs/duo/application-development/gpio-sysfs) · [引脚复用](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [pinpong](https://milkv.io/docs/duo/application-development/pinpong) · [多媒体框架](https://milkv.io/docs/duo/application-development/multimedia)
- 摄像头：[USB 摄像头](https://milkv.io/docs/duo/camera/usb) · [GC2083 传感器](https://milkv.io/docs/duo/camera/gc2083) · [ISP tuning](https://milkv.io/docs/duo/camera/tuning)
- TPU 与 TDL：[TPU 简介](https://milkv.io/docs/duo/application-development/tpu/tpu-introduction) · [TDL SDK 简介](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-introduction) · YOLO：[v5](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov5) · [v8](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov8) · [v11](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo11) · [v12](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo12) · [人脸检测](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-face-detection) · [行人检测](https://milkv.io/docs/duo/application-development/tdl-sdk/pedestrian-detection) · [人宠检测](https://milkv.io/docs/duo/application-development/tdl-sdk/yolov8-person-pets-detection)
- IO 扩展板：[IO Board 总览](https://milkv.io/docs/duo/io-board) · [Duo S PoE HAT](https://milkv.io/docs/duo/io-board/duos-poe-hat) · [USB 以太网 IO 板](https://milkv.io/docs/duo/io-board/usb-ethernet-iob)
- 官方整理的资源与生态进展：[有用资源总表](https://milkv.io/docs/duo/useful-resources) · [主线内核支持状态](https://milkv.io/docs/duo/resources/mainline) · [上游支持现状](https://milkv.io/docs/duo/resources/upstream-status) · [MMF 多媒体框架](https://milkv.io/docs/duo/resources/mmf) · [OpenCV Mobile](https://milkv.io/docs/duo/resources/opencv-mobile) · [SPILVGL](https://milkv.io/docs/duo/resources/spilvgl) · [Visuino](https://milkv.io/docs/duo/resources/visuino) · [xyzdims 笔记](https://milkv.io/docs/duo/resources/xyzdims)
- [文档站源码](https://github.com/milk-v/milkv.io) —— 文档有错或想补翻译，往这里提 PR

**产品页**

- [Duo（系列页）](https://milkv.io/duo) · [Duo S](https://milkv.io/duo-s) · [Duo Module 01](https://milkv.io/duo-module-01)
- Duo 256M 没有独立的商品页，规格见系列页与[文档](https://milkv.io/docs/duo/getting-started/duo256m)

**硬件文件与芯片手册**

- [duo-files](https://github.com/milkv-duo/duo-files) —— 官方板级文件总库：原理图、数据手册、机械图、丝印
- 原理图：[Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)
- 数据手册：[CV1800B/CV1801B 英文](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf)（[中文](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf)） · [SG2002 中文](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 中文](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 TRM 英文](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)
- [Sophgo 文档发布页](https://github.com/sophgo/sophgo-doc/releases) —— 上游芯片文档的正式出口

---

## 4. 官方镜像与烧录

官方镜像全部基于 Buildroot，分 V1 / V2 两条线。**64 MB 的 Duo 建议用 V1**（V2 的 AI 示例在 64 MB 上跑不动）；Duo 256M 与 Duo S 用 V2。

### V2（推荐给 Duo 256M / Duo S）· [v2.0.1，2025-05-30](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)

| 资产文件 | 板型 | 启动介质 | C 库 / 架构 |
| --- | --- | --- | --- |
| `milkv-duo-musl-riscv64-sd_v2.0.1.img.zip` | Duo | TF 卡 | musl / riscv64 |
| `milkv-duo256m-musl-riscv64-sd_v2.0.1.img.zip` | Duo 256M | TF 卡 | musl / riscv64 |
| `milkv-duo256m-glibc-arm64-sd_v2.0.1.img.zip` | Duo 256M | TF 卡 | glibc / arm64（走 A53） |
| `milkv-duos-musl-riscv64-sd_v2.0.1.img.zip` | Duo S | TF 卡 | musl / riscv64 |
| `milkv-duos-glibc-arm64-sd_v2.0.1.img.zip` | Duo S | TF 卡 | glibc / arm64（走 A53） |
| `milkv-duos-musl-riscv64-emmc_v2.0.1.zip` | Duo S（需 eMMC） | 板载 eMMC | musl / riscv64 |
| `milkv-duos-glibc-arm64-emmc_v2.0.1.zip` | Duo S（需 eMMC） | 板载 eMMC | glibc / arm64 |

### V1 · [v1.1.4，2024-11-22](https://github.com/milkv-duo/duo-buildroot-sdk/releases)

| 资产文件 | 板型 | 启动介质 |
| --- | --- | --- |
| `milkv-duo-sd-v1.1.4.img.zip` | Duo | TF 卡 |
| `milkv-duo256m-sd-v1.1.4.img.zip` | Duo 256M | TF 卡 |
| `milkv-duos-sd-v1.1.4.img.zip` | Duo S | TF 卡 |
| `milkv-duos-emmc-v1.1.4.zip` | Duo S（需 eMMC） | 板载 eMMC |
| `arduino-milkv-duo-sd-v1.1.4.img.zip` 等 4 个 | 三款板 | 同名规则，Arduino 预置镜像 |

### 烧录要点

- TF 卡镜像：解压后用 balenaEtcher / `dd` 写入，插卡上电即可；**默认开 ssh、默认开 USB-NCM 网卡，root 密码 `milkv`**
- eMMC 镜像：**不是** TF 卡镜像的写法。Duo S 要按住 Recovery 键、用 Type-C 数据线连电脑，再用 CVITEK 的 `usb_dl.exe`（Windows）或 `CviBurn` 工具从 USB 烧写；烧前务必拔掉 TF 卡
- Duo S 有 **ARM / RISC-V 启动切换开关**，固件与开关不一致时起不来；串口日志首字符 `C` 是从 RISC-V 启动、`B` 是从 ARM 启动
- Duo S 的 Type-C（USB-NCM）与 Type-A（USB HOST）**不能同时用**，靠 `/mnt/system/usb.sh` 软链接切换

---

## 5. 第三方镜像（社区维护，按板型分）

官方下载页有一份[第三方镜像表](https://milkv.io/docs/duo/getting-started/download)，这里按板型摊平，方便直接点。

### Duo（CV1800B，64 MB）

- [Fedora 41 镜像站](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo/images/latest/) —— Fedora-V Force 维护，跟着上游滚动
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) —— 镜像构建脚本，也能编 Duo 256M 的
- [Debian / Ubuntu 镜像构建器](https://github.com/logicethos/Milk-V_Duo_Linux2SD) —— 自己出镜像用这个
- [Arch Linux](https://community.milkv.io/t/arch-linux-on-milkv-duo-milkv-duo-arch-linux/329) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1) · [Debian 全量镜像](https://community.milkv.io/t/milkv-duo-duo-debian-full-7z-519m-download/862)
- [OpenWrt / VizOS](https://github.com/Pillar1989/VizOS) · [Zephyr（辅助核）](https://github.com/kinsamanka/milkv-zephyros) · [Yocto 层](https://github.com/kinsamanka/meta-milkv)
- [RT-Thread cvitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek)（[RISC-V RT-Thread 编程指南](https://riscv-rtthread-programming-manual.readthedocs.io/zh-cn/latest/)） · [ThreadX 移植](https://github.com/saicogn/ThreadX-to-RISC-V64)

### Duo 256M（SG2002）

- [Fedora 41 镜像站](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo256M/images/latest/)
- [Debian（Fishwaldo / sophgo-sg200x-debian）](https://github.com/Fishwaldo/sophgo-sg200x-debian/releases/tag/v1.2.0)
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) · [Arch Linux](https://community.milkv.io/t/debian-arch-linux-on-milkv-duo-256m-milkv-duo-256m-debian-arch-linux/1110) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1)

### Duo S（SG2000）

- [Fedora 41 镜像站](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/DuoS/images/latest/) —— 默认账号 `root` / 密码 `riscv`
- [Debian（scpcom）](https://github.com/scpcom/sophgo-sg200x-debian/releases) —— `root`/`rv` 与 `debian`/`rv` 两套账号
- [NuttX（lupyuen）](https://github.com/lupyuen/nuttx-sg2000/releases) —— 在 Duo S 上跑 NuttX 的现成镜像

---

## 6. SDK、工具链与示例

- SDK 源码：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [主机侧工具链](https://github.com/milkv-duo/host-tools)
- [duo-examples](https://github.com/milkv-duo/duo-examples) —— 官方 C/C++ 示例： [GPIO 闪灯](https://github.com/milkv-duo/duo-examples/tree/main/blink) · [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c) · [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) · [外设驱动操作指南（PDF）](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux)（引脚复用） · [duo-wiringx](https://github.com/milkv-duo/duo-wiringx)（wiringX 移植） · [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo)（LVGL framebuffer） · [duo-accessories](https://github.com/milkv-duo/accessories)（官方配件）
- Arduino：[已归档的官方核心库](https://github.com/milkv-duo/duo-arduino)（仓库已指向 [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)） · [Duo Arduino 示例](https://github.com/milkv-duo/duo-arduino-examples)
- SoC 侧工具：[CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x) · [TPU-MLIR 模型转换](https://github.com/milkv-duo/tpu-mlir)
- TDL（深度学习示例）：[CV180X / Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SG200X / Duo 256M & Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK V2 版 TDL 示例](https://github.com/milkv-duo/duo-tdl-examples) · [YOLO 部署](https://github.com/milkv-duo/duo-yolo-deployment)
- 多媒体：[duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples)

---

## 7. 官方组织、社区与交流

- [milkv-duo GitHub 组织](https://github.com/milkv-duo) —— 官方 SDK、示例、硬件文件都在这里
- [Milk-V 社区 Duo 分类](https://community.milkv.io/c/duo/5) —— 提问与经验贴的主场
- [Duo Module 01 评估板文档](https://milkv.io/docs/duo/getting-started/duo-module-01)
- 原 `forum.sophgo.com` 已不可访问（2026-10 实测连接失败），芯片侧资料改从 [sophgo-doc](https://github.com/sophgo/sophgo-doc/releases) 取

---

## 8. 视频：哔哩哔哩（50 支）

全部逐条核过页面存在（HTTP 200）且标题/简介确实指向 Duo 系列；播放量是 2026-10-31 的快照，只作热度参考。个别条目作者没写板卡型号，已在条目内注明。

**东东老师系列（eastdong）—— 最适合从零开始**

- 《零压力上手 RISC-V：东东老师带你玩转 milk-v duo》01. RVOS on Duo — [BV1vm421E7R6](https://www.bilibili.com/video/BV1vm421E7R6/) · 9578
- 02. RT-Thread on Duo — [BV1ym411z7Qo](https://www.bilibili.com/video/BV1ym411z7Qo/) · 3558
- 04. Camera 和 YOLOv5 图像识别 — [BV1mt421A7tL](https://www.bilibili.com/video/BV1mt421A7tL/) · 2972
- 05. TPU 使用 — [BV1Wi421Q7b4](https://www.bilibili.com/video/BV1Wi421Q7b4/) · 2171
- 06. 完结（补讲 Duo 256M 的新变化）— [BV1Fx4y1W7x9](https://www.bilibili.com/video/BV1Fx4y1W7x9/) · 2212

**苦芽科技 —— Duo S 官方课程的完整链路**

- 00. 认识 Milk-V Duo S — [BV1PNDoYeEpT](https://www.bilibili.com/video/BV1PNDoYeEpT/) · 2307
- 01. Windows 下安装及启动 — [BV1u3DYYGES7](https://www.bilibili.com/video/BV1u3DYYGES7/) · 376
- macOS 下安装及启动 — [BV1U5qqYUEAm](https://www.bilibili.com/video/BV1U5qqYUEAm/) · 233
- 02. SPI 演示 — [BV1vYqHYnE8G](https://www.bilibili.com/video/BV1vYqHYnE8G/) · 186

**入门与评测**

- 35 块带 TPU、1GHz 的 Linux 开发板，还玩啥树莓派（科学中国）— [BV19h4y1t7Ct](https://www.bilibili.com/video/BV19h4y1t7Ct/) · 1.9 万
- 镜像烧写教程：带 TPU 的 RISC-V Linux 板（斑梨电子）— [BV1uM4y1n763](https://www.bilibili.com/video/BV1uM4y1n763/) · 9098
- 能跑轻量 AI 的最便宜 RISC-V Linux 开发板？Duo 64M（捡个肥仔上战场）— [BV11w411j71u](https://www.bilibili.com/video/BV11w411j71u/) · 9365
- RISC-V 峰会现场 Duo 开箱（半导体都市隶人 Ayla）— [BV1oh4y1K724](https://www.bilibili.com/video/BV1oh4y1K724/) · 8415
- 野生的开发板性能再强又有何用，软件适配稀烂：Duo 256M 尝试 Arduino 彻底失败（沈洁 Eacc）— [BV1sZZHYdEPP](https://www.bilibili.com/video/BV1sZZHYdEPP/) · 8026 ← **负面评测，值得看**
- 35 元的 milkv-duo Linux 单片机还要啥自行车（开源社区的二掌柜）— [BV1tM4y1Y7kh](https://www.bilibili.com/video/BV1tM4y1Y7kh/) · 2792
- 学习 RISC-V 能跑 Debian & Linux 的最便宜开发板之一（蘭雅 sRGB）— [BV1XQ4y1E7Tj](https://www.bilibili.com/video/BV1XQ4y1E7Tj/) · 3054
- 好玩！RISC-V duo256M 开发板测玩（蘭雅 sRGB）— [BV1Zw411V7bK](https://www.bilibili.com/video/BV1Zw411V7bK/) · 2257
- 麻雀虽小五脏俱全：超高性价比开发板 Milk-V Duo S（qinyunti）— [BV1hyKmzJEw5](https://www.bilibili.com/video/BV1hyKmzJEw5/) · 664

**环境搭建与烧录**

- Linux 下开发环境搭建（future 待续）— [BV1B8411m7jR](https://www.bilibili.com/video/BV1B8411m7jR/) · 3192
- 烧写 Linux 系统 + USB 虚拟 RNDIS 网卡登录（蘭雅 sRGB）— [BV1G14y1k7V4](https://www.bilibili.com/video/BV1G14y1k7V4/) · 1062
- Duo-debian 初体验（蘭雅 sRGB）— [BV11c411o76T](https://www.bilibili.com/video/BV11c411o76T/) · 3416
- Duo 简介和开发环境搭建（谁说现在是冬天呢）— [BV1PF411S7To](https://www.bilibili.com/video/BV1PF411S7To/) · 1959
- Buildroot SDK 简介和编译镜像的方法（谁说现在是冬天呢）— [BV1xc411s7qk](https://www.bilibili.com/video/BV1xc411s7qk/) · 462
- 安装 Hyper-V & 配置 Docker 开发环境（_1dentity）— [BV1nC4y117WS](https://www.bilibili.com/video/BV1nC4y117WS/) · 1826

**外设、显示与双核**

- LVGL 库实战教程 — 刘文涛（群芯闪耀），lazyparser 频道 — [BV1Mp421m7qJ](https://www.bilibili.com/video/BV1Mp421m7qJ/) · 966
- 通过 SPI 驱动 ST7789V 跑 LVGL（谁说现在是冬天呢）— [BV1gLeueWEWr](https://www.bilibili.com/video/BV1gLeueWEWr/) · 2239
- Duo 256M 基于 TinyDRM 驱动 ST7796s 4.0 寸屏并移植 LVGL 8.3（二掌柜）— [BV1Tv421k71W](https://www.bilibili.com/video/BV1Tv421k71W/) · 1230
- USB & Ethernet IO-Board 简介和使用方法（谁说现在是冬天呢）— [BV1Ga4y1Z7oM](https://www.bilibili.com/video/BV1Ga4y1Z7oM/) · 1096
- 通过大核控制小核点亮 LED（谁说现在是冬天呢）— [BV1nH4y1y7CM](https://www.bilibili.com/video/BV1nH4y1y7CM/) · 1057
- 用 Duo 驱动 DF9GMS 微型舵机（谁说现在是冬天呢）— [BV1Dj411E7yD](https://www.bilibili.com/video/BV1Dj411E7yD/) · 571
- Duo S 硬件解码 MP4 并在 LCD 上播放（一只御坂美琴）— [BV1ktvseWEhr](https://www.bilibili.com/video/BV1ktvseWEhr/) · 519

**系统移植**

- 在 Duo 上运行 ThreadX（谁说现在是冬天呢）— [BV1yi421C7SK](https://www.bilibili.com/video/BV1yi421C7SK/) · 419
- 在小核上运行 Zephyr OS（谁说现在是冬天呢）— [BV1uK421Y7x9](https://www.bilibili.com/video/BV1uK421Y7x9/) · 435
- 在 Duo 256M 上运行 Arch Linux（谁说现在是冬天呢）— [BV1j8yyYTEp2](https://www.bilibili.com/video/BV1j8yyYTEp2/) · 1274
- 在 Duo S 上启动 NuttX（悲伤的黑山羊）— [BV1RMUeYjELe](https://www.bilibili.com/video/BV1RMUeYjELe/) · 75
- 罗君：Duo 的 UniProton 适配（PLCT 内部报告）（lazyparser）— [BV1RD421G773](https://www.bilibili.com/video/BV1RD421G773/) · 903
- Duo S 启动！（谁说现在是冬天呢）— [BV1Bm421N72y](https://www.bilibili.com/video/BV1Bm421N72y/) · 564
- 使用 Wi-Fi 连接 Duo S（谁说现在是冬天呢）— [BV11r421T7Sk](https://www.bilibili.com/video/BV11r421T7Sk/) · 318
- 在 Duo S 上部署 Caddy 服务器（谁说现在是冬天呢）— [BV1poBzYQEoC](https://www.bilibili.com/video/BV1poBzYQEoC/) · 214
- Duo 256M 部署相册文件管理器和博客笔记（蘭雅 sRGB）— [BV1cC4y1e7uk](https://www.bilibili.com/video/BV1cC4y1e7uk/) · 1455
- GameOS 开发日常：自制系统上跑 Doom、用「小电视」按 BV 号播放 B 站视频（我的大可乐呢；作者未标板卡型号）— [BV1iZx46BEV7](https://www.bilibili.com/video/BV1iZx46BEV7/) · 38

**AI / 视觉**

- Duo 256M 锁头测试：官方脚本跑人脸检测并拉流到电脑（Judehahh）— [BV1w4421A7A2](https://www.bilibili.com/video/BV1w4421A7A2/) · 3.6 万
- 基于 Duo 和 YOLOv5 的目标检测（谁说现在是冬天呢）— [BV1iG41197qa](https://www.bilibili.com/video/BV1iG41197qa/) · 1211
- 基于 TDL SDK 实现 YOLOv5 目标检测（谁说现在是冬天呢）— [BV1Vw4m1U71C](https://www.bilibili.com/video/BV1Vw4m1U71C/) · 446
- YOLOv8 目标检测（谁说现在是冬天呢）— [BV1AWqUYGEaS](https://www.bilibili.com/video/BV1AWqUYGEaS/) · 269
- 测试通过 VLC 显示 CAM-GC2083 摄像头画面（谁说现在是冬天呢）— [BV188411v7tc](https://www.bilibili.com/video/BV188411v7tc/) · 1159
- Duo S 运行故事机 baby llama2（谁说现在是冬天呢）— [BV1dn4y197UW](https://www.bilibili.com/video/BV1dn4y197UW/) · 621
- Duo S 上用 TDL SDK 部署人脸检测（谁说现在是冬天呢）— [BV1AM4m1m7fe](https://www.bilibili.com/video/BV1AM4m1m7fe/) · 522
- YOLO 实战：车牌识别效果展示（谁说现在是冬天呢）— [BV1uYAHerEbL](https://www.bilibili.com/video/BV1uYAHerEbL/) · 1272
- 【软硬件开源】TideSense双目VIO（单三拍）— [BV1EcnG6XESF](https://www.bilibili.com/video/BV1EcnG6XESF/) · 15376

---

## 9. 视频：YouTube（37 支）

国外站点，走代理才能打开；同样逐条核过页面存在且内容真的涉及 Duo。

**评测与上手**

- Platima Tinkers — Testing out the Milk-V Duo: the new $9 RISC-V eSBC that runs Linux — [YqUtGk0DHbQ](https://www.youtube.com/watch?v=YqUtGk0DHbQ) · Duo
- Platima Tinkers — Duo 256M: the SBC stick that can dual boot RISC-V and ARM — [wmmTYOXtESg](https://www.youtube.com/watch?v=wmmTYOXtESg) · Duo 256M
- Platima Tinkers — Duo 256 running Arduino code and Linux at the same time — [QOdZkn0MmYk](https://www.youtube.com/watch?v=QOdZkn0MmYk) · Duo 256M
- Platima Tinkers — Duo S: dual boot RISC-V or ARM, dual camera, Wi-Fi and RTOS — [k98xevAmmp8](https://www.youtube.com/watch?v=k98xevAmmp8) · Duo S
- Platima Tinkers — This $9 board solves the Duo's biggest problem (camera options) — [KivoIjkQZVY](https://www.youtube.com/watch?v=KivoIjkQZVY) · Duo
- Platima Tinkers — SBC showdown: Milk-V Duo vs Luckfox Pico — [0R1MH5Gcmmo](https://www.youtube.com/watch?v=0R1MH5Gcmmo) · Duo
- Andreas Spiess — (485) $8 MilkV Duo: Arduino on one core and Linux on the other — [SeExddxWdNs](https://www.youtube.com/watch?v=SeExddxWdNs) · Duo
- Biblioman09 — Review Milk-V Duo S — [GiNb60_oEDk](https://www.youtube.com/watch?v=GiNb60_oEDk) · Duo S
- Biblioman09 — Review Milk-V Duo — [4pejiKvLW_U](https://www.youtube.com/watch?v=4pejiKvLW_U) · Duo
- Technically Unsure — Unleashing the $10 tech revolution: Duo S rocks the Linux world — [rby8a_DsSYc](https://www.youtube.com/watch?v=rby8a_DsSYc) · Duo S
- StableCore PC — Duo 256M: a RISC-V mini SBC — [c5FCJgvBkN8](https://www.youtube.com/watch?v=c5FCJgvBkN8) · Duo 256M
- Hotel Foxtrot Tango Echo — Extremely small Linux computer, 1 GHz Duo 256M — [2MMSqUrZ0kk](https://www.youtube.com/watch?v=2MMSqUrZ0kk) · Duo 256M

**入门、烧录与网络**

- R&V world — What? Flash Milk-V Duo S within 2 minutes! — [N9xfqDrpNTU](https://www.youtube.com/watch?v=N9xfqDrpNTU) · Duo S
- Thao Le Thach — Getting started, SDK build, IDE config for C, LED blinking with Zig — [Xh_NMALphgs](https://www.youtube.com/watch?v=Xh_NMALphgs) · Duo
- Technology Kinestronics — Build an embedded Linux computer with Milk-V Duo — [UYgq4qOaZnk](https://www.youtube.com/watch?v=UYgq4qOaZnk) · Duo
- CanHobby Explorations — Milk-V Duo for Linux users — [g-yl8UscCbI](https://www.youtube.com/watch?v=g-yl8UscCbI) · Duo
- CanHobby Explorations — Mastering wiringX on Milk-V Duo — [lolPJnM13Ys](https://www.youtube.com/watch?v=lolPJnM13Ys) · Duo
- CanHobby Explorations — MilkV Duo Linux bash scripting — [UT-4jspCWwU](https://www.youtube.com/watch?v=UT-4jspCWwU) · Duo
- spotpear — Image burning tutorial, $9.9 Linux board Duo RISC-V 1 GHz TPU — [N-t344wXcJU](https://www.youtube.com/watch?v=N-t344wXcJU) · Duo
- spotpear — Enter terminal via UART tutorial — [j-X0wyDSirw](https://www.youtube.com/watch?v=j-X0wyDSirw) · Duo
- spotpear — GPIO LED tutorial — [YJ_iXxWPhbo](https://www.youtube.com/watch?v=YJ_iXxWPhbo) · Duo
- spotpear — Linux kernel compilation — [_KwRw36hA4U](https://www.youtube.com/watch?v=_KwRw36hA4U) · Duo
- 蘭雅 sRGB — Burning Linux and USB virtual RNDIS network card — [fCE62HeDFP8](https://www.youtube.com/watch?v=fCE62HeDFP8) · Duo
- 蘭雅 sRGB — Build the compilation environment, Hello World and blink LED — [Fe7IWqkbFFU](https://www.youtube.com/watch?v=Fe7IWqkbFFU) · Duo

**外设与 AI**

- Anton Maltsev — Is it good for computer vision? How to start a neural network on it — [dkIVDOd_Fa4](https://www.youtube.com/watch?v=dkIVDOd_Fa4) · Duo
- Mark Birss — Milk-V Duo USB input ST7789 240×240 SPI display — [Swo-zJ6brQI](https://www.youtube.com/watch?v=Swo-zJ6brQI) · Duo
- Sonny Cruz — I²C demo, source in the description — [85uglOz48Pg](https://www.youtube.com/watch?v=85uglOz48Pg) · Duo
- Sonny Cruz — RC servo demo using PWM — [1u2LZJWPtNU](https://www.youtube.com/watch?v=1u2LZJWPtNU) · Duo
- Leigh — Duo + CAM-GC2083: fix RTSP streaming to VLC — [PjiUDsoWCvo](https://www.youtube.com/watch?v=PjiUDsoWCvo) · Duo
- Muhammad Yunus — YOLOX inference on Duo S using TDL SDK + VPSS — [wzUTGK4TuqA](https://www.youtube.com/watch?v=wzUTGK4TuqA) · Duo S

**系统移植与整机项目**

- Muhammad Yunus — RT-Thread on Duo S: the best RTOS for cheap RISC-V? — [WjWM5YoAq-c](https://www.youtube.com/watch?v=WjWM5YoAq-c) · Duo S
- RISC-V Developers — S1E2 Enjoy RISC-V with Milk-V Duo: RT-Thread — [B7EXWE6l9xE](https://www.youtube.com/watch?v=B7EXWE6l9xE) · Duo
- Chris McDonough — NixOS 71: NixOS on RISC-V (Milk-V Duo / Duo 256M) — [-ydXjEWUlGE](https://www.youtube.com/watch?v=-ydXjEWUlGE) · Duo 系列
- admin ka — Running Ubuntu glibc 24.04.4 on the Duo 256M — [0Dqbdtjt8Ro](https://www.youtube.com/watch?v=0Dqbdtjt8Ro) · Duo 256M
- 福田重夫 — Running Linux on the Duo 256M (RISC-V + ARM) — [Ga3HX-d8GHQ](https://www.youtube.com/watch?v=Ga3HX-d8GHQ) · Duo 256M
- Nch-Lab — Milk-V Duo 256M を買ったので Linux を動かしてみる — [tcAqYCwbqeU](https://www.youtube.com/watch?v=tcAqYCwbqeU) · Duo 256M
- Mark Birss — Duo 256 CyberDeck LoRa communicator (TLMVC) — [9qOJ3fKwfC0](https://www.youtube.com/watch?v=9qOJ3fKwfC0) · Duo 256M

---

## 10. GitHub 开源项目

按用途分类。star 数与最后提交日期是 2026-10-31 的快照，会变；带「官方」的是 milkv-duo 组织下的仓库。

**官方 SDK、固件与工具**

- [duo-buildroot-sdk](https://github.com/milkv-duo/duo-buildroot-sdk) — 官方 Buildroot SDK V1（Duo/CV1800B）· 495★
- [duo-buildroot-sdk-v2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) — 官方 SDK V2（Duo 256M / Duo S，SG200x）· 154★
- [duo-examples](https://github.com/milkv-duo/duo-examples) — 官方 C/C++ 外设示例 · 159★
- [duo-sdk](https://github.com/milkv-duo/duo-sdk) — 宿主机侧交叉编译 SDK（duo-app-sdk）· 5★
- [host-tools](https://github.com/milkv-duo/host-tools) — 预编译主机 gcc 工具链 · 9★
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) — 引脚复用配置工具 · 7★
- [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) — wiringX 的 Duo 移植 · 11★
- [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples) — 多媒体链路示例 · 6★
- [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) — LVGL on framebuffer · 10★
- [duo-arduino](https://github.com/milkv-duo/duo-arduino) — 官方 Arduino 支持（已归档，指向 [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)）· 20★
- [duo-arduino-examples](https://github.com/milkv-duo/duo-arduino-examples) — Arduino 示例
- [duo-tdl-examples](https://github.com/milkv-duo/duo-tdl-examples) — SDK V2 的 TDL 样例 · 13★
- [cvitek-tdl-sdk-sg200x](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) — SG200x TDL-SDK 样例 · 30★
- [cvitek-tdl-sdk-cv180x](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) — CV180x TDL-SDK 样例
- [tpu-sdk-sg200x](https://github.com/milkv-duo/tpu-sdk-sg200x) — SG200x TPU SDK · 5★
- [tpu-sdk-cv180x](https://github.com/milkv-duo/tpu-sdk-cv180x) — CV180x TPU SDK
- [tpu-mlir](https://github.com/milkv-duo/tpu-mlir) — TPU-MLIR 模型转换 · 9★
- [duo-yolo-deployment](https://github.com/milkv-duo/duo-yolo-deployment) — YOLO 部署示例
- [milkv-duo-linux](https://github.com/milkv-duo/milkv-duo-linux) — 官方内核树 · 1★
- [milkv-duo-u-boot](https://github.com/milkv-duo/milkv-duo-u-boot) — 官方 U-Boot 树 · 4★
- [milkv-duo-opensbi](https://github.com/milkv-duo/milkv-duo-opensbi) — 官方 OpenSBI 移植 · 2★
- [milkv-duo-smallcore-freertos](https://github.com/milkv-duo/milkv-duo-smallcore-freertos) — 小核 C906 跑 FreeRTOS · 17★
- [duo-8051](https://github.com/milkv-duo/duo-8051) — 内置 8051 核示例 · 8★

**官方文档与硬件资料**

- [duo-files](https://github.com/milkv-duo/duo-files) — 原理图、数据手册、机械图总库 · 203★
- [accessories](https://github.com/milkv-duo/accessories) — 官方配件资料 · 14★
- [milkv.io](https://github.com/milk-v/milkv.io) — 官网与文档站源码 · 4★
- [sophgo-doc](https://github.com/sophgo/sophgo-doc) — 上游芯片文档发布口
- [datasheet-en](https://github.com/taspenwall/datasheet-en) — SG2002 数据手册英译 · 5★
- [riscv-rtthread-programming-manual](https://github.com/flyingcys/riscv-rtthread-programming-manual) — 《RISC-V 编程指南：基于 RT-Thread 与 Milk-V Duo》配套代码 · 10★
- [MilkV-Duo-Resources](https://github.com/robtech21/MilkV-Duo-Resources) — 资源合集
- [johandevlabs/milk-v-duo-s-notes](https://github.com/johandevlabs/milk-v-duo-s-notes) — Duo S 折腾笔记 · 5★
- [Mirrorium227/MilkvDuo_Basic](https://github.com/Mirrorium227/MilkvDuo_Basic) — CV1800B 排障与例程
- [imagineeeinc/things-on-milkv-duo](https://github.com/imagineeeinc/things-on-milkv-duo) — 用 Nim 玩 Duo

**引导与固件**

- [u-boot/u-boot](https://github.com/u-boot/u-boot) — 主线已含 `board/sophgo/milkv_duo` · 5309★
- [sg_boot](https://github.com/platform-system-interface/sg_boot) — Rust 写的 CV1800B/SG200x 引导器 · 12★
- [gtxzsxxk/milkv-duo-firmware-fsbl](https://github.com/gtxzsxxk/milkv-duo-firmware-fsbl) — FSBL 实现 · 6★
- [Taumille/uboot-milkv](https://github.com/Taumille/uboot-milkv) — 已消失的官方 u-boot 仓库的社区 fork

**发行版与系统镜像**

- [armbian/build](https://github.com/armbian/build) — 已含 `milkv-duos-riscv` / `milkv-duos-arm` 板型 · 5499★
- [Fishwaldo/sophgo-sg200x-debian](https://github.com/Fishwaldo/sophgo-sg200x-debian) — 最活跃的 SG200x Debian 构建 · 219★
- [ambraglow/milkv-duo-ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) — Duo Ubuntu · 68★
- [olivaw448/milkv-duo-s-512mb-debian](https://github.com/olivaw448/milkv-duo-s-512mb-debian) — Duo S 512MB Debian（含 WiFi/蓝牙/USB host/摄像头）· 11★
- [eznix86/milkv-duo-s-alpine-linux](https://github.com/eznix86/milkv-duo-s-alpine-linux) — Duo S Alpine · 9★
- [CrocNet/duo-docker-builder](https://github.com/CrocNet/duo-docker-builder) — Docker 构建 Ubuntu 镜像 · 9★
- [logicethos/Milk-V_Duo_Linux2SD](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — 构建并直接写卡 · 21★
- [RawFish69/ubuntu-milkv-duos](https://github.com/RawFish69/ubuntu-milkv-duos) — Duo S Ubuntu 22.04
- [draftbottle/Milkv-duo-openwrt](https://github.com/draftbottle/Milkv-duo-openwrt) — 基于 VizOS 的 OpenWrt
- [Pillar1989/VizOS](https://github.com/Pillar1989/VizOS) — OpenWrt / VizOS 项目
- [georgewhewell/nixos-nanokvm](https://github.com/georgewhewell/nixos-nanokvm) — SG2000/SG2002 的 NixOS 配置
- [kinsamanka/meta-milkv](https://github.com/kinsamanka/meta-milkv) — Yocto / OpenEmbedded 层

**RTOS 与裸机**

- [RT-Thread/rt-thread](https://github.com/RT-Thread/rt-thread) — `bsp/cvitek` 含 milkv-duo / duo256m / duos · 12318★
- [lupyuen/nuttx-sg2000](https://github.com/lupyuen/nuttx-sg2000) — Duo S 上的 NuttX · 45★
- [kinsamanka/milkv-zephyros](https://github.com/kinsamanka/milkv-zephyros) — 小核 Zephyr · 35★
- [saicogn/ThreadX-to-RISC-V64](https://github.com/saicogn/ThreadX-to-RISC-V64) — ThreadX 移植 · 8★
- [Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK](https://github.com/Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK) — 不用 SDK 的双核裸机 · 11★
- [zuki/xv6-milkv-duo](https://github.com/zuki/xv6-milkv-duo) — xv6 on Duo · 7★
- [jiegegena/milkv-sg2002-xv6](https://github.com/jiegegena/milkv-sg2002-xv6) — xv6 on SG2002
- [Lam920/xv6-cv1800b](https://github.com/Lam920/xv6-cv1800b) — xv6 on CV1800B
- [rota1001/milkv-baremetal-toolkit](https://github.com/rota1001/milkv-baremetal-toolkit) — 一键生成裸机镜像 · 8★
- [PeterForth/MILKV-FORTH](https://github.com/PeterForth/MILKV-FORTH) — Duo 上的 Forth · 8★
- [xingrz/milkv-duo-zephyr-mailbox-example](https://github.com/xingrz/milkv-duo-zephyr-mailbox-example) — Zephyr 与 Linux 的 mailbox 通信
- [DivByDiamond/OnyxOS](https://github.com/DivByDiamond/OnyxOS) — Rust 写的 RISC-V 单体内核（整机约 272 KB，含 C++ 引导器与自举 C 编译器），内核带 SG2000 平台驱动，目标板包括 Duo S · 0★

**工具链与构建环境**

- [aidancrowther/Milk-V-Duo-Docker-Compile](https://github.com/aidancrowther/Milk-V-Duo-Docker-Compile) — 预装工具链的 Docker 镜像 · 24★
- [Tosainu/docker-milkv-duo-linux](https://github.com/Tosainu/docker-milkv-duo-linux) — 容器化构建 Linux
- [boberace/milkv_duo_dc](https://github.com/boberace/milkv_duo_dc) — VS Code Dev Container
- [kitnerboy/milkv-duo-buildroot](https://github.com/kitnerboy/milkv-duo-buildroot) — 主线风格 Buildroot BSP

**驱动与外设**

- [hexdump0815/linux-cvitek-cv18xx-kernel](https://github.com/hexdump0815/linux-cvitek-cv18xx-kernel) — 社区内核树（多个镜像的内核来源）
- [ret7020/CVI_HW_OpenCV](https://github.com/ret7020/CVI_HW_OpenCV) — 用 NPU 加速的 OpenCV 移植 · 7★
- [pavelanni/gpiod-milkvduo](https://github.com/pavelanni/gpiod-milkvduo) — libgpiod 用法 · 3★
- [Satharus/I2C-WiringX-Milk-V](https://github.com/Satharus/I2C-WiringX-Milk-V) — wiringX 操作 I²C · 2★
- [KuLvo/milk-v_duo_oled_driver](https://github.com/KuLvo/milk-v_duo_oled_driver) — 0.96 寸 OLED 驱动 · 3★
- [queenkjuul/aic8800-milkv-duos](https://github.com/queenkjuul/aic8800-milkv-duos) — AIC8800 WiFi+BT 适配
- [GrootLiu/milkv-duo-rtl8723du](https://github.com/GrootLiu/milkv-duo-rtl8723du) — RTL8723DU WiFi 移植
- [Tactical-TV-Remote/infrared_milkv](https://github.com/Tactical-TV-Remote/infrared_milkv) — 红外收发（Rust）
- [harshareddy1611/milkv-duo-s-baremetal-drivers](https://github.com/harshareddy1611/milkv-duo-s-baremetal-drivers) — Duo S 裸机 GPIO/UART
- [wanghengZzz/Milkv-Duo-FreeRTOS-DMA](https://github.com/wanghengZzz/Milkv-Duo-FreeRTOS-DMA) — FreeRTOS DMA HAL

**项目实战**
- [tidesense](https://github.com/HumpbackLab/tidesense) — 基于 SG2002 的双目视觉惯性里程计（自研板，不是 Duo 256M）：OV9281 全局快门双目 + SC7U22 IMU，SchurVINS 做 20 Hz 视觉校正 / 200 Hz 预测，附 OpenVINS 对比、标定与数据集工具；VIO 跑在 Cortex-A53 上，纯 SD 启动。硬件按 CC BY-NC-SA 4.0 开源（链接见仓库 README）· 142★

- [pavelanni/milkv-duo-experiments](https://github.com/pavelanni/milkv-duo-experiments) — Go 写的实验集 · 27★
- [driver1998/DiscEmu](https://github.com/driver1998/DiscEmu) — 用 Duo 做 CD-ROM 模拟器 · 11★
- [0x1iii1ii/Pwn-V-Duo](https://github.com/0x1iii1ii/Pwn-V-Duo) — PPPwn 漏洞利用移植 · 6★
- [aceraoc/MilkV-Duo_TPU](https://github.com/aceraoc/MilkV-Duo_TPU) — TPU 推理实例 · 8★
- [xmdjy/milkv-car](https://github.com/xmdjy/milkv-car) — 基于 Duo 的智能小车
- [Arielfoever/milkv-duo-yolo11](https://github.com/Arielfoever/milkv-duo-yolo11) — YOLO11 部署
- [Basicname/SG200x_GC2083_Yolov8_11](https://github.com/Basicname/SG200x_GC2083_Yolov8_11) — 单文件部署 YOLOv8/11 + GC2083
- [chius-me/globi-v](https://github.com/chius-me/globi-v) — Duo S 上的视障辅助视觉系统
- [f3jry/milkv-duo-xmrsigner](https://github.com/f3jry/milkv-duo-xmrsigner) — Monero 冷钱包移植到 Duo
- [sdwood68/MilkV_Duo_S_Camera](https://github.com/sdwood68/MilkV_Duo_S_Camera) — 可接 Frigate / Home Assistant 的摄像头节点
- [ar90n/ptp-server-milkv-duos](https://github.com/ar90n/ptp-server-milkv-duos) — PTP 主时钟服务器
- [avalitan/MilkV-Duo-S-NTP-UPS-Server](https://github.com/avalitan/MilkV-Duo-S-NTP-UPS-Server) — NTP + NUT UPS 监控
- [vojinvukcevic/boot-time-optimization-milkv](https://github.com/vojinvukcevic/boot-time-optimization-milkv) — 冷启动 14.1 s → 3.2 s 的完整记录
- [manio/milkv-duos-hwcodec-test](https://github.com/manio/milkv-duos-hwcodec-test) — Duo S 上最小的硬件 H.264 编解码自检：直接调 cvi_mpi 的 libsys / libvenc / libvdec，跳过 VI/VPSS/VO，编码合成帧再解码回来比对 PSNR（默认 1280×720、60 帧），在 Buildroot 镜像（内核 5.10.4）上实测 · 0★
- [Tom-game-project/MilkV-DuoS-rust-tpu-example](https://github.com/Tom-game-project/MilkV-DuoS-rust-tpu-example) — Duo S 上用 Rust 跑 TPU 矩阵乘法：Makefile 自动拉 host-tools、tpu-sdk-sg200x 与 tpu-mlir，把 ONNX 编成 .cvimodel，Rust 交叉编译到 riscv64 musl 后 scp 部署 · 0★

**硬件与外壳**

- [iyegoroff/milkv-duo-s-case](https://github.com/iyegoroff/milkv-duo-s-case) — Duo S 参数化 3D 打印外壳 · 12★
- [pauleffect90/MilkVDuoKicad](https://github.com/pauleffect90/MilkVDuoKicad) — KiCad 符号与封装 · 4★
- [Tosainu/milkv-duo-iob](https://github.com/Tosainu/milkv-duo-iob) — IO 扩展板设计文件

---

## 11. Gitee 项目与中文教程

**Gitee（19 个）**

- [tinylab/milkv-buildroot](https://gitee.com/tinylab/milkv-buildroot) — 泰晓社区镜像的 Buildroot 构建工程
- [tinylab/duo-buildroot-sdk](https://gitee.com/tinylab/duo-buildroot-sdk) — 官方 V1 SDK 国内镜像
- [tinylab/duo-examples](https://gitee.com/tinylab/duo-examples) — 官方示例国内镜像
- [tinylab/i2c-lsm6dsr](https://gitee.com/tinylab/i2c-lsm6dsr) — I²C LSM6DSR 传感器示例
- [weilinfox/pinpong-milkv-duo-doc](https://gitee.com/weilinfox/pinpong-milkv-duo-doc) — 在 Duo 上跑 pinpong · 3★
- [lan-ruixin/duo-buildroot-sdk](https://gitee.com/lan-ruixin/duo-buildroot-sdk) — 个人维护的 V1 分支，补了中文编译说明
- [lan-ruixin/milkv-duo-rtl8723du](https://gitee.com/lan-ruixin/milkv-duo-rtl8723du) — RTL8723DU WiFi/蓝牙适配
- [qhw136/milkv_duo_sdk](https://gitee.com/qhw136/milkv_duo_sdk) — 补 LCD/触摸/WiFi/蓝牙的增强 SDK
- [zhidao101/Milkv_duo_Ubuntu_image](https://gitee.com/zhidao101/Milkv_duo_Ubuntu_image) — 256M 与 512MB 的 Ubuntu 22.04 镜像
- [tiberium/duosdk2yocto](https://gitee.com/tiberium/duosdk2yocto) — 把 SDK 改造成 Yocto 构建
- [tiberium/meta-milkv-duo-sdk](https://gitee.com/tiberium/meta-milkv-duo-sdk) — 配套 meta layer
- [fixxer2020/duo-multimedia-examples](https://gitee.com/fixxer2020/duo-multimedia-examples) — 多媒体示例镜像
- [dongshan-community/DongShanPiExtboard](https://gitee.com/dongshan-community/DongShanPiExtboard) — Duo 256M 的 mini-ITX 扩展板
- [linux-proj/Milkv-duo_Cross_Compile_software](https://gitee.com/linux-proj/Milkv-duo_Cross_Compile_software) — 预编译交叉编译依赖包
- [atari/opencv-mobile](https://gitee.com/atari/opencv-mobile) — opencv-mobile 同步仓（riscv64-musl、硬件 JPG 解码、MIPI CSI）· 5★
- [unicornx/riscv-operating-system-mooc](https://gitee.com/unicornx/riscv-operating-system-mooc) — RVOS 课程代码（已移植到 Duo）· 541★
- [openeuler/UniProton](https://gitee.com/openeuler/UniProton) — 含 `demos/milkv-duo` 的大小核示例 · 73★（仓库已迁往 AtomGit）
- [k0059/duo-buildroot-sdk-v2](https://gitee.com/k0059/duo-buildroot-sdk-v2) — SDK V2 的 sg200x-evb 分支
- [xju_kjc/duo-buildroot-sdk](https://gitee.com/xju_kjc/duo-buildroot-sdk) — V1 SDK 完整镜像（中/日/英 README）

**中文教程与文章（22 篇）**

- 博客园 [milkv-duo 启动流程分析：手动构建 fip.bin [1/2]](https://www.cnblogs.com/maomaotou-thu/p/17765721.html) · [2/2](https://www.cnblogs.com/maomaotou-thu/p/17766024.html) · [手动构建 boot.sd](https://www.cnblogs.com/maomaotou-thu/p/17767315.html) — 想搞懂启动链必读
- 博客园 [Milk-V Duo S 使用报告](https://www.cnblogs.com/BiaoZyx/p/18956632) — 开箱到外设试用，含踩坑
- 博客园 [大作业：milkv-duo 小车设计工作日志](https://www.cnblogs.com/Cybersites/p/18859275)
- 博客园 [小核引导 RTOS —— RISC-V C906](https://www.cnblogs.com/gaoyang3513/articles/18854508)
- 博客园 [集成构建流程之根文件系统 Buildroot](https://www.cnblogs.com/gaoyang3513/p/18854502) · [网络升级固件](https://www.cnblogs.com/gaoyang3513/p/18854509) · [以太网使用与配置](https://www.cnblogs.com/gaoyang3513/p/18854518) · [Docker 开发环境搭建](https://www.cnblogs.com/gaoyang3513/p/18854511)
- 博客园 [milkv duo 256M 使用 Debian 系统](https://www.cnblogs.com/GrootStudy/p/18225934)
- 博客园 [milkV-duo 的 Linux 开发环境搭建](https://www.cnblogs.com/yzh0526/p/18098794)
- 博客园 [milk-v duo 开机引导进入 rust 程序](https://www.cnblogs.com/longxiangam/p/19640491)
- 掘金 [milkv-duo 开发环境搭建 & 烧录](https://juejin.cn/post/7269416466314821668) · [打包 SDK 时遇到的问题及解决](https://juejin.cn/post/7269417409370505235) · [小奶板点灯 & sensor bring up](https://juejin.cn/post/7269644295588659261) · [image burn](https://juejin.cn/post/7269424598260334648) · [milkv 256duo 初品](https://juejin.cn/post/7355829021311238182)
- B 站专栏 [Milk-v Duo：35 块带 TPU 1GHz 的 Linux 开发板](https://www.bilibili.com/read/cv24253633) · [Linux 与 RTOS 双核开发实践](https://www.bilibili.com/read/cv27449966) · [Duo S 部署 PicoClaw 完整教程](https://www.bilibili.com/read/cv46804507) · [Ubuntu 20.04 详细编译环境搭建指南](https://www.bilibili.com/read/cv24743710)

> **CSDN 与知乎暂缺**：这两个站在本机网络下返回 521 / 403（浏览器直访同样被拦），无法通过「页面确实存在」的校验，因此不收未核实的链接。RT-Thread 问答社区 `club.rt-thread.org` 同样被 WAF 拦截。等能直连时再补。

---

## 12. 这个索引怎么维护

- 每天 14:00 自动跑一次全网增量扫描（官方 releases、文档站新页、新视频、新仓库），有变化就提交更新
- 只收**能打开**的链接；每次更新跑一遍全量链接检查，死链下线或换新地址
- 视频要求确实用了 Duo 系列；项目要求仓库里真的支持这些板子（不是只提一句）
- 收录不代表背书。第三方镜像与项目的安全性、许可证、维护状态请自己判断
- 发现漏掉的资源，欢迎提 issue 或 PR；提 PR 时请按现有分节放，并注明适用板型（Duo / Duo 256M / Duo S）

[返回语言索引](README.md)
