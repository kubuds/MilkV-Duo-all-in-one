# Milk-V Duo family resource index (Duo · Duo 256M · Duo S)

Everything we could find for the Milk-V Duo family is gathered on this page as far as possible: official documentation and datasheets, images you can download directly, SDKs and toolchains, open-source projects on GitHub and Gitee, and Bilibili and YouTube videos that genuinely feature this board.

This page does not copy or mirror any firmware or documentation — it only gives sources and maintainers. **Community images and projects have not been tested or endorsed by Milk-V**; before flashing, check the board model, SoC, memory, storage medium, and release notes yourself.

> **First, confirm which board you are holding.** The three generations are not the same thing: Duo uses CV1800B (64 MB RAM), Duo 256M uses SG2002 (256 MB, plus one more Cortex-A53), Duo S uses SG2000 (512 MB, optional Wi-Fi 6 / BT5 and optional eMMC). **The original Duo has been marked end-of-life (EOL) by the vendor**, so new projects should go straight to the 256M or the Duo S.

---

## 1. Boards and variants

| Model | SoC | Memory | Storage | Wireless | Ethernet | TPU | Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Duo** | CVITEK CV1800B | 64 MB | microSD or onboard SD NAND | None | 100M (PHY) | 0.5 TOPS@INT8 | EOL |
| **Duo 256M** | SG2002 | 256 MB | microSD or onboard SD NAND | None | 100M (PHY) | 1.0 TOPS@INT8 | In production |
| **Duo S** | SG2000 | 512 MB | microSD + onboard eMMC footprint | **Optional** Wi-Fi 6 / BT5 | 100M (RJ45, PoE HAT supported) | 0.5 TOPS@INT8 | In production |
| **Duo Module 01** (core board + evaluation board) | SG2000 | 512 MB | 8 GB eMMC onboard | Wi-Fi 6 / BT5.4 onboard | 2× 100M | 0.5 TOPS@INT8 | In production |

**The four Duo S combinations**: eMMC soldered or not × Wi-Fi module soldered or not, four SKUs in total. When buying, check carefully which one the product page is selling.

Images are **split only by boot medium** (`-sd` / `-emmc`), not by Wi-Fi — none of the seven assets in official v2.0.1 has "wifi" in its name (see the table below). So:

- Duo S boards with and without Wi-Fi flash the same image; wireless works only if that module is physically on the board
- A board that has eMMC can flash `-sd` to boot from a TF card, or flash `-emmc` to write to onboard storage
- A board **without** eMMC can only use a TF card

---

## 2. Where to buy

The Kubuds Taobao store (苦芽企业店) carries these three (the listing needs a Taobao login before it shows details; the links themselves return 200):

- **Milk-V Duo 256M** (SG2002, 256 MB, no Wi-Fi): https://item.taobao.com/item.htm?id=842972320584&skuId=5661357677549
- **Milk-V Duo S base version** (SG2000, 512 MB, no Wi-Fi, no eMMC): https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544644
- **Milk-V Duo S Wi-Fi version** (SG2000, 512 MB, Wi-Fi 6 / BT, no eMMC): https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544645

The two Duo S entries are **two SKUs of the same listing** (same `id`, different `skuId`) — check the SKU name for Wi-Fi when ordering. Neither has eMMC, so onboard storage means finding an eMMC variant elsewhere. The original Duo (CV1800B) is end-of-life, so there is no purchase link for it.

This is the only commercial part of the page; everything else points at upstream sources.

---

## 3. Official documentation, datasheets, and hardware files

**Documentation site: a page-by-page index**

- Start here: [Duo family overview and specification comparison](https://milkv.io/docs/duo/overview) (full specification table for all four products, and also where the EOL statement comes from) · [documentation site home](https://milkv.io/docs/duo/getting-started)
- Per-board guides: [Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos) · [Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- Power-on and flashing: [Booting the system](https://milkv.io/docs/duo/getting-started/boot) · [First connection and USB networking](https://milkv.io/docs/duo/getting-started/setup) · [Image download catalog](https://milkv.io/docs/duo/getting-started/download) · [Buildroot SDK build](https://milkv.io/docs/duo/getting-started/buildroot-sdk)
- Dual core and low level: [8051 auxiliary core development](https://milkv.io/docs/duo/getting-started/8051core) · [RTOS small-core development](https://milkv.io/docs/duo/getting-started/rtoscore) · [Arduino support](https://milkv.io/docs/duo/getting-started/arduino) · [Low-level development](https://milkv.io/docs/duo/low-level-dev) ([MIPI DSI](https://milkv.io/docs/duo/low-level-dev/mipi-dsi))
- Application development: [Overview](https://milkv.io/docs/duo/application-development) · [GPIO sysfs](https://milkv.io/docs/duo/application-development/gpio-sysfs) · [Pin multiplexing](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [pinpong](https://milkv.io/docs/duo/application-development/pinpong) · [Multimedia framework](https://milkv.io/docs/duo/application-development/multimedia)
- Cameras: [USB camera](https://milkv.io/docs/duo/camera/usb) · [GC2083 sensor](https://milkv.io/docs/duo/camera/gc2083) · [ISP tuning](https://milkv.io/docs/duo/camera/tuning)
- TPU and TDL: [TPU introduction](https://milkv.io/docs/duo/application-development/tpu/tpu-introduction) · [TDL SDK introduction](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-introduction) · YOLO: [v5](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov5) · [v8](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov8) · [v11](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo11) · [v12](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo12) · [Face detection](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-face-detection) · [Pedestrian detection](https://milkv.io/docs/duo/application-development/tdl-sdk/pedestrian-detection) · [Person and pet detection](https://milkv.io/docs/duo/application-development/tdl-sdk/yolov8-person-pets-detection)
- IO expansion boards: [IO Board overview](https://milkv.io/docs/duo/io-board) · [Duo S PoE HAT](https://milkv.io/docs/duo/io-board/duos-poe-hat) · [USB Ethernet IO board](https://milkv.io/docs/duo/io-board/usb-ethernet-iob)
- Officially curated resources and ecosystem progress: [Useful resources index](https://milkv.io/docs/duo/useful-resources) · [Mainline kernel support status](https://milkv.io/docs/duo/resources/mainline) · [Upstream support status](https://milkv.io/docs/duo/resources/upstream-status) · [MMF multimedia framework](https://milkv.io/docs/duo/resources/mmf) · [OpenCV Mobile](https://milkv.io/docs/duo/resources/opencv-mobile) · [SPILVGL](https://milkv.io/docs/duo/resources/spilvgl) · [Visuino](https://milkv.io/docs/duo/resources/visuino) · [xyzdims notes](https://milkv.io/docs/duo/resources/xyzdims)
- [Documentation site source](https://github.com/milk-v/milkv.io) — if the docs are wrong or you want to add a translation, send a PR here

**Product pages**

- [Duo (family page)](https://milkv.io/duo) · [Duo S](https://milkv.io/duo-s) · [Duo Module 01](https://milkv.io/duo-module-01)
- Duo 256M has no standalone product page; for specifications see the family page and the [documentation](https://milkv.io/docs/duo/getting-started/duo256m)

**Hardware files and chip manuals**

- [duo-files](https://github.com/milkv-duo/duo-files) — the official board-file repository: schematics, datasheets, mechanical drawings, silkscreen
- Schematics: [Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)
- Datasheets: [CV1800B/CV1801B English](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf) ([Chinese](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf)) · [SG2002 Chinese](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 Chinese](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 TRM English](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)
- [Sophgo documentation releases](https://github.com/sophgo/sophgo-doc/releases) — the official outlet for upstream chip documentation

---

## 4. Official images and flashing

All official images are Buildroot-based and come in two lines, V1 and V2. **For the 64 MB Duo, use V1** (V2's AI samples will not run on 64 MB); Duo 256M and Duo S use V2.

### V2 (recommended for Duo 256M / Duo S) · [v2.0.1, 2025-05-30](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)

| Asset file | Board | Boot medium | C library / architecture |
| --- | --- | --- | --- |
| `milkv-duo-musl-riscv64-sd_v2.0.1.img.zip` | Duo | TF card | musl / riscv64 |
| `milkv-duo256m-musl-riscv64-sd_v2.0.1.img.zip` | Duo 256M | TF card | musl / riscv64 |
| `milkv-duo256m-glibc-arm64-sd_v2.0.1.img.zip` | Duo 256M | TF card | glibc / arm64 (via the A53) |
| `milkv-duos-musl-riscv64-sd_v2.0.1.img.zip` | Duo S | TF card | musl / riscv64 |
| `milkv-duos-glibc-arm64-sd_v2.0.1.img.zip` | Duo S | TF card | glibc / arm64 (via the A53) |
| `milkv-duos-musl-riscv64-emmc_v2.0.1.zip` | Duo S (eMMC required) | Onboard eMMC | musl / riscv64 |
| `milkv-duos-glibc-arm64-emmc_v2.0.1.zip` | Duo S (eMMC required) | Onboard eMMC | glibc / arm64 |

### V1 · [v1.1.4, 2024-11-22](https://github.com/milkv-duo/duo-buildroot-sdk/releases)

| Asset file | Board | Boot medium |
| --- | --- | --- |
| `milkv-duo-sd-v1.1.4.img.zip` | Duo | TF card |
| `milkv-duo256m-sd-v1.1.4.img.zip` | Duo 256M | TF card |
| `milkv-duos-sd-v1.1.4.img.zip` | Duo S | TF card |
| `milkv-duos-emmc-v1.1.4.zip` | Duo S (eMMC required) | Onboard eMMC |
| `arduino-milkv-duo-sd-v1.1.4.img.zip` and 3 others | All three boards | Same naming rule, Arduino-preinstalled images |

### Flashing notes

- TF card images: unzip and write with balenaEtcher / `dd`, insert the card and power on; **SSH is on by default, the USB-NCM network interface is on by default, and the root password is `milkv`**
- eMMC images: **not** written the same way as TF card images. On the Duo S, hold the Recovery button, connect to a computer with a Type-C data cable, then flash over USB with CVITEK's `usb_dl.exe` (Windows) or the `CviBurn` tool; always remove the TF card first
- The Duo S has an **ARM / RISC-V boot selector switch**; it will not come up if the firmware and the switch disagree; the first character of the serial log is `C` when booting from RISC-V and `B` when booting from ARM
- On the Duo S, Type-C (USB-NCM) and Type-A (USB HOST) **cannot be used at the same time**; switch between them with the `/mnt/system/usb.sh` symlink

---

## 5. Third-party images (community-maintained, by board)

The official download page has a [third-party image table](https://milkv.io/docs/duo/getting-started/download); here it is flattened out by board so you can click straight through.

### Duo (CV1800B, 64 MB)

- [Fedora 41 image mirror](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo/images/latest/) — maintained by Fedora-V Force, tracks upstream
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) — image build scripts; can also build for the Duo 256M
- [Debian / Ubuntu image builder](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — use this one to produce your own images
- [Arch Linux](https://community.milkv.io/t/arch-linux-on-milkv-duo-milkv-duo-arch-linux/329) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1) · [Full Debian image](https://community.milkv.io/t/milkv-duo-duo-debian-full-7z-519m-download/862)
- [OpenWrt / VizOS](https://github.com/Pillar1989/VizOS) · [Zephyr (secondary core)](https://github.com/kinsamanka/milkv-zephyros) · [Yocto layer](https://github.com/kinsamanka/meta-milkv)
- [RT-Thread cvitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) ([RISC-V RT-Thread programming guide](https://riscv-rtthread-programming-manual.readthedocs.io/zh-cn/latest/)) · [ThreadX port](https://github.com/saicogn/ThreadX-to-RISC-V64)

### Duo 256M (SG2002)

- [Fedora 41 image mirror](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo256M/images/latest/)
- [Debian (Fishwaldo / sophgo-sg200x-debian)](https://github.com/Fishwaldo/sophgo-sg200x-debian/releases/tag/v1.2.0)
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) · [Arch Linux](https://community.milkv.io/t/debian-arch-linux-on-milkv-duo-256m-milkv-duo-256m-debian-arch-linux/1110) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1)

### Duo S (SG2000)

- [Fedora 41 image mirror](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/DuoS/images/latest/) — default account `root` / password `riscv`
- [Debian (scpcom)](https://github.com/scpcom/sophgo-sg200x-debian/releases) — two account sets, `root`/`rv` and `debian`/`rv`
- [NuttX (lupyuen)](https://github.com/lupyuen/nuttx-sg2000/releases) — ready-made images for running NuttX on the Duo S

---

## 6. SDKs, toolchains, and examples

- SDK sources: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [Host-side toolchain](https://github.com/milkv-duo/host-tools)
- [duo-examples](https://github.com/milkv-duo/duo-examples) — official C/C++ examples: [GPIO blink](https://github.com/milkv-duo/duo-examples/tree/main/blink) · [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c) · [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) · [Peripheral driver operation guide (PDF)](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) (pin multiplexing) · [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) (wiringX port) · [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) (LVGL framebuffer) · [duo-accessories](https://github.com/milkv-duo/accessories) (official accessories)
- Arduino: [archived official core library](https://github.com/milkv-duo/duo-arduino) (the repository now points to [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)) · [Duo Arduino examples](https://github.com/milkv-duo/duo-arduino-examples)
- SoC-side tools: [CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x) · [TPU-MLIR model conversion](https://github.com/milkv-duo/tpu-mlir)
- TDL (deep-learning examples): [CV180X / Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SG200X / Duo 256M & Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK V2 TDL examples](https://github.com/milkv-duo/duo-tdl-examples) · [YOLO deployment](https://github.com/milkv-duo/duo-yolo-deployment)
- Multimedia: [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples)

---

## 7. Official organization, community, and discussion

- [milkv-duo GitHub organization](https://github.com/milkv-duo) — official SDKs, examples, and hardware files all live here
- [Milk-V community Duo category](https://community.milkv.io/c/duo/5) — the main venue for questions and experience reports
- [Duo Module 01 evaluation board documentation](https://milkv.io/docs/duo/getting-started/duo-module-01)
- The former `forum.sophgo.com` can no longer be reached (connection failed when tested in 2026-10); chip-side material now comes from [sophgo-doc](https://github.com/sophgo/sophgo-doc/releases)

---

## 8. Videos: Bilibili (49)

Every page was checked individually to confirm it exists (HTTP 200) and that its title/description really points to the Duo family; view counts are a snapshot from 2026-10-31 and serve only as an indication of popularity.

**The eastdong series — the best place to start from zero**

- 《零压力上手 RISC-V：东东老师带你玩转 milk-v duo》01. RVOS on Duo — [BV1vm421E7R6](https://www.bilibili.com/video/BV1vm421E7R6/) · 9578
- 02. RT-Thread on Duo — [BV1ym411z7Qo](https://www.bilibili.com/video/BV1ym411z7Qo/) · 3558
- 04. Camera 和 YOLOv5 图像识别 — [BV1mt421A7tL](https://www.bilibili.com/video/BV1mt421A7tL/) · 2972
- 05. TPU 使用 — [BV1Wi421Q7b4](https://www.bilibili.com/video/BV1Wi421Q7b4/) · 2171
- 06. 完结（补讲 Duo 256M 的新变化）— [BV1Fx4y1W7x9](https://www.bilibili.com/video/BV1Fx4y1W7x9/) · 2212

**Kubuds — the complete official Duo S course**

- 00. 认识 Milk-V Duo S — [BV1PNDoYeEpT](https://www.bilibili.com/video/BV1PNDoYeEpT/) · 2307
- 01. Windows 下安装及启动 — [BV1u3DYYGES7](https://www.bilibili.com/video/BV1u3DYYGES7/) · 376
- macOS 下安装及启动 — [BV1U5qqYUEAm](https://www.bilibili.com/video/BV1U5qqYUEAm/) · 233
- 02. SPI 演示 — [BV1vYqHYnE8G](https://www.bilibili.com/video/BV1vYqHYnE8G/) · 186

**Getting started and reviews**

- 35 块带 TPU、1GHz 的 Linux 开发板，还玩啥树莓派（科学中国）— [BV19h4y1t7Ct](https://www.bilibili.com/video/BV19h4y1t7Ct/) · 1.9 万
- 镜像烧写教程：带 TPU 的 RISC-V Linux 板（斑梨电子）— [BV1uM4y1n763](https://www.bilibili.com/video/BV1uM4y1n763/) · 9098
- 能跑轻量 AI 的最便宜 RISC-V Linux 开发板？Duo 64M（捡个肥仔上战场）— [BV11w411j71u](https://www.bilibili.com/video/BV11w411j71u/) · 9365
- RISC-V 峰会现场 Duo 开箱（半导体都市隶人 Ayla）— [BV1oh4y1K724](https://www.bilibili.com/video/BV1oh4y1K724/) · 8415
- 野生的开发板性能再强又有何用，软件适配稀烂：Duo 256M 尝试 Arduino 彻底失败（沈洁 Eacc）— [BV1sZZHYdEPP](https://www.bilibili.com/video/BV1sZZHYdEPP/) · 8026 ← **negative review, worth watching**
- 35 元的 milkv-duo Linux 单片机还要啥自行车（开源社区的二掌柜）— [BV1tM4y1Y7kh](https://www.bilibili.com/video/BV1tM4y1Y7kh/) · 2792
- 学习 RISC-V 能跑 Debian & Linux 的最便宜开发板之一（蘭雅 sRGB）— [BV1XQ4y1E7Tj](https://www.bilibili.com/video/BV1XQ4y1E7Tj/) · 3054
- 好玩！RISC-V duo256M 开发板测玩（蘭雅 sRGB）— [BV1Zw411V7bK](https://www.bilibili.com/video/BV1Zw411V7bK/) · 2257
- 麻雀虽小五脏俱全：超高性价比开发板 Milk-V Duo S（qinyunti）— [BV1hyKmzJEw5](https://www.bilibili.com/video/BV1hyKmzJEw5/) · 664

**Environment setup and flashing**

- Linux 下开发环境搭建（future 待续）— [BV1B8411m7jR](https://www.bilibili.com/video/BV1B8411m7jR/) · 3192
- 烧写 Linux 系统 + USB 虚拟 RNDIS 网卡登录（蘭雅 sRGB）— [BV1G14y1k7V4](https://www.bilibili.com/video/BV1G14y1k7V4/) · 1062
- Duo-debian 初体验（蘭雅 sRGB）— [BV11c411o76T](https://www.bilibili.com/video/BV11c411o76T/) · 3416
- Duo 简介和开发环境搭建（谁说现在是冬天呢）— [BV1PF411S7To](https://www.bilibili.com/video/BV1PF411S7To/) · 1959
- Buildroot SDK 简介和编译镜像的方法（谁说现在是冬天呢）— [BV1xc411s7qk](https://www.bilibili.com/video/BV1xc411s7qk/) · 462
- 安装 Hyper-V & 配置 Docker 开发环境（_1dentity）— [BV1nC4y117WS](https://www.bilibili.com/video/BV1nC4y117WS/) · 1826

**Peripherals, displays, and dual core**

- LVGL 库实战教程 — 刘文涛（群芯闪耀），lazyparser 频道 — [BV1Mp421m7qJ](https://www.bilibili.com/video/BV1Mp421m7qJ/) · 966
- 通过 SPI 驱动 ST7789V 跑 LVGL（谁说现在是冬天呢）— [BV1gLeueWEWr](https://www.bilibili.com/video/BV1gLeueWEWr/) · 2239
- Duo 256M 基于 TinyDRM 驱动 ST7796s 4.0 寸屏并移植 LVGL 8.3（二掌柜）— [BV1Tv421k71W](https://www.bilibili.com/video/BV1Tv421k71W/) · 1230
- USB & Ethernet IO-Board 简介和使用方法（谁说现在是冬天呢）— [BV1Ga4y1Z7oM](https://www.bilibili.com/video/BV1Ga4y1Z7oM/) · 1096
- 通过大核控制小核点亮 LED（谁说现在是冬天呢）— [BV1nH4y1y7CM](https://www.bilibili.com/video/BV1nH4y1y7CM/) · 1057
- 用 Duo 驱动 DF9GMS 微型舵机（谁说现在是冬天呢）— [BV1Dj411E7yD](https://www.bilibili.com/video/BV1Dj411E7yD/) · 571
- Duo S 硬件解码 MP4 并在 LCD 上播放（一只御坂美琴）— [BV1ktvseWEhr](https://www.bilibili.com/video/BV1ktvseWEhr/) · 519

**OS ports**

- 在 Duo 上运行 ThreadX（谁说现在是冬天呢）— [BV1yi421C7SK](https://www.bilibili.com/video/BV1yi421C7SK/) · 419
- 在小核上运行 Zephyr OS（谁说现在是冬天呢）— [BV1uK421Y7x9](https://www.bilibili.com/video/BV1uK421Y7x9/) · 435
- 在 Duo 256M 上运行 Arch Linux（谁说现在是冬天呢）— [BV1j8yyYTEp2](https://www.bilibili.com/video/BV1j8yyYTEp2/) · 1274
- 在 Duo S 上启动 NuttX（悲伤的黑山羊）— [BV1RMUeYjELe](https://www.bilibili.com/video/BV1RMUeYjELe/) · 75
- 罗君：Duo 的 UniProton 适配（PLCT 内部报告）（lazyparser）— [BV1RD421G773](https://www.bilibili.com/video/BV1RD421G773/) · 903
- Duo S 启动！（谁说现在是冬天呢）— [BV1Bm421N72y](https://www.bilibili.com/video/BV1Bm421N72y/) · 564
- 使用 Wi-Fi 连接 Duo S（谁说现在是冬天呢）— [BV11r421T7Sk](https://www.bilibili.com/video/BV11r421T7Sk/) · 318
- 在 Duo S 上部署 Caddy 服务器（谁说现在是冬天呢）— [BV1poBzYQEoC](https://www.bilibili.com/video/BV1poBzYQEoC/) · 214
- Duo 256M 部署相册文件管理器和博客笔记（蘭雅 sRGB）— [BV1cC4y1e7uk](https://www.bilibili.com/video/BV1cC4y1e7uk/) · 1455

**AI / vision**

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

## 9. Videos: YouTube (37)

An overseas site that requires a proxy to open; every page here was likewise checked to confirm it exists and really covers the Duo.

**Reviews and first looks**

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

**Getting started, flashing, and networking**

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

**Peripherals and AI**

- Anton Maltsev — Is it good for computer vision? How to start a neural network on it — [dkIVDOd_Fa4](https://www.youtube.com/watch?v=dkIVDOd_Fa4) · Duo
- Mark Birss — Milk-V Duo USB input ST7789 240×240 SPI display — [Swo-zJ6brQI](https://www.youtube.com/watch?v=Swo-zJ6brQI) · Duo
- Sonny Cruz — I²C demo, source in the description — [85uglOz48Pg](https://www.youtube.com/watch?v=85uglOz48Pg) · Duo
- Sonny Cruz — RC servo demo using PWM — [1u2LZJWPtNU](https://www.youtube.com/watch?v=1u2LZJWPtNU) · Duo
- Leigh — Duo + CAM-GC2083: fix RTSP streaming to VLC — [PjiUDsoWCvo](https://www.youtube.com/watch?v=PjiUDsoWCvo) · Duo
- Muhammad Yunus — YOLOX inference on Duo S using TDL SDK + VPSS — [wzUTGK4TuqA](https://www.youtube.com/watch?v=wzUTGK4TuqA) · Duo S

**OS ports and complete projects**

- Muhammad Yunus — RT-Thread on Duo S: the best RTOS for cheap RISC-V? — [WjWM5YoAq-c](https://www.youtube.com/watch?v=WjWM5YoAq-c) · Duo S
- RISC-V Developers — S1E2 Enjoy RISC-V with Milk-V Duo: RT-Thread — [B7EXWE6l9xE](https://www.youtube.com/watch?v=B7EXWE6l9xE) · Duo
- Chris McDonough — NixOS 71: NixOS on RISC-V (Milk-V Duo / Duo 256M) — [-ydXjEWUlGE](https://www.youtube.com/watch?v=-ydXjEWUlGE) · Duo family
- admin ka — Running Ubuntu glibc 24.04.4 on the Duo 256M — [0Dqbdtjt8Ro](https://www.youtube.com/watch?v=0Dqbdtjt8Ro) · Duo 256M
- 福田重夫 — Running Linux on the Duo 256M (RISC-V + ARM) — [Ga3HX-d8GHQ](https://www.youtube.com/watch?v=Ga3HX-d8GHQ) · Duo 256M
- Nch-Lab — Milk-V Duo 256M を買ったので Linux を動かしてみる — [tcAqYCwbqeU](https://www.youtube.com/watch?v=tcAqYCwbqeU) · Duo 256M
- Mark Birss — Duo 256 CyberDeck LoRa communicator (TLMVC) — [9qOJ3fKwfC0](https://www.youtube.com/watch?v=9qOJ3fKwfC0) · Duo 256M

---

## 10. GitHub open-source projects

Grouped by use. Star counts and last-commit dates are a snapshot from 2026-10-31 and will change; entries described as official are repositories under the milkv-duo organization.

**Official SDKs, firmware, and tools**

- [duo-buildroot-sdk](https://github.com/milkv-duo/duo-buildroot-sdk) — official Buildroot SDK V1 (Duo/CV1800B) · 495★
- [duo-buildroot-sdk-v2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) — official SDK V2 (Duo 256M / Duo S, SG200x) · 154★
- [duo-examples](https://github.com/milkv-duo/duo-examples) — official C/C++ peripheral examples · 159★
- [duo-sdk](https://github.com/milkv-duo/duo-sdk) — host-side cross-compilation SDK (duo-app-sdk) · 5★
- [host-tools](https://github.com/milkv-duo/host-tools) — prebuilt host gcc toolchain · 9★
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) — pin multiplexing configuration tool · 7★
- [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) — Duo port of wiringX · 11★
- [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples) — multimedia pipeline examples · 6★
- [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) — LVGL on framebuffer · 10★
- [duo-arduino](https://github.com/milkv-duo/duo-arduino) — official Arduino support (archived, now points to [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)) · 20★
- [duo-arduino-examples](https://github.com/milkv-duo/duo-arduino-examples) — Arduino examples
- [duo-tdl-examples](https://github.com/milkv-duo/duo-tdl-examples) — TDL samples for SDK V2 · 13★
- [cvitek-tdl-sdk-sg200x](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) — SG200x TDL-SDK samples · 30★
- [cvitek-tdl-sdk-cv180x](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) — CV180x TDL-SDK samples
- [tpu-sdk-sg200x](https://github.com/milkv-duo/tpu-sdk-sg200x) — SG200x TPU SDK · 5★
- [tpu-sdk-cv180x](https://github.com/milkv-duo/tpu-sdk-cv180x) — CV180x TPU SDK
- [tpu-mlir](https://github.com/milkv-duo/tpu-mlir) — TPU-MLIR model conversion · 9★
- [duo-yolo-deployment](https://github.com/milkv-duo/duo-yolo-deployment) — YOLO deployment examples
- [milkv-duo-linux](https://github.com/milkv-duo/milkv-duo-linux) — official kernel tree · 1★
- [milkv-duo-u-boot](https://github.com/milkv-duo/milkv-duo-u-boot) — official U-Boot tree · 4★
- [milkv-duo-opensbi](https://github.com/milkv-duo/milkv-duo-opensbi) — official OpenSBI port · 2★
- [milkv-duo-smallcore-freertos](https://github.com/milkv-duo/milkv-duo-smallcore-freertos) — FreeRTOS on the C906 small core · 17★
- [duo-8051](https://github.com/milkv-duo/duo-8051) — examples for the built-in 8051 core · 8★

**Official documentation and hardware files**

- [duo-files](https://github.com/milkv-duo/duo-files) — central repository of schematics, datasheets, and mechanical drawings · 203★
- [accessories](https://github.com/milkv-duo/accessories) — official accessory files · 14★
- [milkv.io](https://github.com/milk-v/milkv.io) — website and documentation site source · 4★
- [sophgo-doc](https://github.com/sophgo/sophgo-doc) — upstream chip documentation outlet
- [datasheet-en](https://github.com/taspenwall/datasheet-en) — English translation of the SG2002 datasheet · 5★
- [riscv-rtthread-programming-manual](https://github.com/flyingcys/riscv-rtthread-programming-manual) — companion code for the book "RISC-V Programming Guide: Based on RT-Thread and Milk-V Duo" · 10★
- [MilkV-Duo-Resources](https://github.com/robtech21/MilkV-Duo-Resources) — resource collection
- [johandevlabs/milk-v-duo-s-notes](https://github.com/johandevlabs/milk-v-duo-s-notes) — Duo S tinkering notes · 5★
- [Mirrorium227/MilkvDuo_Basic](https://github.com/Mirrorium227/MilkvDuo_Basic) — CV1800B troubleshooting and examples
- [imagineeeinc/things-on-milkv-duo](https://github.com/imagineeeinc/things-on-milkv-duo) — playing with the Duo in Nim

**Boot and firmware**

- [u-boot/u-boot](https://github.com/u-boot/u-boot) — mainline already includes `board/sophgo/milkv_duo` · 5309★
- [sg_boot](https://github.com/platform-system-interface/sg_boot) — bootloader for CV1800B/SG200x written in Rust · 12★
- [gtxzsxxk/milkv-duo-firmware-fsbl](https://github.com/gtxzsxxk/milkv-duo-firmware-fsbl) — FSBL implementation · 6★
- [Taumille/uboot-milkv](https://github.com/Taumille/uboot-milkv) — community fork of the official u-boot repository that has disappeared

**Distributions and system images**

- [armbian/build](https://github.com/armbian/build) — already includes `milkv-duos-riscv` / `milkv-duos-arm` board targets · 5499★
- [Fishwaldo/sophgo-sg200x-debian](https://github.com/Fishwaldo/sophgo-sg200x-debian) — the most active SG200x Debian build · 219★
- [ambraglow/milkv-duo-ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) — Duo Ubuntu · 68★
- [olivaw448/milkv-duo-s-512mb-debian](https://github.com/olivaw448/milkv-duo-s-512mb-debian) — Duo S 512MB Debian (with WiFi/Bluetooth/USB host/camera) · 11★
- [eznix86/milkv-duo-s-alpine-linux](https://github.com/eznix86/milkv-duo-s-alpine-linux) — Duo S Alpine · 9★
- [CrocNet/duo-docker-builder](https://github.com/CrocNet/duo-docker-builder) — build Ubuntu images with Docker · 9★
- [logicethos/Milk-V_Duo_Linux2SD](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — build and write straight to the card · 21★
- [RawFish69/ubuntu-milkv-duos](https://github.com/RawFish69/ubuntu-milkv-duos) — Duo S Ubuntu 22.04
- [draftbottle/Milkv-duo-openwrt](https://github.com/draftbottle/Milkv-duo-openwrt) — OpenWrt based on VizOS
- [Pillar1989/VizOS](https://github.com/Pillar1989/VizOS) — OpenWrt / VizOS project
- [georgewhewell/nixos-nanokvm](https://github.com/georgewhewell/nixos-nanokvm) — NixOS configuration for SG2000/SG2002
- [kinsamanka/meta-milkv](https://github.com/kinsamanka/meta-milkv) — Yocto / OpenEmbedded layer

**RTOS and bare metal**

- [RT-Thread/rt-thread](https://github.com/RT-Thread/rt-thread) — `bsp/cvitek` covers milkv-duo / duo256m / duos · 12318★
- [lupyuen/nuttx-sg2000](https://github.com/lupyuen/nuttx-sg2000) — NuttX on the Duo S · 45★
- [kinsamanka/milkv-zephyros](https://github.com/kinsamanka/milkv-zephyros) — Zephyr on the small core · 35★
- [saicogn/ThreadX-to-RISC-V64](https://github.com/saicogn/ThreadX-to-RISC-V64) — ThreadX port · 8★
- [Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK](https://github.com/Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK) — dual-core bare metal without the SDK · 11★
- [zuki/xv6-milkv-duo](https://github.com/zuki/xv6-milkv-duo) — xv6 on Duo · 7★
- [jiegegena/milkv-sg2002-xv6](https://github.com/jiegegena/milkv-sg2002-xv6) — xv6 on SG2002
- [Lam920/xv6-cv1800b](https://github.com/Lam920/xv6-cv1800b) — xv6 on CV1800B
- [rota1001/milkv-baremetal-toolkit](https://github.com/rota1001/milkv-baremetal-toolkit) — one-command bare-metal image generation · 8★
- [PeterForth/MILKV-FORTH](https://github.com/PeterForth/MILKV-FORTH) — Forth on the Duo · 8★
- [xingrz/milkv-duo-zephyr-mailbox-example](https://github.com/xingrz/milkv-duo-zephyr-mailbox-example) — mailbox communication between Zephyr and Linux
- [DivByDiamond/OnyxOS](https://github.com/DivByDiamond/OnyxOS) — monolithic RISC-V kernel in Rust (~272 KB in total, including a C++ bootloader and a self-hosting C compiler); ships SG2000 platform drivers and lists Duo S as a target board · 0★

**Toolchains and build environments**

- [aidancrowther/Milk-V-Duo-Docker-Compile](https://github.com/aidancrowther/Milk-V-Duo-Docker-Compile) — Docker image with the toolchain preinstalled · 24★
- [Tosainu/docker-milkv-duo-linux](https://github.com/Tosainu/docker-milkv-duo-linux) — containerized Linux builds
- [boberace/milkv_duo_dc](https://github.com/boberace/milkv_duo_dc) — VS Code Dev Container
- [kitnerboy/milkv-duo-buildroot](https://github.com/kitnerboy/milkv-duo-buildroot) — mainline-style Buildroot BSP

**Drivers and peripherals**

- [hexdump0815/linux-cvitek-cv18xx-kernel](https://github.com/hexdump0815/linux-cvitek-cv18xx-kernel) — community kernel tree (the kernel source for several images)
- [ret7020/CVI_HW_OpenCV](https://github.com/ret7020/CVI_HW_OpenCV) — OpenCV port accelerated with the NPU · 7★
- [pavelanni/gpiod-milkvduo](https://github.com/pavelanni/gpiod-milkvduo) — libgpiod usage · 3★
- [Satharus/I2C-WiringX-Milk-V](https://github.com/Satharus/I2C-WiringX-Milk-V) — I²C through wiringX · 2★
- [KuLvo/milk-v_duo_oled_driver](https://github.com/KuLvo/milk-v_duo_oled_driver) — 0.96-inch OLED driver · 3★
- [queenkjuul/aic8800-milkv-duos](https://github.com/queenkjuul/aic8800-milkv-duos) — AIC8800 WiFi+BT support
- [GrootLiu/milkv-duo-rtl8723du](https://github.com/GrootLiu/milkv-duo-rtl8723du) — RTL8723DU WiFi port
- [Tactical-TV-Remote/infrared_milkv](https://github.com/Tactical-TV-Remote/infrared_milkv) — infrared transmit and receive (Rust)
- [harshareddy1611/milkv-duo-s-baremetal-drivers](https://github.com/harshareddy1611/milkv-duo-s-baremetal-drivers) — Duo S bare-metal GPIO/UART
- [wanghengZzz/Milkv-Duo-FreeRTOS-DMA](https://github.com/wanghengZzz/Milkv-Duo-FreeRTOS-DMA) — FreeRTOS DMA HAL

**Projects in practice**
- [tidesense](https://github.com/HumpbackLab/tidesense) — stereo visual-inertial odometry on SG2002 (custom board, not a Duo 256M): dual OV9281 global-shutter cameras plus an SC7U22 IMU, SchurVINS at 20 Hz visual correction / 200 Hz prediction, with OpenVINS comparison, calibration and dataset tooling; the VIO runs on the Cortex-A53 and boots from SD only. Hardware is open under CC BY-NC-SA 4.0 (link in the repository README) · 142★

- [pavelanni/milkv-duo-experiments](https://github.com/pavelanni/milkv-duo-experiments) — collection of experiments written in Go · 27★
- [driver1998/DiscEmu](https://github.com/driver1998/DiscEmu) — using the Duo as a CD-ROM emulator · 11★
- [0x1iii1ii/Pwn-V-Duo](https://github.com/0x1iii1ii/Pwn-V-Duo) — PPPwn exploit port · 6★
- [aceraoc/MilkV-Duo_TPU](https://github.com/aceraoc/MilkV-Duo_TPU) — TPU inference examples · 8★
- [xmdjy/milkv-car](https://github.com/xmdjy/milkv-car) — smart car based on the Duo
- [Arielfoever/milkv-duo-yolo11](https://github.com/Arielfoever/milkv-duo-yolo11) — YOLO11 deployment
- [Basicname/SG200x_GC2083_Yolov8_11](https://github.com/Basicname/SG200x_GC2083_Yolov8_11) — single-file YOLOv8/11 + GC2083 deployment
- [chius-me/globi-v](https://github.com/chius-me/globi-v) — assistive vision system for the visually impaired on the Duo S
- [f3jry/milkv-duo-xmrsigner](https://github.com/f3jry/milkv-duo-xmrsigner) — Monero cold wallet ported to the Duo
- [sdwood68/MilkV_Duo_S_Camera](https://github.com/sdwood68/MilkV_Duo_S_Camera) — camera node that works with Frigate / Home Assistant
- [ar90n/ptp-server-milkv-duos](https://github.com/ar90n/ptp-server-milkv-duos) — PTP grandmaster clock server
- [avalitan/MilkV-Duo-S-NTP-UPS-Server](https://github.com/avalitan/MilkV-Duo-S-NTP-UPS-Server) — NTP + NUT UPS monitoring
- [vojinvukcevic/boot-time-optimization-milkv](https://github.com/vojinvukcevic/boot-time-optimization-milkv) — full write-up of cold boot going from 14.1 s to 3.2 s
- [Tom-game-project/MilkV-DuoS-rust-tpu-example](https://github.com/Tom-game-project/MilkV-DuoS-rust-tpu-example) — TPU matrix multiplication from Rust on Duo S: the Makefile pulls host-tools, tpu-sdk-sg200x and tpu-mlir, compiles ONNX into .cvimodel, cross-builds Rust for riscv64 musl and deploys over scp · 0★

**Hardware and enclosures**

- [iyegoroff/milkv-duo-s-case](https://github.com/iyegoroff/milkv-duo-s-case) — parametric 3D-printed case for the Duo S · 12★
- [pauleffect90/MilkVDuoKicad](https://github.com/pauleffect90/MilkVDuoKicad) — KiCad symbols and footprints · 4★
- [Tosainu/milkv-duo-iob](https://github.com/Tosainu/milkv-duo-iob) — IO expansion board design files

---

## 11. Gitee projects and Chinese-language tutorials

**Gitee (19)**

- [tinylab/milkv-buildroot](https://gitee.com/tinylab/milkv-buildroot) — Buildroot build project for the TinyLab community images
- [tinylab/duo-buildroot-sdk](https://gitee.com/tinylab/duo-buildroot-sdk) — domestic mirror of the official V1 SDK
- [tinylab/duo-examples](https://gitee.com/tinylab/duo-examples) — domestic mirror of the official examples
- [tinylab/i2c-lsm6dsr](https://gitee.com/tinylab/i2c-lsm6dsr) — I²C LSM6DSR sensor example
- [weilinfox/pinpong-milkv-duo-doc](https://gitee.com/weilinfox/pinpong-milkv-duo-doc) — running pinpong on the Duo · 3★
- [lan-ruixin/duo-buildroot-sdk](https://gitee.com/lan-ruixin/duo-buildroot-sdk) — personally maintained V1 branch with Chinese build notes added
- [lan-ruixin/milkv-duo-rtl8723du](https://gitee.com/lan-ruixin/milkv-duo-rtl8723du) — RTL8723DU WiFi/Bluetooth support
- [qhw136/milkv_duo_sdk](https://gitee.com/qhw136/milkv_duo_sdk) — enhanced SDK with LCD/touch/WiFi/Bluetooth added
- [zhidao101/Milkv_duo_Ubuntu_image](https://gitee.com/zhidao101/Milkv_duo_Ubuntu_image) — Ubuntu 22.04 images for the 256M and 512MB variants
- [tiberium/duosdk2yocto](https://gitee.com/tiberium/duosdk2yocto) — turns the SDK into a Yocto build
- [tiberium/meta-milkv-duo-sdk](https://gitee.com/tiberium/meta-milkv-duo-sdk) — the matching meta layer
- [fixxer2020/duo-multimedia-examples](https://gitee.com/fixxer2020/duo-multimedia-examples) — mirror of the multimedia examples
- [dongshan-community/DongShanPiExtboard](https://gitee.com/dongshan-community/DongShanPiExtboard) — mini-ITX expansion board for the Duo 256M
- [linux-proj/Milkv-duo_Cross_Compile_software](https://gitee.com/linux-proj/Milkv-duo_Cross_Compile_software) — prebuilt cross-compilation dependency packages
- [atari/opencv-mobile](https://gitee.com/atari/opencv-mobile) — opencv-mobile sync repository (riscv64-musl, hardware JPEG decoding, MIPI CSI) · 5★
- [unicornx/riscv-operating-system-mooc](https://gitee.com/unicornx/riscv-operating-system-mooc) — RVOS course code (already ported to the Duo) · 541★
- [openeuler/UniProton](https://gitee.com/openeuler/UniProton) — includes big/little-core examples in `demos/milkv-duo` · 73★ (repository has moved to AtomGit)
- [k0059/duo-buildroot-sdk-v2](https://gitee.com/k0059/duo-buildroot-sdk-v2) — sg200x-evb branch of SDK V2
- [xju_kjc/duo-buildroot-sdk](https://gitee.com/xju_kjc/duo-buildroot-sdk) — complete mirror of the V1 SDK (Chinese/Japanese/English README)

**Chinese-language tutorials and articles (22)**

- Cnblogs [milkv-duo 启动流程分析：手动构建 fip.bin [1/2]](https://www.cnblogs.com/maomaotou-thu/p/17765721.html) · [2/2](https://www.cnblogs.com/maomaotou-thu/p/17766024.html) · [手动构建 boot.sd](https://www.cnblogs.com/maomaotou-thu/p/17767315.html) — essential reading if you want to understand the boot chain
- Cnblogs [Milk-V Duo S 使用报告](https://www.cnblogs.com/BiaoZyx/p/18956632) — from unboxing to trying the peripherals, pitfalls included
- Cnblogs [大作业：milkv-duo 小车设计工作日志](https://www.cnblogs.com/Cybersites/p/18859275)
- Cnblogs [小核引导 RTOS —— RISC-V C906](https://www.cnblogs.com/gaoyang3513/articles/18854508)
- Cnblogs [集成构建流程之根文件系统 Buildroot](https://www.cnblogs.com/gaoyang3513/p/18854502) · [网络升级固件](https://www.cnblogs.com/gaoyang3513/p/18854509) · [以太网使用与配置](https://www.cnblogs.com/gaoyang3513/p/18854518) · [Docker 开发环境搭建](https://www.cnblogs.com/gaoyang3513/p/18854511)
- Cnblogs [milkv duo 256M 使用 Debian 系统](https://www.cnblogs.com/GrootStudy/p/18225934)
- Cnblogs [milkV-duo 的 Linux 开发环境搭建](https://www.cnblogs.com/yzh0526/p/18098794)
- Cnblogs [milk-v duo 开机引导进入 rust 程序](https://www.cnblogs.com/longxiangam/p/19640491)
- Juejin [milkv-duo 开发环境搭建 & 烧录](https://juejin.cn/post/7269416466314821668) · [打包 SDK 时遇到的问题及解决](https://juejin.cn/post/7269417409370505235) · [小奶板点灯 & sensor bring up](https://juejin.cn/post/7269644295588659261) · [image burn](https://juejin.cn/post/7269424598260334648) · [milkv 256duo 初品](https://juejin.cn/post/7355829021311238182)
- Bilibili articles [Milk-v Duo：35 块带 TPU 1GHz 的 Linux 开发板](https://www.bilibili.com/read/cv24253633) · [Linux 与 RTOS 双核开发实践](https://www.bilibili.com/read/cv27449966) · [Duo S 部署 PicoClaw 完整教程](https://www.bilibili.com/read/cv46804507) · [Ubuntu 20.04 详细编译环境搭建指南](https://www.bilibili.com/read/cv24743710)

> **CSDN and Zhihu are still missing**: on this machine's network both sites return 521 / 403 (direct browser visits are blocked as well), so a link cannot pass the check that the page really exists, and unverified links are therefore not included. The RT-Thread Q&A community `club.rt-thread.org` is likewise blocked by a WAF. They will be added once they can be reached directly.

---

## 12. How this index is maintained

- An incremental full-web scan runs automatically once a day at 14:00 (official releases, new documentation pages, new videos, new repositories), and any change is committed as an update
- Only links that **open** are included; every update runs a full link check, and dead links are dropped or replaced with a new address
- Videos must actually use the Duo family; projects must genuinely support these boards in the repository (not just mention them in passing)
- Inclusion is not endorsement. Please judge the safety, licensing, and maintenance status of third-party images and projects yourself
- If you find a missing resource, an issue or PR is welcome; when you send a PR, put it in the existing section and note the applicable board (Duo / Duo 256M / Duo S)

[Back to the language index](README.md)
