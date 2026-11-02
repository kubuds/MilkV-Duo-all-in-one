# Milk-V Duo シリーズ リソース総覧（Duo · Duo 256M · Duo S）

Milk-V Duo シリーズで見つけられるリソースは、できるだけこの 1 ページにまとめています。公式ドキュメントとデータシート、すぐにダウンロードできるイメージ、SDK とツールチェーン、GitHub と Gitee のオープンソースプロジェクト、そして Bilibili と YouTube で実際にこのボードを使っている動画です。

このページはファームウェアやドキュメント本体を複製・ミラーせず、出典とメンテナーのみを示します。**コミュニティのイメージとプロジェクトは Milk-V によるテストや承認を受けていません**。書き込みの前に、ボードの種類、SoC、メモリ、ストレージメディア、リリースノートをご自身で確認してください。

> **まず、手元にあるのがどのボードかを確認してください。** 3 世代の製品は同じものではありません。Duo は CV1800B（64 MB メモリ）、Duo 256M は SG2002（256 MB、Cortex-A53 が 1 基追加）、Duo S は SG2000（512 MB、Wi-Fi 6 / BT5 と eMMC はオプション）を搭載しています。**初代 Duo は公式に生産終了（EOL）とされています**。新しいプロジェクトでは 256M か Duo S をそのまま選ぶことをおすすめします。

---

## 1. ボードの種類とバリエーション

| 型番 | SoC | メモリ | ストレージ | 無線 | イーサネット | TPU | ステータス |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Duo** | CVITEK CV1800B | 64 MB | microSD またはオンボード SD NAND | なし | 100M（PHY） | 0.5 TOPS@INT8 | 生産終了 EOL |
| **Duo 256M** | SG2002 | 256 MB | microSD またはオンボード SD NAND | なし | 100M（PHY） | 1.0 TOPS@INT8 | 販売中 |
| **Duo S** | SG2000 | 512 MB | microSD + 基板上 eMMC 実装位置 | **オプション** Wi-Fi 6 / BT5 | 100M（RJ45、PoE HAT 対応） | 0.5 TOPS@INT8 | 販売中 |
| **Duo Module 01**（コアボード + 評価ボード） | SG2000 | 512 MB | 8 GB eMMC オンボード | Wi-Fi 6 / BT5.4 オンボード | 2× 100M | 0.5 TOPS@INT8 | 販売中 |

**Duo S の 4 つの組み合わせ**：eMMC の実装あり / なし × Wi-Fi モジュールの実装あり / なしで、全部で 4 つの SKU があります。購入時は、商品ページにどれが書かれているかをよく確認してください。

イメージは**起動メディアだけで区別**され（`-sd` / `-emmc`）、Wi-Fi では区別されません —— 公式 v2.0.1 の 7 つのアセットにも、wifi という文字を含むイメージは 1 つもありません（下表参照）。したがって：

- Wi-Fi あり / なしの Duo S は同じイメージを書き込みます。無線機能は、基板上にそのモジュールがあるかどうかで決まります
- eMMC ありのボードは、`-sd` イメージを書き込んで TF カードから起動することも、`-emmc` イメージをオンボードストレージに書き込むこともできます
- eMMC が**ない**ボードは TF カードのみです

---

## 2. 購入先

Taobao の「苦芽企業店（Kubuds）」で以下の 3 種類を販売しています（商品ページの詳細表示には Taobao へのログインが必要です。リンク自体は 200 を返します）：

- **Milk-V Duo 256M**（SG2002、256 MB、Wi-Fi なし）：https://item.taobao.com/item.htm?id=842972320584&skuId=5661357677549
- **Milk-V Duo S ベーシック版**（SG2000、512 MB、Wi-Fi なし・eMMC なし）：https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544644
- **Milk-V Duo S Wi-Fi 版**（SG2000、512 MB、Wi-Fi 6 / BT あり、eMMC なし）：https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544645

Duo S の 2 件は**同一商品の別 SKU** です（`id` が同じで `skuId` が異なります）。注文時は SKU 名に Wi-Fi が含まれるか確認してください。どちらも eMMC はありません。オンボードストレージが必要なら eMMC 版を別途探してください。初代 Duo（CV1800B）は生産終了のため購入リンクは載せていません。

このページで商業色があるのはこの節だけです。それ以外は上流の出典のみを指しています。

---

## 3. 公式ドキュメント、データシート、ハードウェア資料

**ドキュメントサイト：ページごとの索引**

- 起点：[Duo シリーズの概要と仕様比較](https://milkv.io/docs/duo/overview)（4 製品の完全な仕様表で、EOL 声明の出典でもあります） · [ドキュメントサイトのトップ](https://milkv.io/docs/duo/getting-started)
- ボード別ガイド：[Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos) · [Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- 電源投入と書き込み：[システムの起動](https://milkv.io/docs/duo/getting-started/boot) · [初回接続と USB ネットワーク](https://milkv.io/docs/duo/getting-started/setup) · [イメージダウンロード一覧](https://milkv.io/docs/duo/getting-started/download) · [Buildroot SDK のビルド](https://milkv.io/docs/duo/getting-started/buildroot-sdk)
- デュアルコアと低レベル：[サブコア 8051 の開発](https://milkv.io/docs/duo/getting-started/8051core) · [RTOS 小コア開発](https://milkv.io/docs/duo/getting-started/rtoscore) · [Arduino サポート](https://milkv.io/docs/duo/getting-started/arduino) · [低レベル開発](https://milkv.io/docs/duo/low-level-dev)（[MIPI DSI](https://milkv.io/docs/duo/low-level-dev/mipi-dsi)）
- アプリケーション開発：[概要](https://milkv.io/docs/duo/application-development) · [GPIO sysfs](https://milkv.io/docs/duo/application-development/gpio-sysfs) · [ピンマルチプレクス](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [pinpong](https://milkv.io/docs/duo/application-development/pinpong) · [マルチメディアフレームワーク](https://milkv.io/docs/duo/application-development/multimedia)
- カメラ：[USB カメラ](https://milkv.io/docs/duo/camera/usb) · [GC2083 センサー](https://milkv.io/docs/duo/camera/gc2083) · [ISP tuning](https://milkv.io/docs/duo/camera/tuning)
- TPU と TDL：[TPU の紹介](https://milkv.io/docs/duo/application-development/tpu/tpu-introduction) · [TDL SDK の紹介](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-introduction) · YOLO：[v5](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov5) · [v8](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov8) · [v11](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo11) · [v12](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo12) · [顔検出](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-face-detection) · [歩行者検出](https://milkv.io/docs/duo/application-development/tdl-sdk/pedestrian-detection) · [人とペットの検出](https://milkv.io/docs/duo/application-development/tdl-sdk/yolov8-person-pets-detection)
- IO 拡張ボード：[IO Board の概要](https://milkv.io/docs/duo/io-board) · [Duo S PoE HAT](https://milkv.io/docs/duo/io-board/duos-poe-hat) · [USB イーサネット IO ボード](https://milkv.io/docs/duo/io-board/usb-ethernet-iob)
- 公式がまとめたリソースとエコシステムの進捗：[有用なリソース一覧](https://milkv.io/docs/duo/useful-resources) · [メインラインカーネルのサポート状況](https://milkv.io/docs/duo/resources/mainline) · [アップストリーム対応の現状](https://milkv.io/docs/duo/resources/upstream-status) · [MMF マルチメディアフレームワーク](https://milkv.io/docs/duo/resources/mmf) · [OpenCV Mobile](https://milkv.io/docs/duo/resources/opencv-mobile) · [SPILVGL](https://milkv.io/docs/duo/resources/spilvgl) · [Visuino](https://milkv.io/docs/duo/resources/visuino) · [xyzdims のノート](https://milkv.io/docs/duo/resources/xyzdims)
- [ドキュメントサイトのソース](https://github.com/milk-v/milkv.io) —— ドキュメントの誤りや翻訳の追加は、ここに PR を送ってください

**製品ページ**

- [Duo（シリーズページ）](https://milkv.io/duo) · [Duo S](https://milkv.io/duo-s) · [Duo Module 01](https://milkv.io/duo-module-01)
- Duo 256M には独立した製品ページがありません。仕様はシリーズページと[ドキュメント](https://milkv.io/docs/duo/getting-started/duo256m)を参照してください

**ハードウェアファイルとチップのマニュアル**

- [duo-files](https://github.com/milkv-duo/duo-files) —— 公式のボード関連ファイル総合リポジトリ：回路図、データシート、機械図、シルク印刷
- 回路図：[Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)
- データシート：[CV1800B/CV1801B 英語版](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf)（[中国語版](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf)） · [SG2002 中国語版](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 中国語版](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 TRM 英語版](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)
- [Sophgo ドキュメントのリリースページ](https://github.com/sophgo/sophgo-doc/releases) —— 上流チップドキュメントの正式な配布窓口

---

## 4. 公式イメージと書き込み

公式イメージはすべて Buildroot ベースで、V1 / V2 の 2 系統に分かれます。**64 MB の Duo には V1 をおすすめします**（V2 の AI サンプルは 64 MB では動きません）。Duo 256M と Duo S は V2 を使います。

### V2（Duo 256M / Duo S に推奨）· [v2.0.1、2025-05-30](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)

| アセットファイル | ボード | 起動メディア | C ライブラリ / アーキテクチャ |
| --- | --- | --- | --- |
| `milkv-duo-musl-riscv64-sd_v2.0.1.img.zip` | Duo | TF カード | musl / riscv64 |
| `milkv-duo256m-musl-riscv64-sd_v2.0.1.img.zip` | Duo 256M | TF カード | musl / riscv64 |
| `milkv-duo256m-glibc-arm64-sd_v2.0.1.img.zip` | Duo 256M | TF カード | glibc / arm64（A53 経由） |
| `milkv-duos-musl-riscv64-sd_v2.0.1.img.zip` | Duo S | TF カード | musl / riscv64 |
| `milkv-duos-glibc-arm64-sd_v2.0.1.img.zip` | Duo S | TF カード | glibc / arm64（A53 経由） |
| `milkv-duos-musl-riscv64-emmc_v2.0.1.zip` | Duo S（eMMC 必須） | オンボード eMMC | musl / riscv64 |
| `milkv-duos-glibc-arm64-emmc_v2.0.1.zip` | Duo S（eMMC 必須） | オンボード eMMC | glibc / arm64 |

### V1 · [v1.1.4、2024-11-22](https://github.com/milkv-duo/duo-buildroot-sdk/releases)

| アセットファイル | ボード | 起動メディア |
| --- | --- | --- |
| `milkv-duo-sd-v1.1.4.img.zip` | Duo | TF カード |
| `milkv-duo256m-sd-v1.1.4.img.zip` | Duo 256M | TF カード |
| `milkv-duos-sd-v1.1.4.img.zip` | Duo S | TF カード |
| `milkv-duos-emmc-v1.1.4.zip` | Duo S（eMMC 必須） | オンボード eMMC |
| `arduino-milkv-duo-sd-v1.1.4.img.zip` など 4 個 | 3 種類のボード | 同じ命名規則、Arduino プリセットイメージ |

### 書き込みのポイント

- TF カードイメージ：解凍後に balenaEtcher / `dd` で書き込み、カードを挿して電源を入れれば使えます。**ssh はデフォルトで有効、USB-NCM ネットワークインターフェースもデフォルトで有効、root のパスワードは `milkv`**
- eMMC イメージ：TF カードイメージとは**書き方が違います**。Duo S は Recovery キーを押しながら Type-C ケーブルで PC に接続し、CVITEK の `usb_dl.exe`（Windows）または `CviBurn` ツールで USB から書き込みます。書き込みの前に必ず TF カードを抜いてください
- Duo S には **ARM / RISC-V の起動切り替えスイッチ**があり、ファームウェアとスイッチが一致しないと起動しません。シリアルログの先頭文字が `C` なら RISC-V 起動、`B` なら ARM 起動です
- Duo S の Type-C（USB-NCM）と Type-A（USB HOST）は**同時に使えません**。`/mnt/system/usb.sh` のシンボリックリンクで切り替えます

---

## 5. サードパーティイメージ（コミュニティ管理、ボード別）

公式ダウンロードページに[サードパーティイメージの表](https://milkv.io/docs/duo/getting-started/download)があります。ここではボード別に並べ、直接クリックできるようにしています。

### Duo（CV1800B、64 MB）

- [Fedora 41 ミラーサイト](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo/images/latest/) —— Fedora-V Force が管理、上流に追随して更新
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) —— イメージビルドスクリプト、Duo 256M 用もビルドできます
- [Debian / Ubuntu イメージビルダー](https://github.com/logicethos/Milk-V_Duo_Linux2SD) —— 自分でイメージを作るならこれ
- [Arch Linux](https://community.milkv.io/t/arch-linux-on-milkv-duo-milkv-duo-arch-linux/329) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1) · [Debian フルイメージ](https://community.milkv.io/t/milkv-duo-duo-debian-full-7z-519m-download/862)
- [OpenWrt / VizOS](https://github.com/Pillar1989/VizOS) · [Zephyr（サブコア）](https://github.com/kinsamanka/milkv-zephyros) · [Yocto レイヤー](https://github.com/kinsamanka/meta-milkv)
- [RT-Thread cvitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek)（[RISC-V RT-Thread プログラミングガイド](https://riscv-rtthread-programming-manual.readthedocs.io/zh-cn/latest/)） · [ThreadX 移植](https://github.com/saicogn/ThreadX-to-RISC-V64)

### Duo 256M（SG2002）

- [Fedora 41 ミラーサイト](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo256M/images/latest/)
- [Debian（Fishwaldo / sophgo-sg200x-debian）](https://github.com/Fishwaldo/sophgo-sg200x-debian/releases/tag/v1.2.0)
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) · [Arch Linux](https://community.milkv.io/t/debian-arch-linux-on-milkv-duo-256m-milkv-duo-256m-debian-arch-linux/1110) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1)

### Duo S（SG2000）

- [Fedora 41 ミラーサイト](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/DuoS/images/latest/) —— デフォルトのアカウントは `root`、パスワードは `riscv`
- [Debian（scpcom）](https://github.com/scpcom/sophgo-sg200x-debian/releases) —— `root`/`rv` と `debian`/`rv` の 2 組のアカウント
- [NuttX（lupyuen）](https://github.com/lupyuen/nuttx-sg2000/releases) —— Duo S で NuttX を動かす既成イメージ

---

## 6. SDK、ツールチェーン、サンプル

- SDK ソース：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [ホスト側ツールチェーン](https://github.com/milkv-duo/host-tools)
- [duo-examples](https://github.com/milkv-duo/duo-examples) —— 公式 C/C++ サンプル：[GPIO 点滅](https://github.com/milkv-duo/duo-examples/tree/main/blink) · [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c) · [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) · [ペリフェラルドライバ操作ガイド（PDF）](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux)（ピンマルチプレクス） · [duo-wiringx](https://github.com/milkv-duo/duo-wiringx)（wiringX 移植） · [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo)（LVGL framebuffer） · [duo-accessories](https://github.com/milkv-duo/accessories)（公式アクセサリー）
- Arduino：[アーカイブ済みの公式コアライブラリ](https://github.com/milkv-duo/duo-arduino)（リポジトリは [sophgo-arduino](https://github.com/kubuds/sophgo-arduino) を指しています） · [Duo Arduino サンプル](https://github.com/milkv-duo/duo-arduino-examples)
- SoC 側ツール：[CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x) · [TPU-MLIR モデル変換](https://github.com/milkv-duo/tpu-mlir)
- TDL（深層学習サンプル）：[CV180X / Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SG200X / Duo 256M & Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK V2 版 TDL サンプル](https://github.com/milkv-duo/duo-tdl-examples) · [YOLO デプロイ](https://github.com/milkv-duo/duo-yolo-deployment)
- マルチメディア：[duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples)

---

## 7. 公式組織、コミュニティ、交流

- [milkv-duo GitHub 組織](https://github.com/milkv-duo) —— 公式 SDK、サンプル、ハードウェアファイルはすべてここにあります
- [Milk-V コミュニティの Duo カテゴリ](https://community.milkv.io/c/duo/5) —— 質問と体験談の主な場所
- [Duo Module 01 評価ボードのドキュメント](https://milkv.io/docs/duo/getting-started/duo-module-01)
- 旧 `forum.sophgo.com` はアクセスできません（2026-10 の実測で接続失敗）。チップ側の資料は [sophgo-doc](https://github.com/sophgo/sophgo-doc/releases) から入手してください

---

## 8. 動画：Bilibili（50 本）

すべて 1 件ずつページの存在（HTTP 200）と、タイトル・概要が実際に Duo シリーズを指していることを確認済みです。再生数は 2026-10-31 時点のスナップショットで、人気の参考程度です。

**东东老师 シリーズ（eastdong）—— ゼロから始めるのに最適**

- 《零压力上手 RISC-V：东东老师带你玩转 milk-v duo》01. RVOS on Duo — [BV1vm421E7R6](https://www.bilibili.com/video/BV1vm421E7R6/) · 9578
- 02. RT-Thread on Duo — [BV1ym411z7Qo](https://www.bilibili.com/video/BV1ym411z7Qo/) · 3558
- 04. Camera 和 YOLOv5 图像识别 — [BV1mt421A7tL](https://www.bilibili.com/video/BV1mt421A7tL/) · 2972
- 05. TPU 使用 — [BV1Wi421Q7b4](https://www.bilibili.com/video/BV1Wi421Q7b4/) · 2171
- 06. 完结（补讲 Duo 256M 的新变化）— [BV1Fx4y1W7x9](https://www.bilibili.com/video/BV1Fx4y1W7x9/) · 2212

**苦芽科技 —— Duo S 公式コースの一連の流れ**

- 00. 认识 Milk-V Duo S — [BV1PNDoYeEpT](https://www.bilibili.com/video/BV1PNDoYeEpT/) · 2307
- 01. Windows 下安装及启动 — [BV1u3DYYGES7](https://www.bilibili.com/video/BV1u3DYYGES7/) · 376
- macOS 下安装及启动 — [BV1U5qqYUEAm](https://www.bilibili.com/video/BV1U5qqYUEAm/) · 233
- 02. SPI 演示 — [BV1vYqHYnE8G](https://www.bilibili.com/video/BV1vYqHYnE8G/) · 186

**入門とレビュー**

- 35 块带 TPU、1GHz 的 Linux 开发板，还玩啥树莓派（科学中国）— [BV19h4y1t7Ct](https://www.bilibili.com/video/BV19h4y1t7Ct/) · 1.9 万
- 镜像烧写教程：带 TPU 的 RISC-V Linux 板（斑梨电子）— [BV1uM4y1n763](https://www.bilibili.com/video/BV1uM4y1n763/) · 9098
- 能跑轻量 AI 的最便宜 RISC-V Linux 开发板？Duo 64M（捡个肥仔上战场）— [BV11w411j71u](https://www.bilibili.com/video/BV11w411j71u/) · 9365
- RISC-V 峰会现场 Duo 开箱（半导体都市隶人 Ayla）— [BV1oh4y1K724](https://www.bilibili.com/video/BV1oh4y1K724/) · 8415
- 野生的开发板性能再强又有何用，软件适配稀烂：Duo 256M 尝试 Arduino 彻底失败（沈洁 Eacc）— [BV1sZZHYdEPP](https://www.bilibili.com/video/BV1sZZHYdEPP/) · 8026 ← **否定的なレビュー、一見の価値あり**
- 35 元的 milkv-duo Linux 单片机还要啥自行车（开源社区的二掌柜）— [BV1tM4y1Y7kh](https://www.bilibili.com/video/BV1tM4y1Y7kh/) · 2792
- 学习 RISC-V 能跑 Debian & Linux 的最便宜开发板之一（蘭雅 sRGB）— [BV1XQ4y1E7Tj](https://www.bilibili.com/video/BV1XQ4y1E7Tj/) · 3054
- 好玩！RISC-V duo256M 开发板测玩（蘭雅 sRGB）— [BV1Zw411V7bK](https://www.bilibili.com/video/BV1Zw411V7bK/) · 2257
- 麻雀虽小五脏俱全：超高性价比开发板 Milk-V Duo S（qinyunti）— [BV1hyKmzJEw5](https://www.bilibili.com/video/BV1hyKmzJEw5/) · 664

**環境構築と書き込み**

- Linux 下开发环境搭建（future 待续）— [BV1B8411m7jR](https://www.bilibili.com/video/BV1B8411m7jR/) · 3192
- 烧写 Linux 系统 + USB 虚拟 RNDIS 网卡登录（蘭雅 sRGB）— [BV1G14y1k7V4](https://www.bilibili.com/video/BV1G14y1k7V4/) · 1062
- Duo-debian 初体验（蘭雅 sRGB）— [BV11c411o76T](https://www.bilibili.com/video/BV11c411o76T/) · 3416
- Duo 简介和开发环境搭建（谁说现在是冬天呢）— [BV1PF411S7To](https://www.bilibili.com/video/BV1PF411S7To/) · 1959
- Buildroot SDK 简介和编译镜像的方法（谁说现在是冬天呢）— [BV1xc411s7qk](https://www.bilibili.com/video/BV1xc411s7qk/) · 462
- 安装 Hyper-V & 配置 Docker 开发环境（_1dentity）— [BV1nC4y117WS](https://www.bilibili.com/video/BV1nC4y117WS/) · 1826

**ペリフェラル、表示、デュアルコア**

- LVGL 库实战教程 — 刘文涛（群芯闪耀），lazyparser 频道 — [BV1Mp421m7qJ](https://www.bilibili.com/video/BV1Mp421m7qJ/) · 966
- 通过 SPI 驱动 ST7789V 跑 LVGL（谁说现在是冬天呢）— [BV1gLeueWEWr](https://www.bilibili.com/video/BV1gLeueWEWr/) · 2239
- Duo 256M 基于 TinyDRM 驱动 ST7796s 4.0 寸屏并移植 LVGL 8.3（二掌柜）— [BV1Tv421k71W](https://www.bilibili.com/video/BV1Tv421k71W/) · 1230
- USB & Ethernet IO-Board 简介和使用方法（谁说现在是冬天呢）— [BV1Ga4y1Z7oM](https://www.bilibili.com/video/BV1Ga4y1Z7oM/) · 1096
- 通过大核控制小核点亮 LED（谁说现在是冬天呢）— [BV1nH4y1y7CM](https://www.bilibili.com/video/BV1nH4y1y7CM/) · 1057
- 用 Duo 驱动 DF9GMS 微型舵机（谁说现在是冬天呢）— [BV1Dj411E7yD](https://www.bilibili.com/video/BV1Dj411E7yD/) · 571
- Duo S 硬件解码 MP4 并在 LCD 上播放（一只御坂美琴）— [BV1ktvseWEhr](https://www.bilibili.com/video/BV1ktvseWEhr/) · 519

**システム移植**

- 在 Duo 上运行 ThreadX（谁说现在是冬天呢）— [BV1yi421C7SK](https://www.bilibili.com/video/BV1yi421C7SK/) · 419
- 在小核上运行 Zephyr OS（谁说现在是冬天呢）— [BV1uK421Y7x9](https://www.bilibili.com/video/BV1uK421Y7x9/) · 435
- 在 Duo 256M 上运行 Arch Linux（谁说现在是冬天呢）— [BV1j8yyYTEp2](https://www.bilibili.com/video/BV1j8yyYTEp2/) · 1274
- 在 Duo S 上启动 NuttX（悲伤的黑山羊）— [BV1RMUeYjELe](https://www.bilibili.com/video/BV1RMUeYjELe/) · 75
- 罗君：Duo 的 UniProton 适配（PLCT 内部报告）（lazyparser）— [BV1RD421G773](https://www.bilibili.com/video/BV1RD421G773/) · 903
- Duo S 启动！（谁说现在是冬天呢）— [BV1Bm421N72y](https://www.bilibili.com/video/BV1Bm421N72y/) · 564
- 使用 Wi-Fi 连接 Duo S（谁说现在是冬天呢）— [BV11r421T7Sk](https://www.bilibili.com/video/BV11r421T7Sk/) · 318
- 在 Duo S 上部署 Caddy 服务器（谁说现在是冬天呢）— [BV1poBzYQEoC](https://www.bilibili.com/video/BV1poBzYQEoC/) · 214
- Duo 256M 部署相册文件管理器和博客笔记（蘭雅 sRGB）— [BV1cC4y1e7uk](https://www.bilibili.com/video/BV1cC4y1e7uk/) · 1455
- GameOS 開発日誌：自作 OS で Doom を動かし、内蔵の「小さなテレビ」機能から BV 番号で Bilibili 動画を再生（我的大可乐呢／作者はボード名を明記していません）— [BV1iZx46BEV7](https://www.bilibili.com/video/BV1iZx46BEV7/) · 38

**AI / ビジョン**

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

## 9. 動画：YouTube（37 本）

海外サイトのため、プロキシ経由でないと開けません。こちらも 1 件ずつページの存在と、内容が実際に Duo に関係することを確認済みです。

**レビューと導入**

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

**入門、書き込み、ネットワーク**

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

**ペリフェラルと AI**

- Anton Maltsev — Is it good for computer vision? How to start a neural network on it — [dkIVDOd_Fa4](https://www.youtube.com/watch?v=dkIVDOd_Fa4) · Duo
- Mark Birss — Milk-V Duo USB input ST7789 240×240 SPI display — [Swo-zJ6brQI](https://www.youtube.com/watch?v=Swo-zJ6brQI) · Duo
- Sonny Cruz — I²C demo, source in the description — [85uglOz48Pg](https://www.youtube.com/watch?v=85uglOz48Pg) · Duo
- Sonny Cruz — RC servo demo using PWM — [1u2LZJWPtNU](https://www.youtube.com/watch?v=1u2LZJWPtNU) · Duo
- Leigh — Duo + CAM-GC2083: fix RTSP streaming to VLC — [PjiUDsoWCvo](https://www.youtube.com/watch?v=PjiUDsoWCvo) · Duo
- Muhammad Yunus — YOLOX inference on Duo S using TDL SDK + VPSS — [wzUTGK4TuqA](https://www.youtube.com/watch?v=wzUTGK4TuqA) · Duo S

**システム移植と完成品プロジェクト**

- Muhammad Yunus — RT-Thread on Duo S: the best RTOS for cheap RISC-V? — [WjWM5YoAq-c](https://www.youtube.com/watch?v=WjWM5YoAq-c) · Duo S
- RISC-V Developers — S1E2 Enjoy RISC-V with Milk-V Duo: RT-Thread — [B7EXWE6l9xE](https://www.youtube.com/watch?v=B7EXWE6l9xE) · Duo
- Chris McDonough — NixOS 71: NixOS on RISC-V (Milk-V Duo / Duo 256M) — [-ydXjEWUlGE](https://www.youtube.com/watch?v=-ydXjEWUlGE) · Duo 系列
- admin ka — Running Ubuntu glibc 24.04.4 on the Duo 256M — [0Dqbdtjt8Ro](https://www.youtube.com/watch?v=0Dqbdtjt8Ro) · Duo 256M
- 福田重夫 — Running Linux on the Duo 256M (RISC-V + ARM) — [Ga3HX-d8GHQ](https://www.youtube.com/watch?v=Ga3HX-d8GHQ) · Duo 256M
- Nch-Lab — Milk-V Duo 256M を買ったので Linux を動かしてみる — [tcAqYCwbqeU](https://www.youtube.com/watch?v=tcAqYCwbqeU) · Duo 256M
- Mark Birss — Duo 256 CyberDeck LoRa communicator (TLMVC) — [9qOJ3fKwfC0](https://www.youtube.com/watch?v=9qOJ3fKwfC0) · Duo 256M

---

## 10. GitHub オープンソースプロジェクト

用途別に分類しています。star 数と最終コミット日は 2026-10-31 時点のスナップショットで、変化します。「公式」と付いたものは milkv-duo 組織のリポジトリです。

**公式 SDK、ファームウェア、ツール**

- [duo-buildroot-sdk](https://github.com/milkv-duo/duo-buildroot-sdk) — 公式 Buildroot SDK V1（Duo/CV1800B）· 495★
- [duo-buildroot-sdk-v2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) — 公式 SDK V2（Duo 256M / Duo S、SG200x）· 154★
- [duo-examples](https://github.com/milkv-duo/duo-examples) — 公式 C/C++ ペリフェラルサンプル · 159★
- [duo-sdk](https://github.com/milkv-duo/duo-sdk) — ホスト側クロスコンパイル SDK（duo-app-sdk）· 5★
- [host-tools](https://github.com/milkv-duo/host-tools) — プリビルドのホスト gcc ツールチェーン · 9★
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) — ピンマルチプレクス設定ツール · 7★
- [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) — wiringX の Duo 移植 · 11★
- [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples) — マルチメディアパイプラインのサンプル · 6★
- [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) — LVGL on framebuffer · 10★
- [duo-arduino](https://github.com/milkv-duo/duo-arduino) — 公式 Arduino サポート（アーカイブ済み、[sophgo-arduino](https://github.com/kubuds/sophgo-arduino) を指す）· 20★
- [duo-arduino-examples](https://github.com/milkv-duo/duo-arduino-examples) — Arduino サンプル
- [duo-tdl-examples](https://github.com/milkv-duo/duo-tdl-examples) — SDK V2 の TDL サンプル · 13★
- [cvitek-tdl-sdk-sg200x](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) — SG200x TDL-SDK サンプル · 30★
- [cvitek-tdl-sdk-cv180x](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) — CV180x TDL-SDK サンプル
- [tpu-sdk-sg200x](https://github.com/milkv-duo/tpu-sdk-sg200x) — SG200x TPU SDK · 5★
- [tpu-sdk-cv180x](https://github.com/milkv-duo/tpu-sdk-cv180x) — CV180x TPU SDK
- [tpu-mlir](https://github.com/milkv-duo/tpu-mlir) — TPU-MLIR モデル変換 · 9★
- [duo-yolo-deployment](https://github.com/milkv-duo/duo-yolo-deployment) — YOLO デプロイサンプル
- [milkv-duo-linux](https://github.com/milkv-duo/milkv-duo-linux) — 公式カーネルツリー · 1★
- [milkv-duo-u-boot](https://github.com/milkv-duo/milkv-duo-u-boot) — 公式 U-Boot ツリー · 4★
- [milkv-duo-opensbi](https://github.com/milkv-duo/milkv-duo-opensbi) — 公式 OpenSBI 移植 · 2★
- [milkv-duo-smallcore-freertos](https://github.com/milkv-duo/milkv-duo-smallcore-freertos) — 小コア C906 で FreeRTOS · 17★
- [duo-8051](https://github.com/milkv-duo/duo-8051) — 内蔵 8051 コアのサンプル · 8★

**公式ドキュメントとハードウェア資料**

- [duo-files](https://github.com/milkv-duo/duo-files) — 回路図、データシート、機械図の総合リポジトリ · 203★
- [accessories](https://github.com/milkv-duo/accessories) — 公式アクセサリー資料 · 14★
- [milkv.io](https://github.com/milk-v/milkv.io) — 公式サイトとドキュメントサイトのソース · 4★
- [sophgo-doc](https://github.com/sophgo/sophgo-doc) — 上流チップドキュメントの配布窓口
- [datasheet-en](https://github.com/taspenwall/datasheet-en) — SG2002 データシートの英訳 · 5★
- [riscv-rtthread-programming-manual](https://github.com/flyingcys/riscv-rtthread-programming-manual) — 『RISC-V 编程指南：基于 RT-Thread 与 Milk-V Duo』のサンプルコード · 10★
- [MilkV-Duo-Resources](https://github.com/robtech21/MilkV-Duo-Resources) — リソース集
- [johandevlabs/milkv-duo-s-notes](https://github.com/johandevlabs/milk-v-duo-s-notes) — Duo S の試行錯誤メモ · 5★
- [Mirrorium227/MilkvDuo_Basic](https://github.com/Mirrorium227/MilkvDuo_Basic) — CV1800B のトラブルシューティングとサンプル
- [imagineeeinc/things-on-milkv-duo](https://github.com/imagineeeinc/things-on-milkv-duo) — Nim で Duo を動かす

**ブートローダーとファームウェア**

- [u-boot/u-boot](https://github.com/u-boot/u-boot) — メインラインに `board/sophgo/milkv_duo` を含む · 5309★
- [sg_boot](https://github.com/platform-system-interface/sg_boot) — Rust で書かれた CV1800B/SG200x ブートローダー · 12★
- [gtxzsxxk/milkv-duo-firmware-fsbl](https://github.com/gtxzsxxk/milkv-duo-firmware-fsbl) — FSBL の実装 · 6★
- [Taumille/uboot-milkv](https://github.com/Taumille/uboot-milkv) — すでに消えた公式 u-boot リポジトリのコミュニティ fork

**ディストリビューションとシステムイメージ**

- [armbian/build](https://github.com/armbian/build) — `milkv-duos-riscv` / `milkv-duos-arm` ボードを含む · 5499★
- [Fishwaldo/sophgo-sg200x-debian](https://github.com/Fishwaldo/sophgo-sg200x-debian) — 最も活発な SG200x Debian ビルド · 219★
- [ambraglow/milkv-duo-ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) — Duo Ubuntu · 68★
- [olivaw448/milkv-duo-s-512mb-debian](https://github.com/olivaw448/milkv-duo-s-512mb-debian) — Duo S 512MB Debian（WiFi/Bluetooth/USB host/カメラ対応）· 11★
- [eznix86/milkv-duo-s-alpine-linux](https://github.com/eznix86/milkv-duo-s-alpine-linux) — Duo S Alpine · 9★
- [CrocNet/duo-docker-builder](https://github.com/CrocNet/duo-docker-builder) — Docker で Ubuntu イメージをビルド · 9★
- [logicethos/Milk-V_Duo_Linux2SD](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — ビルドして直接カードに書き込み · 21★
- [RawFish69/ubuntu-milkv-duos](https://github.com/RawFish69/ubuntu-milkv-duos) — Duo S Ubuntu 22.04
- [draftbottle/Milkv-duo-openwrt](https://github.com/draftbottle/Milkv-duo-openwrt) — VizOS ベースの OpenWrt
- [Pillar1989/VizOS](https://github.com/Pillar1989/VizOS) — OpenWrt / VizOS プロジェクト
- [georgewhewell/nixos-nanokvm](https://github.com/georgewhewell/nixos-nanokvm) — SG2000/SG2002 の NixOS 設定
- [kinsamanka/meta-milkv](https://github.com/kinsamanka/meta-milkv) — Yocto / OpenEmbedded レイヤー

**RTOS とベアメタル**

- [RT-Thread/rt-thread](https://github.com/RT-Thread/rt-thread) — `bsp/cvitek` に milkv-duo / duo256m / duos を含む · 12318★
- [lupyuen/nuttx-sg2000](https://github.com/lupyuen/nuttx-sg2000) — Duo S 上の NuttX · 45★
- [kinsamanka/milkv-zephyros](https://github.com/kinsamanka/milkv-zephyros) — 小コアの Zephyr · 35★
- [saicogn/ThreadX-to-RISC-V64](https://github.com/saicogn/ThreadX-to-RISC-V64) — ThreadX 移植 · 8★
- [Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK](https://github.com/Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK) — SDK を使わないデュアルコアのベアメタル · 11★
- [zuki/xv6-milkv-duo](https://github.com/zuki/xv6-milkv-duo) — xv6 on Duo · 7★
- [jiegegena/milkv-sg2002-xv6](https://github.com/jiegegena/milkv-sg2002-xv6) — xv6 on SG2002
- [Lam920/xv6-cv1800b](https://github.com/Lam920/xv6-cv1800b) — xv6 on CV1800B
- [rota1001/milkv-baremetal-toolkit](https://github.com/rota1001/milkv-baremetal-toolkit) — ワンクリックでベアメタルイメージを生成 · 8★
- [PeterForth/MILKV-FORTH](https://github.com/PeterForth/MILKV-FORTH) — Duo 上の Forth · 8★
- [xingrz/milkv-duo-zephyr-mailbox-example](https://github.com/xingrz/milkv-duo-zephyr-mailbox-example) — Zephyr と Linux の mailbox 通信
- [DivByDiamond/OnyxOS](https://github.com/DivByDiamond/OnyxOS) — Rust で書かれた RISC-V モノリシックカーネル（C++ ブートローダーとセルフホスト C コンパイラを含め全体で約 272 KB）。SG2000 のプラットフォームドライバを備え、対象ボードに Duo S を挙げています · 0★

**ツールチェーンとビルド環境**

- [aidancrowther/Milk-V-Duo-Docker-Compile](https://github.com/aidancrowther/Milk-V-Duo-Docker-Compile) — ツールチェーンをプリインストールした Docker イメージ · 24★
- [Tosainu/docker-milkv-duo-linux](https://github.com/Tosainu/docker-milkv-duo-linux) — コンテナ化した Linux ビルド
- [boberace/milkv_duo_dc](https://github.com/boberace/milkv_duo_dc) — VS Code Dev Container
- [kitnerboy/milkv-duo-buildroot](https://github.com/kitnerboy/milkv-duo-buildroot) — メインライン流の Buildroot BSP

**ドライバとペリフェラル**

- [hexdump0815/linux-cvitek-cv18xx-kernel](https://github.com/hexdump0815/linux-cvitek-cv18xx-kernel) — コミュニティのカーネルツリー（複数のイメージのカーネル供給元）
- [ret7020/CVI_HW_OpenCV](https://github.com/ret7020/CVI_HW_OpenCV) — NPU で高速化した OpenCV 移植 · 7★
- [pavelanni/gpiod-milkvduo](https://github.com/pavelanni/gpiod-milkvduo) — libgpiod の使い方 · 3★
- [Satharus/I2C-WiringX-Milk-V](https://github.com/Satharus/I2C-WiringX-Milk-V) — wiringX で I²C を操作 · 2★
- [KuLvo/milk-v_duo_oled_driver](https://github.com/KuLvo/milk-v_duo_oled_driver) — 0.96 インチ OLED ドライバ · 3★
- [queenkjuul/aic8800-milkv-duos](https://github.com/queenkjuul/aic8800-milkv-duos) — AIC8800 WiFi+BT 対応
- [GrootLiu/milkv-duo-rtl8723du](https://github.com/GrootLiu/milkv-duo-rtl8723du) — RTL8723DU WiFi 移植
- [Tactical-TV-Remote/infrared_milkv](https://github.com/Tactical-TV-Remote/infrared_milkv) — 赤外線送受信（Rust）
- [harshareddy1611/milkv-duo-s-baremetal-drivers](https://github.com/harshareddy1611/milkv-duo-s-baremetal-drivers) — Duo S ベアメタル GPIO/UART
- [wanghengZzz/Milkv-Duo-FreeRTOS-DMA](https://github.com/wanghengZzz/Milkv-Duo-FreeRTOS-DMA) — FreeRTOS DMA HAL

**実践プロジェクト**
- [tidesense](https://github.com/HumpbackLab/tidesense) — SG2002 によるステレオ視覚惯性オドメトリ（自作ボードで、Duo 256M ではありません）：OV9281 グローバルシャッターのステレオ + SC7U22 IMU、SchurVINS が 20 Hz の視覚補正 / 200 Hz の予測、OpenVINS との比較・キャリブレーション・データセット用ツールを同梱。VIO は Cortex-A53 上で動作し、SD のみで起動。ハードウェアは CC BY-NC-SA 4.0 で公開（リンクはリポジトリの README）· 142★

- [pavelanni/milkv-duo-experiments](https://github.com/pavelanni/milkv-duo-experiments) — Go で書いた実験集 · 27★
- [driver1998/DiscEmu](https://github.com/driver1998/DiscEmu) — Duo で CD-ROM エミュレーター · 11★
- [0x1iii1ii/Pwn-V-Duo](https://github.com/0x1iii1ii/Pwn-V-Duo) — PPPwn 脆弱性エクスプロイトの移植 · 6★
- [aceraoc/MilkV-Duo_TPU](https://github.com/aceraoc/MilkV-Duo_TPU) — TPU 推論の実例 · 8★
- [xmdjy/milkv-car](https://github.com/xmdjy/milkv-car) — Duo ベースのスマートカー
- [Arielfoever/milkv-duo-yolo11](https://github.com/Arielfoever/milkv-duo-yolo11) — YOLO11 デプロイ
- [Basicname/SG200x_GC2083_Yolov8_11](https://github.com/Basicname/SG200x_GC2083_Yolov8_11) — YOLOv8/11 + GC2083 の単一ファイルデプロイ
- [chius-me/globi-v](https://github.com/chius-me/globi-v) — Duo S 上の視覚障害者支援システム
- [f3jry/milkv-duo-xmrsigner](https://github.com/f3jry/milkv-duo-xmrsigner) — Monero コールドウォレットの Duo 移植
- [sdwood68/MilkV_Duo_S_Camera](https://github.com/sdwood68/MilkV_Duo_S_Camera) — Frigate / Home Assistant に接続できるカメラノード
- [ar90n/ptp-server-milkv-duos](https://github.com/ar90n/ptp-server-milkv-duos) — PTP マスタークロックサーバー
- [avalitan/MilkV-Duo-S-NTP-UPS-Server](https://github.com/avalitan/MilkV-Duo-S-NTP-UPS-Server) — NTP + NUT UPS 監視
- [vojinvukcevic/boot-time-optimization-milkv](https://github.com/vojinvukcevic/boot-time-optimization-milkv) — コールドブート 14.1 秒 → 3.2 秒の完全な記録
- [Tom-game-project/MilkV-DuoS-rust-tpu-example](https://github.com/Tom-game-project/MilkV-DuoS-rust-tpu-example) — Duo S 上で Rust から TPU の行列演算を実行：Makefile が host-tools、tpu-sdk-sg200x、tpu-mlir を自動取得し、ONNX を .cvimodel に変換、Rust を riscv64 musl 向けにクロスコンパイルして scp で転送 · 0★

**ハードウェアとケース**

- [iyegoroff/milkv-duo-s-case](https://github.com/iyegoroff/milkv-duo-s-case) — Duo S のパラメトリック 3D プリントケース · 12★
- [pauleffect90/MilkVDuoKicad](https://github.com/pauleffect90/MilkVDuoKicad) — KiCad のシンボルとフットプリント · 4★
- [Tosainu/milkv-duo-iob](https://github.com/Tosainu/milkv-duo-iob) — IO 拡張ボードの設計ファイル

---

## 11. Gitee プロジェクトと中国語チュートリアル

**Gitee（19 件）**

- [tinylab/milkv-buildroot](https://gitee.com/tinylab/milkv-buildroot) — 泰晓コミュニティのミラー用 Buildroot ビルドプロジェクト
- [tinylab/duo-buildroot-sdk](https://gitee.com/tinylab/duo-buildroot-sdk) — 公式 V1 SDK の中国国内ミラー
- [tinylab/duo-examples](https://gitee.com/tinylab/duo-examples) — 公式サンプルの中国国内ミラー
- [tinylab/i2c-lsm6dsr](https://gitee.com/tinylab/i2c-lsm6dsr) — I²C LSM6DSR センサーのサンプル
- [weilinfox/pinpong-milkv-duo-doc](https://gitee.com/weilinfox/pinpong-milkv-duo-doc) — Duo 上で pinpong を動かす · 3★
- [lan-ruixin/duo-buildroot-sdk](https://gitee.com/lan-ruixin/duo-buildroot-sdk) — 個人管理の V1 ブランチ、中国語のビルド手順を追加
- [lan-ruixin/milkv-duo-rtl8723du](https://gitee.com/lan-ruixin/milkv-duo-rtl8723du) — RTL8723DU WiFi/Bluetooth 対応
- [qhw136/milkv_duo_sdk](https://gitee.com/qhw136/milkv_duo_sdk) — LCD/タッチ/WiFi/Bluetooth を追加した拡張 SDK
- [zhidao101/Milkv_duo_Ubuntu_image](https://gitee.com/zhidao101/Milkv_duo_Ubuntu_image) — 256M と 512MB 向けの Ubuntu 22.04 イメージ
- [tiberium/duosdk2yocto](https://gitee.com/tiberium/duosdk2yocto) — SDK を Yocto ビルドに改造
- [tiberium/meta-milkv-duo-sdk](https://gitee.com/tiberium/meta-milkv-duo-sdk) — 対応する meta layer
- [fixxer2020/duo-multimedia-examples](https://gitee.com/fixxer2020/duo-multimedia-examples) — マルチメディアサンプルのミラー
- [dongshan-community/DongShanPiExtboard](https://gitee.com/dongshan-community/DongShanPiExtboard) — Duo 256M の mini-ITX 拡張ボード
- [linux-proj/Milkv-duo_Cross_Compile_software](https://gitee.com/linux-proj/Milkv-duo_Cross_Compile_software) — プリビルドのクロスコンパイル依存パッケージ
- [atari/opencv-mobile](https://gitee.com/atari/opencv-mobile) — opencv-mobile の同期リポジトリ（riscv64-musl、ハードウェア JPG デコード、MIPI CSI）· 5★
- [unicornx/riscv-operating-system-mooc](https://gitee.com/unicornx/riscv-operating-system-mooc) — RVOS コースのコード（Duo に移植済み）· 541★
- [openeuler/UniProton](https://gitee.com/openeuler/UniProton) — `demos/milkv-duo` を含む大小コアのサンプル · 73★（リポジトリは AtomGit に移転済み）
- [k0059/duo-buildroot-sdk-v2](https://gitee.com/k0059/duo-buildroot-sdk-v2) — SDK V2 の sg200x-evb ブランチ
- [xju_kjc/duo-buildroot-sdk](https://gitee.com/xju_kjc/duo-buildroot-sdk) — V1 SDK の完全ミラー（中/日/英 README）

**中国語のチュートリアルと記事（22 件）**

- 博客园 [milkv-duo 启动流程分析：手动构建 fip.bin [1/2]](https://www.cnblogs.com/maomaotou-thu/p/17765721.html) · [2/2](https://www.cnblogs.com/maomaotou-thu/p/17766024.html) · [手动构建 boot.sd](https://www.cnblogs.com/maomaotou-thu/p/17767315.html) —— 起動チェーンを理解したいなら必読
- 博客园 [Milk-V Duo S 使用报告](https://www.cnblogs.com/BiaoZyx/p/18956632) — 開封からペリフェラル試用まで、つまずきどころも収録
- 博客园 [大作业：milkv-duo 小车设计工作日志](https://www.cnblogs.com/Cybersites/p/18859275)
- 博客园 [小核引导 RTOS —— RISC-V C906](https://www.cnblogs.com/gaoyang3513/articles/18854508)
- 博客园 [集成构建流程之根文件系统 Buildroot](https://www.cnblogs.com/gaoyang3513/p/18854502) · [网络升级固件](https://www.cnblogs.com/gaoyang3513/p/18854509) · [以太网使用与配置](https://www.cnblogs.com/gaoyang3513/p/18854518) · [Docker 开发环境搭建](https://www.cnblogs.com/gaoyang3513/p/18854511)
- 博客园 [milkv duo 256M 使用 Debian 系统](https://www.cnblogs.com/GrootStudy/p/18225934)
- 博客园 [milkV-duo 的 Linux 开发环境搭建](https://www.cnblogs.com/yzh0526/p/18098794)
- 博客园 [milk-v duo 开机引导进入 rust 程序](https://www.cnblogs.com/longxiangam/p/19640491)
- 掘金 [milkv-duo 开发环境搭建 & 烧录](https://juejin.cn/post/7269416466314821668) · [打包 SDK 时遇到的问题及解决](https://juejin.cn/post/7269417409370505235) · [小奶板点灯 & sensor bring up](https://juejin.cn/post/7269644295588659261) · [image burn](https://juejin.cn/post/7269424598260334648) · [milkv 256duo 初品](https://juejin.cn/post/7355829021311238182)
- Bilibili コラム [Milk-v Duo：35 块带 TPU 1GHz 的 Linux 开发板](https://www.bilibili.com/read/cv24253633) · [Linux 与 RTOS 双核开发实践](https://www.bilibili.com/read/cv27449966) · [Duo S 部署 PicoClaw 完整教程](https://www.bilibili.com/read/cv46804507) · [Ubuntu 20.04 详细编译环境搭建指南](https://www.bilibili.com/read/cv24743710)

> **CSDN と知乎は今回は未収録**：この 2 つのサイトは、この環境のネットワークから 521 / 403 を返し（ブラウザで直接アクセスしても同じくブロックされます）、「ページが実際に存在する」という検証を通せません。そのため未確認のリンクは掲載していません。RT-Thread の Q&A コミュニティ `club.rt-thread.org` も同様に WAF でブロックされます。直接接続できるようになったら追加します。

---

## 12. この索引のメンテナンス方法

- 毎日 14:00 に Web 全体の増分スキャンを自動で 1 回実行し（公式 releases、ドキュメントサイトの新規ページ、新しい動画、新しいリポジトリ）、変更があれば更新をコミットします
- **開くことができる**リンクだけを掲載します。更新のたびに全リンクのチェックを実行し、リンク切れは削除するか新しいアドレスに差し替えます
- 動画は実際に Duo シリーズを使っていること、プロジェクトはリポジトリが本当にこれらのボードをサポートしていること（単に一言触れているだけでは不可）を条件とします
- 掲載は推奨を意味しません。サードパーティのイメージとプロジェクトの安全性、ライセンス、メンテナンス状況はご自身で判断してください
- 抜けているリソースを見つけたら、issue や PR を歓迎します。PR は既存のセクションに合わせて配置し、対象ボード（Duo / Duo 256M / Duo S）を明記してください

[言語一覧に戻る](README.md)
