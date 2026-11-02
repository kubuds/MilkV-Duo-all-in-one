# Milk-V Duo 系列資源總匯（Duo · Duo 256M · Duo S）

Milk-V Duo 系列所有能找到的資源，盡量都收在這一頁：官方文件與資料手冊、可直接下載的映像檔、SDK 與工具鏈、GitHub 與 Gitee 上的開源專案，以及 B 站和 YouTube 上真的用了這塊板子的影片。

這一頁不複製、不鏡像任何韌體和文件本體，只給出處和維護者。**社群映像檔與專案未經 Milk-V 測試或背書**，燒錄前請自己核對板型、SoC、記憶體、儲存媒體與發行說明。

> **先確認你手裡是哪塊板。** 三代產品並不是同一個東西：Duo 用 CV1800B（64 MB 記憶體），Duo 256M 用 SG2002（256 MB，多一個 Cortex-A53），Duo S 用 SG2000（512 MB，可選 Wi-Fi 6 / BT5 與可選 eMMC）。**原版 Duo 已被官方標記為停產（EOL）**，新專案建議直接上 256M 或 Duo S。

---

## 1. 板型與變體

| 型號 | SoC | 記憶體 | 儲存 | 無線 | 乙太網路 | TPU | 狀態 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Duo** | CVITEK CV1800B | 64 MB | microSD 或板載 SD NAND | 無 | 100M（PHY） | 0.5 TOPS@INT8 | 停產 EOL |
| **Duo 256M** | SG2002 | 256 MB | microSD 或板載 SD NAND | 無 | 100M（PHY） | 1.0 TOPS@INT8 | 販售中 |
| **Duo S** | SG2000 | 512 MB | microSD + 板上 eMMC 位置 | **可選** Wi-Fi 6 / BT5 | 100M（RJ45，支援 PoE HAT） | 0.5 TOPS@INT8 | 販售中 |
| **Duo Module 01**（核心板 + 評估板） | SG2000 | 512 MB | 8 GB eMMC 板載 | Wi-Fi 6 / BT5.4 板載 | 2× 100M | 0.5 TOPS@INT8 | 販售中 |

**Duo S 的四種組合**：eMMC 焊不焊 × Wi-Fi 模組焊不焊，共四種 SKU。買的時候看清楚商品頁寫的是哪一種。

映像檔**只按開機媒體區分**（`-sd` / `-emmc`），不按 Wi-Fi 區分 —— 官方 v2.0.1 的七個資產裡沒有任何帶 wifi 字樣的映像檔（見下表）。所以：

- 有 / 無 Wi-Fi 的 Duo S 刷同一份映像檔，無線功能靠的是板上有沒有那顆模組
- 有 eMMC 的板子既可以刷 `-sd` 從 TF 卡開機，也可以刷 `-emmc` 燒到板載儲存
- **沒有** eMMC 的板子只能走 TF 卡

---

## 2. 購買管道

淘寶「苦芽企業店」在售以下三款（商品頁需登入淘寶才能看到詳情，連結本身實測回傳 200）：

- **Milk-V Duo 256M**（SG2002，256 MB，無 Wi-Fi）：https://item.taobao.com/item.htm?id=842972320584&skuId=5661357677549
- **Milk-V Duo S 基礎版**（SG2000，512 MB，無 Wi-Fi、無 eMMC）：https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544644
- **Milk-V Duo S Wi-Fi 版**（SG2000，512 MB，含 Wi-Fi 6 / BT，無 eMMC）：https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544645

Duo S 那兩個是**同一個商品的兩個 SKU**（`id` 相同、`skuId` 不同），下單時看清 SKU 名稱裡有沒有 Wi-Fi；兩款都沒有 eMMC，要板載儲存得另找含 eMMC 的版本。原版 Duo（CV1800B）已停產，不放購買連結。

這是全頁唯一帶商業性質的部分，其餘內容只指向上游出處。

---

## 3. 官方文件、資料手冊與硬體資料

**文件站：逐頁索引**

- 起點：[Duo 系列概覽與規格比較](https://milkv.io/docs/duo/overview)（四款產品完整規格表，也是 EOL 聲明的出處） · [文件站首頁](https://milkv.io/docs/duo/getting-started)
- 各板指南：[Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos) · [Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- 上電與燒錄：[啟動系統](https://milkv.io/docs/duo/getting-started/boot) · [首次連線與 USB 網路](https://milkv.io/docs/duo/getting-started/setup) · [映像檔下載總表](https://milkv.io/docs/duo/getting-started/download) · [Buildroot SDK 建置](https://milkv.io/docs/duo/getting-started/buildroot-sdk)
- 雙核與低階：[輔助核 8051 開發](https://milkv.io/docs/duo/getting-started/8051core) · [RTOS 小核開發](https://milkv.io/docs/duo/getting-started/rtoscore) · [Arduino 支援](https://milkv.io/docs/duo/getting-started/arduino) · [低階開發](https://milkv.io/docs/duo/low-level-dev)（[MIPI DSI](https://milkv.io/docs/duo/low-level-dev/mipi-dsi)）
- 應用開發：[總覽](https://milkv.io/docs/duo/application-development) · [GPIO sysfs](https://milkv.io/docs/duo/application-development/gpio-sysfs) · [腳位複用](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [pinpong](https://milkv.io/docs/duo/application-development/pinpong) · [多媒體框架](https://milkv.io/docs/duo/application-development/multimedia)
- 攝影機：[USB 攝影機](https://milkv.io/docs/duo/camera/usb) · [GC2083 感測器](https://milkv.io/docs/duo/camera/gc2083) · [ISP tuning](https://milkv.io/docs/duo/camera/tuning)
- TPU 與 TDL：[TPU 簡介](https://milkv.io/docs/duo/application-development/tpu/tpu-introduction) · [TDL SDK 簡介](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-introduction) · YOLO：[v5](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov5) · [v8](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov8) · [v11](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo11) · [v12](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo12) · [人臉偵測](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-face-detection) · [行人偵測](https://milkv.io/docs/duo/application-development/tdl-sdk/pedestrian-detection) · [人寵偵測](https://milkv.io/docs/duo/application-development/tdl-sdk/yolov8-person-pets-detection)
- IO 擴充板：[IO Board 總覽](https://milkv.io/docs/duo/io-board) · [Duo S PoE HAT](https://milkv.io/docs/duo/io-board/duos-poe-hat) · [USB 乙太網路 IO 板](https://milkv.io/docs/duo/io-board/usb-ethernet-iob)
- 官方整理的資源與生態進展：[實用資源總表](https://milkv.io/docs/duo/useful-resources) · [主線核心支援狀態](https://milkv.io/docs/duo/resources/mainline) · [上游支援現況](https://milkv.io/docs/duo/resources/upstream-status) · [MMF 多媒體框架](https://milkv.io/docs/duo/resources/mmf) · [OpenCV Mobile](https://milkv.io/docs/duo/resources/opencv-mobile) · [SPILVGL](https://milkv.io/docs/duo/resources/spilvgl) · [Visuino](https://milkv.io/docs/duo/resources/visuino) · [xyzdims 筆記](https://milkv.io/docs/duo/resources/xyzdims)
- [文件站原始碼](https://github.com/milk-v/milkv.io) —— 文件有錯或想補翻譯，往這裡提 PR

**產品頁**

- [Duo（系列頁）](https://milkv.io/duo) · [Duo S](https://milkv.io/duo-s) · [Duo Module 01](https://milkv.io/duo-module-01)
- Duo 256M 沒有獨立的商品頁，規格見系列頁與[文件](https://milkv.io/docs/duo/getting-started/duo256m)

**硬體檔案與晶片手冊**

- [duo-files](https://github.com/milkv-duo/duo-files) —— 官方板級檔案總庫：電路圖、資料手冊、機構圖、絲印
- 電路圖：[Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)
- 資料手冊：[CV1800B/CV1801B 英文](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf)（[中文](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf)） · [SG2002 中文](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 中文](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 TRM 英文](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)
- [Sophgo 文件發布頁](https://github.com/sophgo/sophgo-doc/releases) —— 上游晶片文件的正式出口

---

## 4. 官方映像檔與燒錄

官方映像檔全部基於 Buildroot，分 V1 / V2 兩條線。**64 MB 的 Duo 建議用 V1**（V2 的 AI 範例在 64 MB 上跑不動）；Duo 256M 與 Duo S 用 V2。

### V2（推薦給 Duo 256M / Duo S）· [v2.0.1，2025-05-30](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)

| 資產檔案 | 板型 | 開機媒體 | C 函式庫 / 架構 |
| --- | --- | --- | --- |
| `milkv-duo-musl-riscv64-sd_v2.0.1.img.zip` | Duo | TF 卡 | musl / riscv64 |
| `milkv-duo256m-musl-riscv64-sd_v2.0.1.img.zip` | Duo 256M | TF 卡 | musl / riscv64 |
| `milkv-duo256m-glibc-arm64-sd_v2.0.1.img.zip` | Duo 256M | TF 卡 | glibc / arm64（走 A53） |
| `milkv-duos-musl-riscv64-sd_v2.0.1.img.zip` | Duo S | TF 卡 | musl / riscv64 |
| `milkv-duos-glibc-arm64-sd_v2.0.1.img.zip` | Duo S | TF 卡 | glibc / arm64（走 A53） |
| `milkv-duos-musl-riscv64-emmc_v2.0.1.zip` | Duo S（需 eMMC） | 板載 eMMC | musl / riscv64 |
| `milkv-duos-glibc-arm64-emmc_v2.0.1.zip` | Duo S（需 eMMC） | 板載 eMMC | glibc / arm64 |

### V1 · [v1.1.4，2024-11-22](https://github.com/milkv-duo/duo-buildroot-sdk/releases)

| 資產檔案 | 板型 | 開機媒體 |
| --- | --- | --- |
| `milkv-duo-sd-v1.1.4.img.zip` | Duo | TF 卡 |
| `milkv-duo256m-sd-v1.1.4.img.zip` | Duo 256M | TF 卡 |
| `milkv-duos-sd-v1.1.4.img.zip` | Duo S | TF 卡 |
| `milkv-duos-emmc-v1.1.4.zip` | Duo S（需 eMMC） | 板載 eMMC |
| `arduino-milkv-duo-sd-v1.1.4.img.zip` 等 4 個 | 三款板 | 同名規則，Arduino 預置映像檔 |

### 燒錄要點

- TF 卡映像檔：解壓縮後用 balenaEtcher / `dd` 寫入，插卡上電即可；**預設開啟 ssh、預設開啟 USB-NCM 網路卡，root 密碼 `milkv`**
- eMMC 映像檔：**不是** TF 卡映像檔的寫法。Duo S 要按住 Recovery 鍵、用 Type-C 傳輸線連電腦，再用 CVITEK 的 `usb_dl.exe`（Windows）或 `CviBurn` 工具從 USB 燒寫；燒錄前務必拔掉 TF 卡
- Duo S 有 **ARM / RISC-V 啟動切換開關**，韌體與開關不一致時起不來；序列埠日誌首字元 `C` 是從 RISC-V 啟動、`B` 是從 ARM 啟動
- Duo S 的 Type-C（USB-NCM）與 Type-A（USB HOST）**不能同時用**，靠 `/mnt/system/usb.sh` 符號連結切換

---

## 5. 第三方映像檔（社群維護，依板型分類）

官方下載頁有一份[第三方映像檔表](https://milkv.io/docs/duo/getting-started/download)，這裡依板型攤平，方便直接點。

### Duo（CV1800B，64 MB）

- [Fedora 41 映像站](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo/images/latest/) —— Fedora-V Force 維護，跟著上游滾動
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) —— 映像檔建置腳本，也能編 Duo 256M 的
- [Debian / Ubuntu 映像檔建置器](https://github.com/logicethos/Milk-V_Duo_Linux2SD) —— 自己出映像檔用這個
- [Arch Linux](https://community.milkv.io/t/arch-linux-on-milkv-duo-milkv-duo-arch-linux/329) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1) · [Debian 完整映像檔](https://community.milkv.io/t/milkv-duo-duo-debian-full-7z-519m-download/862)
- [OpenWrt / VizOS](https://github.com/Pillar1989/VizOS) · [Zephyr（輔助核）](https://github.com/kinsamanka/milkv-zephyros) · [Yocto 層](https://github.com/kinsamanka/meta-milkv)
- [RT-Thread cvitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek)（[RISC-V RT-Thread 程式設計指南](https://riscv-rtthread-programming-manual.readthedocs.io/zh-cn/latest/)） · [ThreadX 移植](https://github.com/saicogn/ThreadX-to-RISC-V64)

### Duo 256M（SG2002）

- [Fedora 41 映像站](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo256M/images/latest/)
- [Debian（Fishwaldo / sophgo-sg200x-debian）](https://github.com/Fishwaldo/sophgo-sg200x-debian/releases/tag/v1.2.0)
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) · [Arch Linux](https://community.milkv.io/t/debian-arch-linux-on-milkv-duo-256m-milkv-duo-256m-debian-arch-linux/1110) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1)

### Duo S（SG2000）

- [Fedora 41 映像站](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/DuoS/images/latest/) —— 預設帳號 `root` / 密碼 `riscv`
- [Debian（scpcom）](https://github.com/scpcom/sophgo-sg200x-debian/releases) —— `root`/`rv` 與 `debian`/`rv` 兩套帳號
- [NuttX（lupyuen）](https://github.com/lupyuen/nuttx-sg2000/releases) —— 在 Duo S 上跑 NuttX 的現成映像檔

---

## 6. SDK、工具鏈與範例

- SDK 原始碼：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [主機端工具鏈](https://github.com/milkv-duo/host-tools)
- [duo-examples](https://github.com/milkv-duo/duo-examples) —— 官方 C/C++ 範例： [GPIO 閃燈](https://github.com/milkv-duo/duo-examples/tree/main/blink) · [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c) · [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) · [週邊驅動操作指南（PDF）](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux)（腳位複用） · [duo-wiringx](https://github.com/milkv-duo/duo-wiringx)（wiringX 移植） · [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo)（LVGL framebuffer） · [duo-accessories](https://github.com/milkv-duo/accessories)（官方配件）
- Arduino：[已封存的官方核心程式庫](https://github.com/milkv-duo/duo-arduino)（儲存庫已指向 [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)） · [Duo Arduino 範例](https://github.com/milkv-duo/duo-arduino-examples)
- SoC 端工具：[CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x) · [TPU-MLIR 模型轉換](https://github.com/milkv-duo/tpu-mlir)
- TDL（深度學習範例）：[CV180X / Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SG200X / Duo 256M & Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK V2 版 TDL 範例](https://github.com/milkv-duo/duo-tdl-examples) · [YOLO 部署](https://github.com/milkv-duo/duo-yolo-deployment)
- 多媒體：[duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples)

---

## 7. 官方組織、社群與交流

- [milkv-duo GitHub 組織](https://github.com/milkv-duo) —— 官方 SDK、範例、硬體檔案都在這裡
- [Milk-V 社群 Duo 分類](https://community.milkv.io/c/duo/5) —— 提問與經驗分享的主場
- [Duo Module 01 評估板文件](https://milkv.io/docs/duo/getting-started/duo-module-01)
- 原 `forum.sophgo.com` 已無法存取（2026-10 實測連線失敗），晶片端資料改從 [sophgo-doc](https://github.com/sophgo/sophgo-doc/releases) 取

---

## 8. 影片：嗶哩嗶哩（50 支）

全部逐條核對過頁面存在（HTTP 200）且標題/簡介確實指向 Duo 系列；觀看次數是 2026-10-31 的快照，只作熱度參考。

**東東老師系列（eastdong）—— 最適合從零開始**

- 《零壓力上手 RISC-V：東東老師帶你玩轉 milk-v duo》01. RVOS on Duo — [BV1vm421E7R6](https://www.bilibili.com/video/BV1vm421E7R6/) · 9578
- 02. RT-Thread on Duo — [BV1ym411z7Qo](https://www.bilibili.com/video/BV1ym411z7Qo/) · 3558
- 04. Camera 和 YOLOv5 圖像識別 — [BV1mt421A7tL](https://www.bilibili.com/video/BV1mt421A7tL/) · 2972
- 05. TPU 使用 — [BV1Wi421Q7b4](https://www.bilibili.com/video/BV1Wi421Q7b4/) · 2171
- 06. 完結（補講 Duo 256M 的新變化）— [BV1Fx4y1W7x9](https://www.bilibili.com/video/BV1Fx4y1W7x9/) · 2212

**苦芽科技 —— Duo S 官方課程的完整鏈路**

- 00. 認識 Milk-V Duo S — [BV1PNDoYeEpT](https://www.bilibili.com/video/BV1PNDoYeEpT/) · 2307
- 01. Windows 下安裝及啟動 — [BV1u3DYYGES7](https://www.bilibili.com/video/BV1u3DYYGES7/) · 376
- macOS 下安裝及啟動 — [BV1U5qqYUEAm](https://www.bilibili.com/video/BV1U5qqYUEAm/) · 233
- 02. SPI 演示 — [BV1vYqHYnE8G](https://www.bilibili.com/video/BV1vYqHYnE8G/) · 186

**入門與評測**

- 35 塊帶 TPU、1GHz 的 Linux 開發板，還玩啥樹莓派（科學中國）— [BV19h4y1t7Ct](https://www.bilibili.com/video/BV19h4y1t7Ct/) · 1.9 萬
- 映像檔燒寫教程：帶 TPU 的 RISC-V Linux 板（斑梨電子）— [BV1uM4y1n763](https://www.bilibili.com/video/BV1uM4y1n763/) · 9098
- 能跑輕量 AI 的最便宜 RISC-V Linux 開發板？Duo 64M（撿個肥仔上戰場）— [BV11w411j71u](https://www.bilibili.com/video/BV11w411j71u/) · 9365
- RISC-V 峰會現場 Duo 開箱（半導體都市隸人 Ayla）— [BV1oh4y1K724](https://www.bilibili.com/video/BV1oh4y1K724/) · 8415
- 野生的開發板效能再強又有何用，軟體適配稀爛：Duo 256M 嘗試 Arduino 徹底失敗（沈潔 Eacc）— [BV1sZZHYdEPP](https://www.bilibili.com/video/BV1sZZHYdEPP/) · 8026 ← **負面評測，值得看**
- 35 元的 milkv-duo Linux 單片機還要啥自行車（開源社群的二掌櫃）— [BV1tM4y1Y7kh](https://www.bilibili.com/video/BV1tM4y1Y7kh/) · 2792
- 學習 RISC-V 能跑 Debian & Linux 的最便宜開發板之一（蘭雅 sRGB）— [BV1XQ4y1E7Tj](https://www.bilibili.com/video/BV1XQ4y1E7Tj/) · 3054
- 好玩！RISC-V duo256M 開發板測玩（蘭雅 sRGB）— [BV1Zw411V7bK](https://www.bilibili.com/video/BV1Zw411V7bK/) · 2257
- 麻雀雖小五臟俱全：超高性價比開發板 Milk-V Duo S（qinyunti）— [BV1hyKmzJEw5](https://www.bilibili.com/video/BV1hyKmzJEw5/) · 664

**環境建置與燒錄**

- Linux 下開發環境建置（future 待續）— [BV1B8411m7jR](https://www.bilibili.com/video/BV1B8411m7jR/) · 3192
- 燒寫 Linux 系統 + USB 虛擬 RNDIS 網路卡登入（蘭雅 sRGB）— [BV1G14y1k7V4](https://www.bilibili.com/video/BV1G14y1k7V4/) · 1062
- Duo-debian 初體驗（蘭雅 sRGB）— [BV11c411o76T](https://www.bilibili.com/video/BV11c411o76T/) · 3416
- Duo 簡介和開發環境建置（誰說現在是冬天呢）— [BV1PF411S7To](https://www.bilibili.com/video/BV1PF411S7To/) · 1959
- Buildroot SDK 簡介和編譯映像檔的方法（誰說現在是冬天呢）— [BV1xc411s7qk](https://www.bilibili.com/video/BV1xc411s7qk/) · 462
- 安裝 Hyper-V & 設定 Docker 開發環境（_1dentity）— [BV1nC4y117WS](https://www.bilibili.com/video/BV1nC4y117WS/) · 1826

**週邊、顯示與雙核**

- LVGL 庫實戰教程 — 劉文濤（群芯閃耀），lazyparser 頻道 — [BV1Mp421m7qJ](https://www.bilibili.com/video/BV1Mp421m7qJ/) · 966
- 透過 SPI 驅動 ST7789V 跑 LVGL（誰說現在是冬天呢）— [BV1gLeueWEWr](https://www.bilibili.com/video/BV1gLeueWEWr/) · 2239
- Duo 256M 基於 TinyDRM 驅動 ST7796s 4.0 吋螢幕並移植 LVGL 8.3（二掌櫃）— [BV1Tv421k71W](https://www.bilibili.com/video/BV1Tv421k71W/) · 1230
- USB & Ethernet IO-Board 簡介和使用方法（誰說現在是冬天呢）— [BV1Ga4y1Z7oM](https://www.bilibili.com/video/BV1Ga4y1Z7oM/) · 1096
- 透過大核控制小核點亮 LED（誰說現在是冬天呢）— [BV1nH4y1y7CM](https://www.bilibili.com/video/BV1nH4y1y7CM/) · 1057
- 用 Duo 驅動 DF9GMS 微型舵機（誰說現在是冬天呢）— [BV1Dj411E7yD](https://www.bilibili.com/video/BV1Dj411E7yD/) · 571
- Duo S 硬體解碼 MP4 並在 LCD 上播放（一隻御坂美琴）— [BV1ktvseWEhr](https://www.bilibili.com/video/BV1ktvseWEhr/) · 519

**系統移植**

- 在 Duo 上執行 ThreadX（誰說現在是冬天呢）— [BV1yi421C7SK](https://www.bilibili.com/video/BV1yi421C7SK/) · 419
- 在小核上執行 Zephyr OS（誰說現在是冬天呢）— [BV1uK421Y7x9](https://www.bilibili.com/video/BV1uK421Y7x9/) · 435
- 在 Duo 256M 上執行 Arch Linux（誰說現在是冬天呢）— [BV1j8yyYTEp2](https://www.bilibili.com/video/BV1j8yyYTEp2/) · 1274
- 在 Duo S 上啟動 NuttX（悲傷的黑山羊）— [BV1RMUeYjELe](https://www.bilibili.com/video/BV1RMUeYjELe/) · 75
- 羅君：Duo 的 UniProton 適配（PLCT 內部報告）（lazyparser）— [BV1RD421G773](https://www.bilibili.com/video/BV1RD421G773/) · 903
- Duo S 啟動！（誰說現在是冬天呢）— [BV1Bm421N72y](https://www.bilibili.com/video/BV1Bm421N72y/) · 564
- 使用 Wi-Fi 連接 Duo S（誰說現在是冬天呢）— [BV11r421T7Sk](https://www.bilibili.com/video/BV11r421T7Sk/) · 318
- 在 Duo S 上部署 Caddy 伺服器（誰說現在是冬天呢）— [BV1poBzYQEoC](https://www.bilibili.com/video/BV1poBzYQEoC/) · 214
- Duo 256M 部署相簿檔案管理器和部落格筆記（蘭雅 sRGB）— [BV1cC4y1e7uk](https://www.bilibili.com/video/BV1cC4y1e7uk/) · 1455
- GameOS 開發日常：自製系統上跑 Doom、用「小電視」按 BV 號播放 B 站影片（我的大可樂呢；作者未標板卡型號）— [BV1iZx46BEV7](https://www.bilibili.com/video/BV1iZx46BEV7/) · 38

**AI / 視覺**

- Duo 256M 鎖頭測試：官方腳本跑人臉偵測並拉流到電腦（Judehahh）— [BV1w4421A7A2](https://www.bilibili.com/video/BV1w4421A7A2/) · 3.6 萬
- 基於 Duo 和 YOLOv5 的目標偵測（誰說現在是冬天呢）— [BV1iG41197qa](https://www.bilibili.com/video/BV1iG41197qa/) · 1211
- 基於 TDL SDK 實現 YOLOv5 目標偵測（誰說現在是冬天呢）— [BV1Vw4m1U71C](https://www.bilibili.com/video/BV1Vw4m1U71C/) · 446
- YOLOv8 目標偵測（誰說現在是冬天呢）— [BV1AWqUYGEaS](https://www.bilibili.com/video/BV1AWqUYGEaS/) · 269
- 測試透過 VLC 顯示 CAM-GC2083 攝影機畫面（誰說現在是冬天呢）— [BV188411v7tc](https://www.bilibili.com/video/BV188411v7tc/) · 1159
- Duo S 執行故事機 baby llama2（誰說現在是冬天呢）— [BV1dn4y197UW](https://www.bilibili.com/video/BV1dn4y197UW/) · 621
- Duo S 上用 TDL SDK 部署人臉偵測（誰說現在是冬天呢）— [BV1AM4m1m7fe](https://www.bilibili.com/video/BV1AM4m1m7fe/) · 522
- YOLO 實戰：車牌識別效果展示（誰說現在是冬天呢）— [BV1uYAHerEbL](https://www.bilibili.com/video/BV1uYAHerEbL/) · 1272
- 【软硬件开源】TideSense双目VIO（单三拍）— [BV1EcnG6XESF](https://www.bilibili.com/video/BV1EcnG6XESF/) · 15376

---

## 9. 影片：YouTube（37 支）

國外站點，走代理才能開啟；同樣逐條核對過頁面存在且內容真的涉及 Duo。

**評測與上手**

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

**入門、燒錄與網路**

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

**週邊與 AI**

- Anton Maltsev — Is it good for computer vision? How to start a neural network on it — [dkIVDOd_Fa4](https://www.youtube.com/watch?v=dkIVDOd_Fa4) · Duo
- Mark Birss — Milk-V Duo USB input ST7789 240×240 SPI display — [Swo-zJ6brQI](https://www.youtube.com/watch?v=Swo-zJ6brQI) · Duo
- Sonny Cruz — I²C demo, source in the description — [85uglOz48Pg](https://www.youtube.com/watch?v=85uglOz48Pg) · Duo
- Sonny Cruz — RC servo demo using PWM — [1u2LZJWPtNU](https://www.youtube.com/watch?v=1u2LZJWPtNU) · Duo
- Leigh — Duo + CAM-GC2083: fix RTSP streaming to VLC — [PjiUDsoWCvo](https://www.youtube.com/watch?v=PjiUDsoWCvo) · Duo
- Muhammad Yunus — YOLOX inference on Duo S using TDL SDK + VPSS — [wzUTGK4TuqA](https://www.youtube.com/watch?v=wzUTGK4TuqA) · Duo S

**系統移植與整機專案**

- Muhammad Yunus — RT-Thread on Duo S: the best RTOS for cheap RISC-V? — [WjWM5YoAq-c](https://www.youtube.com/watch?v=WjWM5YoAq-c) · Duo S
- RISC-V Developers — S1E2 Enjoy RISC-V with Milk-V Duo: RT-Thread — [B7EXWE6l9xE](https://www.youtube.com/watch?v=B7EXWE6l9xE) · Duo
- Chris McDonough — NixOS 71: NixOS on RISC-V (Milk-V Duo / Duo 256M) — [-ydXjEWUlGE](https://www.youtube.com/watch?v=-ydXjEWUlGE) · Duo 系列
- admin ka — Running Ubuntu glibc 24.04.4 on the Duo 256M — [0Dqbdtjt8Ro](https://www.youtube.com/watch?v=0Dqbdtjt8Ro) · Duo 256M
- 福田重夫 — Running Linux on the Duo 256M (RISC-V + ARM) — [Ga3HX-d8GHQ](https://www.youtube.com/watch?v=Ga3HX-d8GHQ) · Duo 256M
- Nch-Lab — Milk-V Duo 256M を買ったので Linux を動かしてみる — [tcAqYCwbqeU](https://www.youtube.com/watch?v=tcAqYCwbqeU) · Duo 256M
- Mark Birss — Duo 256 CyberDeck LoRa communicator (TLMVC) — [9qOJ3fKwfC0](https://www.youtube.com/watch?v=9qOJ3fKwfC0) · Duo 256M

---

## 10. GitHub 開源專案

依用途分類。star 數與最後提交日期是 2026-10-31 的快照，會變；帶「官方」的是 milkv-duo 組織下的儲存庫。

**官方 SDK、韌體與工具**

- [duo-buildroot-sdk](https://github.com/milkv-duo/duo-buildroot-sdk) — 官方 Buildroot SDK V1（Duo/CV1800B）· 495★
- [duo-buildroot-sdk-v2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) — 官方 SDK V2（Duo 256M / Duo S，SG200x）· 154★
- [duo-examples](https://github.com/milkv-duo/duo-examples) — 官方 C/C++ 週邊範例 · 159★
- [duo-sdk](https://github.com/milkv-duo/duo-sdk) — 主機端交叉編譯 SDK（duo-app-sdk）· 5★
- [host-tools](https://github.com/milkv-duo/host-tools) — 預編譯主機 gcc 工具鏈 · 9★
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) — 腳位複用設定工具 · 7★
- [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) — wiringX 的 Duo 移植 · 11★
- [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples) — 多媒體鏈路範例 · 6★
- [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) — LVGL on framebuffer · 10★
- [duo-arduino](https://github.com/milkv-duo/duo-arduino) — 官方 Arduino 支援（已封存，指向 [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)）· 20★
- [duo-arduino-examples](https://github.com/milkv-duo/duo-arduino-examples) — Arduino 範例
- [duo-tdl-examples](https://github.com/milkv-duo/duo-tdl-examples) — SDK V2 的 TDL 範例 · 13★
- [cvitek-tdl-sdk-sg200x](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) — SG200x TDL-SDK 範例 · 30★
- [cvitek-tdl-sdk-cv180x](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) — CV180x TDL-SDK 範例
- [tpu-sdk-sg200x](https://github.com/milkv-duo/tpu-sdk-sg200x) — SG200x TPU SDK · 5★
- [tpu-sdk-cv180x](https://github.com/milkv-duo/tpu-sdk-cv180x) — CV180x TPU SDK
- [tpu-mlir](https://github.com/milkv-duo/tpu-mlir) — TPU-MLIR 模型轉換 · 9★
- [duo-yolo-deployment](https://github.com/milkv-duo/duo-yolo-deployment) — YOLO 部署範例
- [milkv-duo-linux](https://github.com/milkv-duo/milkv-duo-linux) — 官方核心樹 · 1★
- [milkv-duo-u-boot](https://github.com/milkv-duo/milkv-duo-u-boot) — 官方 U-Boot 樹 · 4★
- [milkv-duo-opensbi](https://github.com/milkv-duo/milkv-duo-opensbi) — 官方 OpenSBI 移植 · 2★
- [milkv-duo-smallcore-freertos](https://github.com/milkv-duo/milkv-duo-smallcore-freertos) — 小核 C906 跑 FreeRTOS · 17★
- [duo-8051](https://github.com/milkv-duo/duo-8051) — 內建 8051 核範例 · 8★

**官方文件與硬體資料**

- [duo-files](https://github.com/milkv-duo/duo-files) — 電路圖、資料手冊、機構圖總庫 · 203★
- [accessories](https://github.com/milkv-duo/accessories) — 官方配件資料 · 14★
- [milkv.io](https://github.com/milk-v/milkv.io) — 官網與文件站原始碼 · 4★
- [sophgo-doc](https://github.com/sophgo/sophgo-doc) — 上游晶片文件發布口
- [datasheet-en](https://github.com/taspenwall/datasheet-en) — SG2002 資料手冊英譯 · 5★
- [riscv-rtthread-programming-manual](https://github.com/flyingcys/riscv-rtthread-programming-manual) — 《RISC-V 編程指南：基於 RT-Thread 與 Milk-V Duo》配套程式碼 · 10★
- [MilkV-Duo-Resources](https://github.com/robtech21/MilkV-Duo-Resources) — 資源合集
- [johandevlabs/milk-v-duo-s-notes](https://github.com/johandevlabs/milk-v-duo-s-notes) — Duo S 折騰筆記 · 5★
- [Mirrorium227/MilkvDuo_Basic](https://github.com/Mirrorium227/MilkvDuo_Basic) — CV1800B 除錯與範例
- [imagineeeinc/things-on-milkv-duo](https://github.com/imagineeeinc/things-on-milkv-duo) — 用 Nim 玩 Duo

**開機引導與韌體**

- [u-boot/u-boot](https://github.com/u-boot/u-boot) — 主線已含 `board/sophgo/milkv_duo` · 5309★
- [sg_boot](https://github.com/platform-system-interface/sg_boot) — Rust 寫的 CV1800B/SG200x 開機引導器 · 12★
- [gtxzsxxk/milkv-duo-firmware-fsbl](https://github.com/gtxzsxxk/milkv-duo-firmware-fsbl) — FSBL 實作 · 6★
- [Taumille/uboot-milkv](https://github.com/Taumille/uboot-milkv) — 已消失的官方 u-boot 儲存庫的社群 fork

**發行版與系統映像檔**

- [armbian/build](https://github.com/armbian/build) — 已含 `milkv-duos-riscv` / `milkv-duos-arm` 板型 · 5499★
- [Fishwaldo/sophgo-sg200x-debian](https://github.com/Fishwaldo/sophgo-sg200x-debian) — 最活躍的 SG200x Debian 建置 · 219★
- [ambraglow/milkv-duo-ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) — Duo Ubuntu · 68★
- [olivaw448/milkv-duo-s-512mb-debian](https://github.com/olivaw448/milkv-duo-s-512mb-debian) — Duo S 512MB Debian（含 WiFi/藍牙/USB host/攝影機）· 11★
- [eznix86/milkv-duo-s-alpine-linux](https://github.com/eznix86/milkv-duo-s-alpine-linux) — Duo S Alpine · 9★
- [CrocNet/duo-docker-builder](https://github.com/CrocNet/duo-docker-builder) — Docker 建置 Ubuntu 映像檔 · 9★
- [logicethos/Milk-V_Duo_Linux2SD](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — 建置並直接寫卡 · 21★
- [RawFish69/ubuntu-milkv-duos](https://github.com/RawFish69/ubuntu-milkv-duos) — Duo S Ubuntu 22.04
- [draftbottle/Milkv-duo-openwrt](https://github.com/draftbottle/Milkv-duo-openwrt) — 基於 VizOS 的 OpenWrt
- [Pillar1989/VizOS](https://github.com/Pillar1989/VizOS) — OpenWrt / VizOS 專案
- [georgewhewell/nixos-nanokvm](https://github.com/georgewhewell/nixos-nanokvm) — SG2000/SG2002 的 NixOS 設定
- [kinsamanka/meta-milkv](https://github.com/kinsamanka/meta-milkv) — Yocto / OpenEmbedded 層

**RTOS 與裸機**

- [RT-Thread/rt-thread](https://github.com/RT-Thread/rt-thread) — `bsp/cvitek` 含 milkv-duo / duo256m / duos · 12318★
- [lupyuen/nuttx-sg2000](https://github.com/lupyuen/nuttx-sg2000) — Duo S 上的 NuttX · 45★
- [kinsamanka/milkv-zephyros](https://github.com/kinsamanka/milkv-zephyros) — 小核 Zephyr · 35★
- [saicogn/ThreadX-to-RISC-V64](https://github.com/saicogn/ThreadX-to-RISC-V64) — ThreadX 移植 · 8★
- [Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK](https://github.com/Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK) — 不用 SDK 的雙核裸機 · 11★
- [zuki/xv6-milkv-duo](https://github.com/zuki/xv6-milkv-duo) — xv6 on Duo · 7★
- [jiegegena/milkv-sg2002-xv6](https://github.com/jiegegena/milkv-sg2002-xv6) — xv6 on SG2002
- [Lam920/xv6-cv1800b](https://github.com/Lam920/xv6-cv1800b) — xv6 on CV1800B
- [rota1001/milkv-baremetal-toolkit](https://github.com/rota1001/milkv-baremetal-toolkit) — 一鍵產生裸機映像檔 · 8★
- [PeterForth/MILKV-FORTH](https://github.com/PeterForth/MILKV-FORTH) — Duo 上的 Forth · 8★
- [xingrz/milkv-duo-zephyr-mailbox-example](https://github.com/xingrz/milkv-duo-zephyr-mailbox-example) — Zephyr 與 Linux 的 mailbox 通訊
- [DivByDiamond/OnyxOS](https://github.com/DivByDiamond/OnyxOS) — 以 Rust 撰寫的 RISC-V 單體內核（整機約 272 KB，含 C++ 引導器與自舉 C 編譯器），內核帶 SG2000 平台驅動，目標板包括 Duo S · 0★

**工具鏈與建置環境**

- [aidancrowther/Milk-V-Duo-Docker-Compile](https://github.com/aidancrowther/Milk-V-Duo-Docker-Compile) — 預裝工具鏈的 Docker 映像檔 · 24★
- [Tosainu/docker-milkv-duo-linux](https://github.com/Tosainu/docker-milkv-duo-linux) — 容器化建置 Linux
- [boberace/milkv_duo_dc](https://github.com/boberace/milkv_duo_dc) — VS Code Dev Container
- [kitnerboy/milkv-duo-buildroot](https://github.com/kitnerboy/milkv-duo-buildroot) — 主線風格 Buildroot BSP

**驅動程式與週邊**

- [hexdump0815/linux-cvitek-cv18xx-kernel](https://github.com/hexdump0815/linux-cvitek-cv18xx-kernel) — 社群核心樹（多個映像檔的核心來源）
- [ret7020/CVI_HW_OpenCV](https://github.com/ret7020/CVI_HW_OpenCV) — 用 NPU 加速的 OpenCV 移植 · 7★
- [pavelanni/gpiod-milkvduo](https://github.com/pavelanni/gpiod-milkvduo) — libgpiod 用法 · 3★
- [Satharus/I2C-WiringX-Milk-V](https://github.com/Satharus/I2C-WiringX-Milk-V) — wiringX 操作 I²C · 2★
- [KuLvo/milk-v_duo_oled_driver](https://github.com/KuLvo/milk-v_duo_oled_driver) — 0.96 吋 OLED 驅動 · 3★
- [queenkjuul/aic8800-milkv-duos](https://github.com/queenkjuul/aic8800-milkv-duos) — AIC8800 WiFi+BT 適配
- [GrootLiu/milkv-duo-rtl8723du](https://github.com/GrootLiu/milkv-duo-rtl8723du) — RTL8723DU WiFi 移植
- [Tactical-TV-Remote/infrared_milkv](https://github.com/Tactical-TV-Remote/infrared_milkv) — 紅外線收發（Rust）
- [harshareddy1611/milkv-duo-s-baremetal-drivers](https://github.com/harshareddy1611/milkv-duo-s-baremetal-drivers) — Duo S 裸機 GPIO/UART
- [wanghengZzz/Milkv-Duo-FreeRTOS-DMA](https://github.com/wanghengZzz/Milkv-Duo-FreeRTOS-DMA) — FreeRTOS DMA HAL

**專案實作**
- [tidesense](https://github.com/HumpbackLab/tidesense) — 基於 SG2002 的雙目視覺慣性里程計（自研板，不是 Duo 256M）：OV9281 全域快門雙目 + SC7U22 IMU，SchurVINS 做 20 Hz 視覺校正 / 200 Hz 預測，附 OpenVINS 比較、標定與資料集工具；VIO 跑在 Cortex-A53 上，純 SD 開機。硬體依 CC BY-NC-SA 4.0 開源（連結見儲存庫 README）· 142★

- [pavelanni/milkv-duo-experiments](https://github.com/pavelanni/milkv-duo-experiments) — Go 寫的實驗集 · 27★
- [driver1998/DiscEmu](https://github.com/driver1998/DiscEmu) — 用 Duo 做 CD-ROM 模擬器 · 11★
- [0x1iii1ii/Pwn-V-Duo](https://github.com/0x1iii1ii/Pwn-V-Duo) — PPPwn 漏洞利用移植 · 6★
- [aceraoc/MilkV-Duo_TPU](https://github.com/aceraoc/MilkV-Duo_TPU) — TPU 推論實例 · 8★
- [xmdjy/milkv-car](https://github.com/xmdjy/milkv-car) — 基於 Duo 的智慧小車
- [Arielfoever/milkv-duo-yolo11](https://github.com/Arielfoever/milkv-duo-yolo11) — YOLO11 部署
- [Basicname/SG200x_GC2083_Yolov8_11](https://github.com/Basicname/SG200x_GC2083_Yolov8_11) — 單檔部署 YOLOv8/11 + GC2083
- [chius-me/globi-v](https://github.com/chius-me/globi-v) — Duo S 上的視障輔助視覺系統
- [f3jry/milkv-duo-xmrsigner](https://github.com/f3jry/milkv-duo-xmrsigner) — Monero 冷錢包移植到 Duo
- [sdwood68/MilkV_Duo_S_Camera](https://github.com/sdwood68/MilkV_Duo_S_Camera) — 可接 Frigate / Home Assistant 的攝影機節點
- [ar90n/ptp-server-milkv-duos](https://github.com/ar90n/ptp-server-milkv-duos) — PTP 主時鐘伺服器
- [avalitan/MilkV-Duo-S-NTP-UPS-Server](https://github.com/avalitan/MilkV-Duo-S-NTP-UPS-Server) — NTP + NUT UPS 監控
- [vojinvukcevic/boot-time-optimization-milkv](https://github.com/vojinvukcevic/boot-time-optimization-milkv) — 冷開機 14.1 s → 3.2 s 的完整記錄
- [manio/milkv-duos-hwcodec-test](https://github.com/manio/milkv-duos-hwcodec-test) — Duo S 上最小的硬體 H.264 編解碼自檢：直接呼叫 cvi_mpi 的 libsys / libvenc / libvdec，跳過 VI/VPSS/VO，編碼合成幀再解碼回來比對 PSNR（預設 1280×720、60 幀），在 Buildroot 映像（核心 5.10.4）上實測 · 0★
- [Tom-game-project/MilkV-DuoS-rust-tpu-example](https://github.com/Tom-game-project/MilkV-DuoS-rust-tpu-example) — 在 Duo S 上用 Rust 跑 TPU 矩陣乘法：Makefile 自動拉 host-tools、tpu-sdk-sg200x 與 tpu-mlir，把 ONNX 編成 .cvimodel，Rust 交叉編譯到 riscv64 musl 後以 scp 部署 · 0★

**硬體與外殼**

- [iyegoroff/milkv-duo-s-case](https://github.com/iyegoroff/milkv-duo-s-case) — Duo S 參數化 3D 列印外殼 · 12★
- [pauleffect90/MilkVDuoKicad](https://github.com/pauleffect90/MilkVDuoKicad) — KiCad 符號與封裝 · 4★
- [Tosainu/milkv-duo-iob](https://github.com/Tosainu/milkv-duo-iob) — IO 擴充板設計檔案

---

## 11. Gitee 專案與中文教學

**Gitee（19 個）**

- [tinylab/milkv-buildroot](https://gitee.com/tinylab/milkv-buildroot) — 泰曉社群映像檔的 Buildroot 建置工程
- [tinylab/duo-buildroot-sdk](https://gitee.com/tinylab/duo-buildroot-sdk) — 官方 V1 SDK 國內映像檔
- [tinylab/duo-examples](https://gitee.com/tinylab/duo-examples) — 官方範例國內映像檔
- [tinylab/i2c-lsm6dsr](https://gitee.com/tinylab/i2c-lsm6dsr) — I²C LSM6DSR 感測器範例
- [weilinfox/pinpong-milkv-duo-doc](https://gitee.com/weilinfox/pinpong-milkv-duo-doc) — 在 Duo 上跑 pinpong · 3★
- [lan-ruixin/duo-buildroot-sdk](https://gitee.com/lan-ruixin/duo-buildroot-sdk) — 個人維護的 V1 分支，補了中文編譯說明
- [lan-ruixin/milkv-duo-rtl8723du](https://gitee.com/lan-ruixin/milkv-duo-rtl8723du) — RTL8723DU WiFi/藍牙適配
- [qhw136/milkv_duo_sdk](https://gitee.com/qhw136/milkv_duo_sdk) — 補 LCD/觸控/WiFi/藍牙的增強 SDK
- [zhidao101/Milkv_duo_Ubuntu_image](https://gitee.com/zhidao101/Milkv_duo_Ubuntu_image) — 256M 與 512MB 的 Ubuntu 22.04 映像檔
- [tiberium/duosdk2yocto](https://gitee.com/tiberium/duosdk2yocto) — 把 SDK 改造成 Yocto 建置
- [tiberium/meta-milkv-duo-sdk](https://gitee.com/tiberium/meta-milkv-duo-sdk) — 配套 meta layer
- [fixxer2020/duo-multimedia-examples](https://gitee.com/fixxer2020/duo-multimedia-examples) — 多媒體範例映像檔
- [dongshan-community/DongShanPiExtboard](https://gitee.com/dongshan-community/DongShanPiExtboard) — Duo 256M 的 mini-ITX 擴充板
- [linux-proj/Milkv-duo_Cross_Compile_software](https://gitee.com/linux-proj/Milkv-duo_Cross_Compile_software) — 預編譯交叉編譯相依套件
- [atari/opencv-mobile](https://gitee.com/atari/opencv-mobile) — opencv-mobile 同步儲存庫（riscv64-musl、硬體 JPG 解碼、MIPI CSI）· 5★
- [unicornx/riscv-operating-system-mooc](https://gitee.com/unicornx/riscv-operating-system-mooc) — RVOS 課程程式碼（已移植到 Duo）· 541★
- [openeuler/UniProton](https://gitee.com/openeuler/UniProton) — 含 `demos/milkv-duo` 的大小核範例 · 73★（儲存庫已遷往 AtomGit）
- [k0059/duo-buildroot-sdk-v2](https://gitee.com/k0059/duo-buildroot-sdk-v2) — SDK V2 的 sg200x-evb 分支
- [xju_kjc/duo-buildroot-sdk](https://gitee.com/xju_kjc/duo-buildroot-sdk) — V1 SDK 完整映像檔（中/日/英 README）

**中文教學與文章（22 篇）**

- 博客園 [milkv-duo 啟動流程分析：手動建置 fip.bin [1/2]](https://www.cnblogs.com/maomaotou-thu/p/17765721.html) · [2/2](https://www.cnblogs.com/maomaotou-thu/p/17766024.html) · [手動建置 boot.sd](https://www.cnblogs.com/maomaotou-thu/p/17767315.html) — 想搞懂啟動鏈必讀
- 博客園 [Milk-V Duo S 使用報告](https://www.cnblogs.com/BiaoZyx/p/18956632) — 開箱到週邊試用，含踩坑
- 博客園 [大作業：milkv-duo 小車設計工作日誌](https://www.cnblogs.com/Cybersites/p/18859275)
- 博客園 [小核引導 RTOS —— RISC-V C906](https://www.cnblogs.com/gaoyang3513/articles/18854508)
- 博客園 [整合建置流程之根檔案系統 Buildroot](https://www.cnblogs.com/gaoyang3513/p/18854502) · [網路升級韌體](https://www.cnblogs.com/gaoyang3513/p/18854509) · [乙太網路使用與設定](https://www.cnblogs.com/gaoyang3513/p/18854518) · [Docker 開發環境建置](https://www.cnblogs.com/gaoyang3513/p/18854511)
- 博客園 [milkv duo 256M 使用 Debian 系統](https://www.cnblogs.com/GrootStudy/p/18225934)
- 博客園 [milkV-duo 的 Linux 開發環境建置](https://www.cnblogs.com/yzh0526/p/18098794)
- 博客園 [milk-v duo 開機引導進入 rust 程式](https://www.cnblogs.com/longxiangam/p/19640491)
- 掘金 [milkv-duo 開發環境建置 & 燒錄](https://juejin.cn/post/7269416466314821668) · [打包 SDK 時遇到的問題及解決](https://juejin.cn/post/7269417409370505235) · [小奶板點燈 & sensor bring up](https://juejin.cn/post/7269644295588659261) · [image burn](https://juejin.cn/post/7269424598260334648) · [milkv 256duo 初品](https://juejin.cn/post/7355829021311238182)
- B 站專欄 [Milk-v Duo：35 塊帶 TPU 1GHz 的 Linux 開發板](https://www.bilibili.com/read/cv24253633) · [Linux 與 RTOS 雙核開發實務](https://www.bilibili.com/read/cv27449966) · [Duo S 部署 PicoClaw 完整教程](https://www.bilibili.com/read/cv46804507) · [Ubuntu 20.04 詳細編譯環境建置指南](https://www.bilibili.com/read/cv24743710)

> **CSDN 與知乎暫缺**：這兩個站在本機網路下回傳 521 / 403（瀏覽器直連同樣被攔），無法通過「頁面確實存在」的驗證，因此不收未經核實的連結。RT-Thread 問答社群 `club.rt-thread.org` 同樣被 WAF 攔截。等能直連時再補。

---

## 12. 這個索引怎麼維護

- 每天 14:00 自動跑一次全網增量掃描（官方 releases、文件站新頁、新影片、新儲存庫），有變化就提交更新
- 只收**能開啟**的連結；每次更新跑一遍完整連結檢查，失效連結下線或換新位址
- 影片要求確實用了 Duo 系列；專案要求儲存庫裡真的支援這些板子（不是只提一句）
- 收錄不代表背書。第三方映像檔與專案的安全性、授權條款、維護狀態請自己判斷
- 發現漏掉的資源，歡迎提 issue 或 PR；提 PR 時請依現有分節放，並註明適用板型（Duo / Duo 256M / Duo S）

[返回語言索引](README.md)
