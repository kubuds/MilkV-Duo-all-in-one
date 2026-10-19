# Milk-V Duo、Duo 256M 与 Duo S 资源指南

本页汇集 Milk-V Duo 系列的官方文档、固件、源代码、硬件资料、教程和社区项目。网络资源不可能保证绝对完整，欢迎补充或纠正失效链接。

> **使用前请确认兼容性。** 原版 Duo 使用 CV1800B，内存为 64 MB；Duo 256M 使用 SG2002，内存为 256 MB；Duo S 使用 SG2000，内存为 512 MB。三款开发板的硬件和软件目标并不相同。官方概览已将原版 Duo 标记为停产（EOL）。第三方系统和镜像由社区维护，不一定经过测试。

## 官方产品与文档

- [Duo 系列概览与规格](https://milkv.io/docs/duo/overview) — 开发板对比、功能和生命周期说明。
- 开发板指南：[Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos)。
- 入门：[启动系统](https://milkv.io/docs/duo/getting-started/boot) · [镜像下载与选择](https://milkv.io/docs/duo/getting-started/download) · [Buildroot SDK 指南](https://milkv.io/docs/duo/getting-started/buildroot-sdk)。
- 产品页面：[Duo](https://milkv.io/duo) · [Duo 256M](https://milkv.io/duo256m) · [Duo S](https://milkv.io/duos)。
- [官方文档源代码](https://github.com/milk-v/milkv.io) — 可在此提交修正或翻译。

## 固件、SDK 与工具链

- [官方镜像目录及兼容性说明](https://milkv.io/docs/duo/getting-started/download)。
- 官方固件发布页：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk/releases) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)。
- SDK 源码：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [主机工具链](https://github.com/milkv-duo/host-tools)。
- 官方下载指南建议 64 MB 的 Duo 使用 V1 镜像，Duo 256M 和 Duo S 使用 V2。请务必核对发行说明和构建目标名称。
- [官方 C/C++ 示例及交叉编译工具链设置](https://github.com/milkv-duo/duo-examples)，包括 [GPIO 闪灯](https://github.com/milkv-duo/duo-examples/tree/main/blink)、[I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c)、[SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) 和[外设指南（PDF）](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)。

## 硬件、外设与应用开发

- [官方开发板文件、原理图、数据手册和机械图纸](https://github.com/milkv-duo/duo-files)。
- 开发板原理图：[Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)。
- [Sophgo 芯片数据手册及文档](https://github.com/sophgo/sophgo-doc/releases)。
- SoC 文档：[CV1800B/CV1801B 初步数据手册（英文）](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf)及[中文版](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf) · [SG2002 初步数据手册（中文）](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 初步数据手册（中文）](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf)及[技术参考手册（英文）](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)。
- 官方开发项目：[引脚复用](https://github.com/milkv-duo/duo-pinmux) · [wiringX](https://github.com/milkv-duo/duo-wiringx) · [配件](https://github.com/milkv-duo/accessories) · [LVGL framebuffer 示例](https://github.com/milkv-duo/duo-lvgl-fb-demo)。
- 文档：[GPIO 与引脚复用](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [USB 摄像头](https://milkv.io/docs/duo/camera/usb) · [多媒体框架](https://milkv.io/docs/duo/application-development/multimedia)。
- Arduino：旧版 [Milk-V Arduino 核心库](https://github.com/milkv-duo/duo-arduino) 已归档，其仓库现推荐使用 [Sophgo Arduino](https://github.com/kubuds/sophgo-arduino)。另有 [Duo Arduino 示例](https://github.com/milkv-duo/duo-arduino-examples)；使用前请确认开发板和核心库的支持情况。

## AI、计算机视觉与多媒体

- TDL 示例：[适用于 CV180X／原版 Duo 的 SDK V1](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [适用于 SG200X／Duo 256M 和 Duo S 的 SDK V1](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK V2 示例](https://github.com/milkv-duo/duo-tdl-examples)。
- TPU 与模型工具：[CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [TPU-MLIR 模型转换](https://github.com/milkv-duo/tpu-mlir) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x)。
- [官方多媒体示例](https://github.com/milkv-duo/duo-multimedia-examples) · [TDL 模型部署](https://github.com/milkv-duo/duo-yolo-deployment)。
- [官方镜像下载指南](https://milkv.io/docs/duo/getting-started/download)还列出了按开发板分类的社区镜像；请留意其中的风险提示，并确认镜像维护者及支持的硬件版本。

## 社区操作系统与学习资源

以下均为独立社区项目，并非官方固件。兼容性和维护状态可能变化，安装前请阅读项目自己的文档。

- Linux 发行版：[Fedora 镜像站](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/) · [Sophgo SG200X Debian](https://github.com/scpcom/sophgo-sg200x-debian) · [Ubuntu 镜像构建器](https://github.com/ambraglow/milkv-duo-ubuntu) · [OpenWrt／VizOS 项目](https://github.com/Pillar1989/VizOS)。
- 构建系统与 RTOS：[Yocto／OpenEmbedded 层](https://github.com/kinsamanka/meta-milkv) · [Duo 辅助核心上的 Zephyr](https://github.com/kinsamanka/milkv-zephyros) · [SG2000／Duo S 上的 NuttX](https://github.com/lupyuen/nuttx-sg2000) · [RT-Thread CVitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) · [ThreadX 移植](https://github.com/saicogn/ThreadX-to-RISC-V64)。
- [Milk-V Duo 社区论坛](https://community.milkv.io/c/duo/5) · [Sophgo 论坛](https://forum.sophgo.com/) · [Milk-V Duo GitHub 组织](https://github.com/milkv-duo)。

## 贡献与链接维护

如果链接失效、资源缺失或项目支持的开发板发生变化，欢迎提交 issue 或 pull request。尽量优先引用第一方文档和发行页面，不要重新托管固件。烧录前请核对具体开发板、SoC、内存、存储类型、启动模式和镜像说明；请先备份数据，并遵循安全的供电和接线要求。

[返回语言索引](README.md)
