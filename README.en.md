# Milk-V Duo, Duo 256M & Duo S resource guide

This is a curated directory of official documentation, firmware, source code, hardware files, tutorials, and community projects for the Milk-V Duo family. It is not possible to guarantee that any web index is exhaustive; contributions and corrections are welcome.

> **Check compatibility before use.** The original Duo uses CV1800B and has 64 MB RAM; Duo 256M uses SG2002 and 256 MB; Duo S uses SG2000 and 512 MB. These boards have different hardware and software targets. The original Duo is marked end-of-life in the official overview. Third-party operating systems and images are community-maintained and may be untested.

## Official product and documentation

- [Duo family overview and specifications](https://milkv.io/docs/duo/overview) — board comparison, features, and lifecycle notes.
- Board guides: [Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos).
- Getting started: [booting](https://milkv.io/docs/duo/getting-started/boot) · [download and image selection](https://milkv.io/docs/duo/getting-started/download) · [Buildroot SDK guide](https://milkv.io/docs/duo/getting-started/buildroot-sdk).
- Product pages: [Duo](https://milkv.io/duo) · [Duo 256M](https://milkv.io/duo256m) · [Duo S](https://milkv.io/duos).
- [Official documentation source](https://github.com/milk-v/milkv.io) — contribute fixes or translations.

## Firmware, SDKs, and toolchains

- [Official image catalog and compatibility notes](https://milkv.io/docs/duo/getting-started/download).
- Official firmware releases: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk/releases) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases).
- SDK source: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [host tools](https://github.com/milkv-duo/host-tools).
- V1 images are recommended for the 64 MB Duo; the official download guide recommends V2 for Duo 256M and Duo S. Always check the release notes and target name.
- [Official C/C++ examples and cross-toolchain setup](https://github.com/milkv-duo/duo-examples), including [GPIO blink](https://github.com/milkv-duo/duo-examples/tree/main/blink), [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c), [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi), and the [peripheral guide (PDF)](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf).

## Hardware, peripherals, and application development

- [Official board files, schematics, datasheets, and mechanical drawings](https://github.com/milkv-duo/duo-files).
- Board schematics: [Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf).
- [Sophgo chip datasheets and documents](https://github.com/sophgo/sophgo-doc/releases).
- SoC documents: [CV1800B/CV1801B preliminary datasheet (English)](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf) and [Chinese edition](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf) · [SG2002 preliminary datasheet (Chinese)](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 preliminary datasheet (Chinese)](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) and [technical reference manual (English)](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf).
- Official development projects: [pin multiplexing](https://github.com/milkv-duo/duo-pinmux) · [wiringX](https://github.com/milkv-duo/duo-wiringx) · [accessories](https://github.com/milkv-duo/accessories) · [LVGL framebuffer demo](https://github.com/milkv-duo/duo-lvgl-fb-demo).
- Documentation: [GPIO and pin multiplexing](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [USB cameras](https://milkv.io/docs/duo/camera/usb) · [multimedia framework](https://milkv.io/docs/duo/application-development/multimedia).
- Arduino: the old [Milk-V Arduino core](https://github.com/milkv-duo/duo-arduino) is archived; its repository points to [Sophgo Arduino](https://github.com/kubuds/sophgo-arduino). See also [Duo Arduino examples](https://github.com/milkv-duo/duo-arduino-examples); confirm board and core support before use.

## AI, computer vision, and media

- TDL examples: [SDK V1 for CV180X / original Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SDK V1 for SG200X / Duo 256M and Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK V2 examples](https://github.com/milkv-duo/duo-tdl-examples).
- TPU and model tools: [CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [TPU-MLIR model conversion](https://github.com/milkv-duo/tpu-mlir) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x).
- [Official multimedia examples](https://github.com/milkv-duo/duo-multimedia-examples) · [TDL model deployment](https://github.com/milkv-duo/duo-yolo-deployment).
- The [official download guide](https://milkv.io/docs/duo/getting-started/download) also lists community images by board; follow its warnings and verify each image’s maintainer and supported revision.

## Community operating systems and learning

These are independent projects, not official firmware. Compatibility and maintenance can change; read the project’s own documentation before installing.

- Linux distributions: [Fedora image mirror](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/) · [Debian for Sophgo SG200X](https://github.com/scpcom/sophgo-sg200x-debian) · [Ubuntu image builder](https://github.com/ambraglow/milkv-duo-ubuntu) · [OpenWrt/VizOS project](https://github.com/Pillar1989/VizOS).
- Build systems and RTOS: [Yocto/OpenEmbedded layer](https://github.com/kinsamanka/meta-milkv) · [Zephyr on the Duo secondary core](https://github.com/kinsamanka/milkv-zephyros) · [NuttX on SG2000 / Duo S](https://github.com/lupyuen/nuttx-sg2000) · [RT-Thread CVitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) · [ThreadX port](https://github.com/saicogn/ThreadX-to-RISC-V64).
- [Milk-V Duo community forum](https://community.milkv.io/c/duo/5) · [Sophgo forum](https://forum.sophgo.com/) · [Milk-V Duo GitHub organization](https://github.com/milkv-duo).

## Contributing and link care

Please open an issue or pull request if a link is broken, a resource is missing, or a project’s supported board has changed. Prefer first-party documentation and release pages over rehosting firmware. Before flashing, verify the exact board, SoC, memory size, storage type, boot mode, and image instructions; back up data and follow safe power/wiring practices.

[Back to the language index](README.md)
