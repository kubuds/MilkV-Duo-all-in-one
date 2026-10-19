# Milk-V Duo、Duo 256M、Duo S リソースガイド

Milk-V Duo シリーズの公式ドキュメント、ファームウェア、ソースコード、ハードウェア資料、チュートリアル、コミュニティプロジェクトをまとめたリンク集です。インターネット上のすべての情報を網羅しているとは限りません。リンク切れや追加リソースをぜひお知らせください。

> **利用前に互換性を確認してください。** 初代 Duo は CV1800B と 64 MB メモリ、Duo 256M は SG2002 と 256 MB、Duo S は SG2000 と 512 MB を搭載しています。各ボードではハードウェアやソフトウェアの対象が異なります。公式概要では初代 Duo は生産終了（EOL）とされています。サードパーティーの OS やイメージはコミュニティ管理で、動作確認されていない場合があります。

## 公式製品・ドキュメント

- [Duo シリーズの概要と仕様](https://milkv.io/docs/duo/overview) — ボードの比較、機能、製品ライフサイクル情報。
- ボード別ガイド：[Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos)。
- はじめに：[起動方法](https://milkv.io/docs/duo/getting-started/boot) · [イメージのダウンロードと選択](https://milkv.io/docs/duo/getting-started/download) · [Buildroot SDK ガイド](https://milkv.io/docs/duo/getting-started/buildroot-sdk)。
- 製品ページ：[Duo](https://milkv.io/duo) · [Duo 256M](https://milkv.io/duo256m) · [Duo S](https://milkv.io/duos)。
- [公式ドキュメントのソース](https://github.com/milk-v/milkv.io) — 修正や翻訳の貢献はこちら。

## ファームウェア、SDK、ツールチェーン

- [公式イメージ一覧と互換性に関する注意](https://milkv.io/docs/duo/getting-started/download)。
- 公式ファームウェアのリリース：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk/releases) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)。
- SDK ソース：[Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [ホストツール](https://github.com/milkv-duo/host-tools)。
- 公式ダウンロードガイドでは、64 MB の Duo には V1、Duo 256M と Duo S には V2 を推奨しています。リリースノートとビルド対象の名称を必ず確認してください。
- [公式 C/C++ サンプルとクロスコンパイラーの設定](https://github.com/milkv-duo/duo-examples)：[GPIO 点滅](https://github.com/milkv-duo/duo-examples/tree/main/blink)、[I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c)、[SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi)、[周辺機器ガイド（PDF）](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)。

## ハードウェア、周辺機器、アプリケーション開発

- [公式ボードファイル、回路図、データシート、機械図面](https://github.com/milkv-duo/duo-files)。
- ボード回路図：[Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)。
- [Sophgo チップのデータシートと資料](https://github.com/sophgo/sophgo-doc/releases)。
- SoC 資料：[CV1800B/CV1801B 暫定データシート（英語）](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf)と[中国語版](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf) · [SG2002 暫定データシート（中国語）](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 暫定データシート（中国語）](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf)と[テクニカルリファレンスマニュアル（英語）](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)。
- 公式開発プロジェクト：[ピン多重化](https://github.com/milkv-duo/duo-pinmux) · [wiringX](https://github.com/milkv-duo/duo-wiringx) · [アクセサリー](https://github.com/milkv-duo/accessories) · [LVGL framebuffer デモ](https://github.com/milkv-duo/duo-lvgl-fb-demo)。
- ドキュメント：[GPIO とピン多重化](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [USB カメラ](https://milkv.io/docs/duo/camera/usb) · [マルチメディアフレームワーク](https://milkv.io/docs/duo/application-development/multimedia)。
- Arduino：旧 [Milk-V Arduino コア](https://github.com/milkv-duo/duo-arduino) はアーカイブ済みで、リポジトリでは [Sophgo Arduino](https://github.com/kubuds/sophgo-arduino) が案内されています。[Duo Arduino サンプル](https://github.com/milkv-duo/duo-arduino-examples)もあります。利用前にボードとコアの対応状況を確認してください。

## AI、コンピュータービジョン、メディア

- TDL サンプル：[CV180X／初代 Duo 向け SDK V1](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SG200X／Duo 256M・Duo S 向け SDK V1](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK V2 サンプル](https://github.com/milkv-duo/duo-tdl-examples)。
- TPU とモデルツール：[CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [TPU-MLIR モデル変換](https://github.com/milkv-duo/tpu-mlir) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x)。
- [公式マルチメディアサンプル](https://github.com/milkv-duo/duo-multimedia-examples) · [TDL モデルのデプロイ](https://github.com/milkv-duo/duo-yolo-deployment)。
- [公式ダウンロードガイド](https://milkv.io/docs/duo/getting-started/download)にはボード別のコミュニティ製イメージも掲載されています。注意事項を読み、配布元と対応するハードウェアリビジョンを確認してください。

## コミュニティ OS と学習資料

以下は独立したコミュニティプロジェクトであり、公式ファームウェアではありません。互換性や保守状況は変わる可能性があるため、インストール前に各プロジェクトのドキュメントを確認してください。

- Linux ディストリビューション：[Fedora イメージミラー](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/) · [Sophgo SG200X 向け Debian](https://github.com/scpcom/sophgo-sg200x-debian) · [Ubuntu イメージビルダー](https://github.com/ambraglow/milkv-duo-ubuntu) · [OpenWrt／VizOS プロジェクト](https://github.com/Pillar1989/VizOS)。
- ビルドシステムと RTOS：[Yocto／OpenEmbedded レイヤー](https://github.com/kinsamanka/meta-milkv) · [Duo のセカンダリーコア上の Zephyr](https://github.com/kinsamanka/milkv-zephyros) · [SG2000／Duo S 向け NuttX](https://github.com/lupyuen/nuttx-sg2000) · [RT-Thread CVitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) · [ThreadX 移植版](https://github.com/saicogn/ThreadX-to-RISC-V64)。
- [Milk-V Duo コミュニティフォーラム](https://community.milkv.io/c/duo/5) · [Sophgo フォーラム](https://forum.sophgo.com/) · [Milk-V Duo GitHub 組織](https://github.com/milkv-duo)。

## 貢献とリンクの更新

リンク切れ、リソースの不足、対応ボードの変更を見つけた場合は issue または pull request をお送りください。ファームウェアを再配布せず、開発元のドキュメントやリリースページを優先してください。書き込み前にボード、SoC、メモリー容量、ストレージの種類、起動モード、イメージの手順を確認し、データをバックアップして安全な給電・配線を行ってください。

[言語一覧に戻る](README.md)
