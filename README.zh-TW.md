# Milk-V Duo、Duo 256M 與 Duo S 資源指南

本頁彙整 Milk-V Duo 系列的官方文件、韌體、原始碼、硬體資料、教學與社群專案。網路資源無法保證絕對完整，歡迎補充或回報失效連結。

> **使用前請確認相容性。** 原版 Duo 採用 CV1800B，記憶體為 64 MB；Duo 256M 採用 SG2002，記憶體為 256 MB；Duo S 採用 SG2000，記憶體為 512 MB。三款開發板的硬體和軟體目標並不相同。官方概覽已將原版 Duo 標示為停產（EOL）。第三方系統與映像檔由社群維護，不一定經過測試。

## 官方產品與文件

- [Duo 系列概覽與規格](https://milkv.io/docs/duo/overview) — 開發板比較、功能與產品生命週期說明。
- 開發板指南：[Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos)。
- 入門：[啟動系統](https://milkv.io/docs/duo/getting-started/boot) · [映像檔下載與選擇](https://milkv.io/docs/duo/getting-started/download) · [Buildroot SDK 指南](https://milkv.io/docs/duo/getting-started/buildroot-sdk)。
- 產品頁面：[Duo](https://milkv.io/duo) · [Duo 256M](https://milkv.io/duo256m) · [Duo S](https://milkv.io/duos)。
- [官方文件原始碼](https://github.com/milk-v/milkv.io) — 可提交修正或翻譯。

## 韌體、SDK 與工具鏈

- [官方映像檔目錄與相容性說明](https://milkv.io/docs/duo/getting-started/download)。
- 官方韌體發行頁：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk/releases) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)。
- SDK 原始碼：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [主機工具鏈](https://github.com/milkv-duo/host-tools)。
- 官方下載指南建議 64 MB 的 Duo 使用 V1 映像檔，Duo 256M 與 Duo S 使用 V2。請務必核對發行說明和建置目標名稱。
- [官方 C/C++ 範例與交叉編譯工具鏈設定](https://github.com/milkv-duo/duo-examples)，包含 [GPIO 閃燈](https://github.com/milkv-duo/duo-examples/tree/main/blink)、[I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c)、[SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) 和[週邊指南（PDF）](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)。

## 硬體、週邊與應用程式開發

- [官方開發板檔案、電路圖、資料手冊與機構圖](https://github.com/milkv-duo/duo-files)。
- 開發板電路圖：[Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)。
- [Sophgo 晶片資料手冊與文件](https://github.com/sophgo/sophgo-doc/releases)。
- SoC 文件：[CV1800B/CV1801B 初步資料手冊（英文）](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf)及[中文版](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf) · [SG2002 初步資料手冊（中文）](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 初步資料手冊（中文）](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf)及[技術參考手冊（英文）](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)。
- 官方開發專案：[腳位複用](https://github.com/milkv-duo/duo-pinmux) · [wiringX](https://github.com/milkv-duo/duo-wiringx) · [配件](https://github.com/milkv-duo/accessories) · [LVGL framebuffer 範例](https://github.com/milkv-duo/duo-lvgl-fb-demo)。
- 文件：[GPIO 與腳位複用](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [USB 攝影機](https://milkv.io/docs/duo/camera/usb) · [多媒體框架](https://milkv.io/docs/duo/application-development/multimedia)。
- Arduino：舊版 [Milk-V Arduino 核心程式庫](https://github.com/milkv-duo/duo-arduino) 已封存，該儲存庫目前建議使用 [Sophgo Arduino](https://github.com/kubuds/sophgo-arduino)。另有 [Duo Arduino 範例](https://github.com/milkv-duo/duo-arduino-examples)；使用前請確認開發板和核心程式庫的支援狀況。

## AI、電腦視覺與多媒體

- TDL 範例：[適用於 CV180X／原版 Duo 的 SDK V1](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [適用於 SG200X／Duo 256M 和 Duo S 的 SDK V1](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK V2 範例](https://github.com/milkv-duo/duo-tdl-examples)。
- TPU 與模型工具：[CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [TPU-MLIR 模型轉換](https://github.com/milkv-duo/tpu-mlir) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x)。
- [官方多媒體範例](https://github.com/milkv-duo/duo-multimedia-examples) · [TDL 模型部署](https://github.com/milkv-duo/duo-yolo-deployment)。
- [官方映像檔下載指南](https://milkv.io/docs/duo/getting-started/download)也列有依開發板分類的社群映像檔；請留意風險提示，並確認映像檔維護者及支援的硬體版本。

## 社群作業系統與學習資源

以下皆為獨立社群專案，並非官方韌體。相容性和維護狀態可能改變，安裝前請閱讀專案本身的文件。

- Linux 發行版：[Fedora 映像檔站](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/) · [Sophgo SG200X Debian](https://github.com/scpcom/sophgo-sg200x-debian) · [Ubuntu 映像檔建置器](https://github.com/ambraglow/milkv-duo-ubuntu) · [OpenWrt／VizOS 專案](https://github.com/Pillar1989/VizOS)。
- 建置系統與 RTOS：[Yocto／OpenEmbedded 層](https://github.com/kinsamanka/meta-milkv) · [Duo 次核心上的 Zephyr](https://github.com/kinsamanka/milkv-zephyros) · [SG2000／Duo S 上的 NuttX](https://github.com/lupyuen/nuttx-sg2000) · [RT-Thread CVitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) · [ThreadX 移植](https://github.com/saicogn/ThreadX-to-RISC-V64)。
- [Milk-V Duo 社群論壇](https://community.milkv.io/c/duo/5) · [Sophgo 論壇](https://forum.sophgo.com/) · [Milk-V Duo GitHub 組織](https://github.com/milkv-duo)。

## 貢獻與連結維護

如果連結失效、資源缺漏，或專案支援的開發板有所變更，歡迎提交 issue 或 pull request。請優先引用第一方文件和發行頁面，不要重新託管韌體。燒錄前請核對開發板型號、SoC、記憶體、儲存類型、啟動模式與映像檔說明；請先備份資料，並遵守安全的供電和接線方式。

[返回語言索引](README.md)
