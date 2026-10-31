# Milk-V Duo – Ressourcensammlung (Duo · Duo 256M · Duo S)

Alle Ressourcen zur Milk-V-Duo-Familie, die sich finden lassen, sind möglichst auf dieser einen Seite versammelt: offizielle Dokumentation und Datenblätter, direkt herunterladbare Images, SDKs und Toolchains, Open-Source-Projekte auf GitHub und Gitee sowie Videos auf Bilibili und YouTube, in denen genau diese Boards tatsächlich verwendet werden.

Diese Seite kopiert oder spiegelt weder Firmware noch Dokumente selbst, sondern nennt nur die Bezugsquelle und den Maintainer. **Community-Images und -Projekte werden von Milk-V weder getestet noch empfohlen**; prüfen Sie vor dem Flashen selbst Boardvariante, SoC, Arbeitsspeicher, Speichermedium und Release Notes.

> **Prüfen Sie zuerst, welches Board Sie in der Hand haben.** Die drei Generationen sind nicht dasselbe: Das Duo nutzt den CV1800B (64 MB RAM), das Duo 256M den SG2002 (256 MB, zusätzlich ein Cortex-A53), das Duo S den SG2000 (512 MB, optional Wi-Fi 6 / BT5 und optional eMMC). **Das ursprüngliche Duo ist offiziell als abgekündigt (EOL) gekennzeichnet**; für neue Projekte empfiehlt sich direkt das 256M oder das Duo S.

---

## 1. Boardmodelle und Varianten

| Modell | SoC | RAM | Speicher | Funk | Ethernet | TPU | Status |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Duo** | CVITEK CV1800B | 64 MB | microSD oder onboard SD NAND | – | 100M (PHY) | 0.5 TOPS@INT8 | abgekündigt EOL |
| **Duo 256M** | SG2002 | 256 MB | microSD oder onboard SD NAND | – | 100M (PHY) | 1.0 TOPS@INT8 | erhältlich |
| **Duo S** | SG2000 | 512 MB | microSD + onboard eMMC-Platz | **optional** Wi-Fi 6 / BT5 | 100M (RJ45, PoE-HAT unterstützt) | 0.5 TOPS@INT8 | erhältlich |
| **Duo Module 01** (Core-Board + Evaluierungsboard) | SG2000 | 512 MB | 8 GB eMMC onboard | Wi-Fi 6 / BT5.4 onboard | 2× 100M | 0.5 TOPS@INT8 | erhältlich |

**Die vier Kombinationen des Duo S**: eMMC bestückt oder nicht × Wi-Fi-Modul bestückt oder nicht, insgesamt vier SKUs. Achten Sie beim Kauf genau darauf, welche davon auf der Produktseite steht.

Images unterscheiden sich **ausschließlich nach dem Boot-Medium** (`-sd` / `-emmc`), nicht nach Wi-Fi – unter den sieben Assets der offiziellen Version v2.0.1 trägt kein einziges Image „wifi“ im Namen (siehe Tabelle unten). Daraus folgt:

- Duo S mit und ohne Wi-Fi flashen dasselbe Image; ob WLAN funktioniert, hängt allein davon ab, ob das Modul auf dem Board bestückt ist
- Boards mit eMMC booten entweder mit `-sd` von der TF-Karte oder werden mit `-emmc` in den onboard Speicher geflasht
- Boards **ohne** eMMC laufen ausschließlich über die TF-Karte

---

## 2. Bezugsquellen

Im Kubuds-Shop (苦芽企业店) auf Taobao gibt es diese drei Varianten (für die Artikeldetails ist ein Taobao-Login nötig; die Links selbst liefern 200):

- **Milk-V Duo 256M** (SG2002, 256 MB, kein Wi-Fi): https://item.taobao.com/item.htm?id=842972320584&skuId=5661357677549
- **Milk-V Duo S Basisversion** (SG2000, 512 MB, kein Wi-Fi, kein eMMC): https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544644
- **Milk-V Duo S Wi-Fi** (SG2000, 512 MB, Wi-Fi 6 / BT, kein eMMC): https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544645

Die beiden Duo-S-Positionen sind **zwei SKUs desselben Artikels** (gleiche `id`, unterschiedliche `skuId`) — beim Bestellen im SKU-Namen prüfen, ob Wi-Fi enthalten ist. Beide haben kein eMMC; für Speicher auf dem Board braucht es eine eMMC-Variante. Das ursprüngliche Duo (CV1800B) ist abgekündigt und hat deshalb keinen Kauflink.

Das ist der einzige kommerzielle Teil dieser Seite; alles andere verweist nur auf die Primärquellen.

---

## 3. Offizielle Dokumentation, Datenblätter und Hardware-Unterlagen

**Dokumentationsseite: Seite für Seite indexiert**

- Einstieg: [Überblick über die Duo-Familie und Spezifikationsvergleich](https://milkv.io/docs/duo/overview) (vollständige Spezifikationstabelle aller vier Produkte, zugleich die Quelle der EOL-Erklärung) · [Startseite der Dokumentation](https://milkv.io/docs/duo/getting-started)
- Anleitungen je Board: [Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos) · [Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- Stromversorgung und Flashen: [System booten](https://milkv.io/docs/duo/getting-started/boot) · [Erste Verbindung und USB-Netzwerk](https://milkv.io/docs/duo/getting-started/setup) · [Gesamttabelle der Image-Downloads](https://milkv.io/docs/duo/getting-started/download) · [Build mit dem Buildroot-SDK](https://milkv.io/docs/duo/getting-started/buildroot-sdk)
- Dual-Core und Low-Level: [Entwicklung für den Hilfskern 8051](https://milkv.io/docs/duo/getting-started/8051core) · [RTOS-Entwicklung auf dem kleinen Kern](https://milkv.io/docs/duo/getting-started/rtoscore) · [Arduino-Unterstützung](https://milkv.io/docs/duo/getting-started/arduino) · [Low-Level-Entwicklung](https://milkv.io/docs/duo/low-level-dev) ([MIPI DSI](https://milkv.io/docs/duo/low-level-dev/mipi-dsi))
- Anwendungsentwicklung: [Überblick](https://milkv.io/docs/duo/application-development) · [GPIO sysfs](https://milkv.io/docs/duo/application-development/gpio-sysfs) · [Pin-Multiplexing](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [pinpong](https://milkv.io/docs/duo/application-development/pinpong) · [Multimedia-Framework](https://milkv.io/docs/duo/application-development/multimedia)
- Kamera: [USB-Kamera](https://milkv.io/docs/duo/camera/usb) · [GC2083-Sensor](https://milkv.io/docs/duo/camera/gc2083) · [ISP-Tuning](https://milkv.io/docs/duo/camera/tuning)
- TPU und TDL: [Einführung in die TPU](https://milkv.io/docs/duo/application-development/tpu/tpu-introduction) · [Einführung in das TDL-SDK](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-introduction) · YOLO: [v5](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov5) · [v8](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov8) · [v11](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo11) · [v12](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo12) · [Gesichtserkennung](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-face-detection) · [Fußgängererkennung](https://milkv.io/docs/duo/application-development/tdl-sdk/pedestrian-detection) · [Personen- und Haustiererkennung](https://milkv.io/docs/duo/application-development/tdl-sdk/yolov8-person-pets-detection)
- IO-Erweiterungsboards: [Übersicht der IO-Boards](https://milkv.io/docs/duo/io-board) · [Duo S PoE HAT](https://milkv.io/docs/duo/io-board/duos-poe-hat) · [USB-Ethernet-IO-Board](https://milkv.io/docs/duo/io-board/usb-ethernet-iob)
- Von offizieller Seite zusammengestellte Ressourcen und Fortschritte im Ökosystem: [Übersicht nützlicher Ressourcen](https://milkv.io/docs/duo/useful-resources) · [Stand der Mainline-Kernel-Unterstützung](https://milkv.io/docs/duo/resources/mainline) · [Stand der Upstream-Unterstützung](https://milkv.io/docs/duo/resources/upstream-status) · [MMF-Multimedia-Framework](https://milkv.io/docs/duo/resources/mmf) · [OpenCV Mobile](https://milkv.io/docs/duo/resources/opencv-mobile) · [SPILVGL](https://milkv.io/docs/duo/resources/spilvgl) · [Visuino](https://milkv.io/docs/duo/resources/visuino) · [xyzdims-Notizen](https://milkv.io/docs/duo/resources/xyzdims)
- [Quellcode der Dokumentationsseite](https://github.com/milk-v/milkv.io) – bei Fehlern in der Doku oder wenn Sie Übersetzungen ergänzen möchten, reichen Sie hier einen PR ein

**Produktseiten**

- [Duo (Familienseite)](https://milkv.io/duo) · [Duo S](https://milkv.io/duo-s) · [Duo Module 01](https://milkv.io/duo-module-01)
- Das Duo 256M hat keine eigene Produktseite; die Spezifikationen stehen auf der Familienseite und in der [Dokumentation](https://milkv.io/docs/duo/getting-started/duo256m)

**Hardware-Dateien und Chip-Datenblätter**

- [duo-files](https://github.com/milkv-duo/duo-files) – offizielles Gesamtarchiv der Board-Dateien: Schaltpläne, Datenblätter, mechanische Zeichnungen, Silkscreen
- Schaltpläne: [Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)
- Datenblätter: [CV1800B/CV1801B englisch](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf) ([chinesisch](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf)) · [SG2002 chinesisch](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 chinesisch](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 TRM englisch](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)
- [Release-Seite der Sophgo-Dokumentation](https://github.com/sophgo/sophgo-doc/releases) – der offizielle Ausgabekanal für die Upstream-Chip-Dokumentation

---

## 4. Offizielle Images und Flashen

Die offiziellen Images basieren durchweg auf Buildroot und gliedern sich in zwei Linien, V1 und V2. **Für das Duo mit 64 MB empfiehlt sich V1** (die AI-Beispiele von V2 laufen auf 64 MB nicht); Duo 256M und Duo S nutzen V2.

### V2 (empfohlen für Duo 256M / Duo S) · [v2.0.1, 2025-05-30](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)

| Asset-Datei | Board | Boot-Medium | C-Bibliothek / Architektur |
| --- | --- | --- | --- |
| `milkv-duo-musl-riscv64-sd_v2.0.1.img.zip` | Duo | TF-Karte | musl / riscv64 |
| `milkv-duo256m-musl-riscv64-sd_v2.0.1.img.zip` | Duo 256M | TF-Karte | musl / riscv64 |
| `milkv-duo256m-glibc-arm64-sd_v2.0.1.img.zip` | Duo 256M | TF-Karte | glibc / arm64 (über A53) |
| `milkv-duos-musl-riscv64-sd_v2.0.1.img.zip` | Duo S | TF-Karte | musl / riscv64 |
| `milkv-duos-glibc-arm64-sd_v2.0.1.img.zip` | Duo S | TF-Karte | glibc / arm64 (über A53) |
| `milkv-duos-musl-riscv64-emmc_v2.0.1.zip` | Duo S (eMMC erforderlich) | onboard eMMC | musl / riscv64 |
| `milkv-duos-glibc-arm64-emmc_v2.0.1.zip` | Duo S (eMMC erforderlich) | onboard eMMC | glibc / arm64 |

### V1 · [v1.1.4, 2024-11-22](https://github.com/milkv-duo/duo-buildroot-sdk/releases)

| Asset-Datei | Board | Boot-Medium |
| --- | --- | --- |
| `milkv-duo-sd-v1.1.4.img.zip` | Duo | TF-Karte |
| `milkv-duo256m-sd-v1.1.4.img.zip` | Duo 256M | TF-Karte |
| `milkv-duos-sd-v1.1.4.img.zip` | Duo S | TF-Karte |
| `milkv-duos-emmc-v1.1.4.zip` | Duo S (eMMC erforderlich) | onboard eMMC |
| `arduino-milkv-duo-sd-v1.1.4.img.zip` u. a. 4 Dateien | alle drei Boards | gleiche Namensregel, Images mit Arduino-Vorinstallation |

### Wichtige Hinweise zum Flashen

- TF-Karten-Images: nach dem Entpacken mit balenaEtcher / `dd` schreiben, Karte einstecken und einschalten; **ssh ist standardmäßig aktiv, die USB-NCM-Netzwerkkarte ebenfalls, das root-Passwort lautet `milkv`**
- eMMC-Images: werden **nicht** wie TF-Karten-Images geschrieben. Beim Duo S die Recovery-Taste gedrückt halten, das Board mit einem Type-C-Datenkabel an den Rechner anschließen und dann mit dem CVITEK-Tool `usb_dl.exe` (Windows) oder `CviBurn` über USB flashen; vorher unbedingt die TF-Karte entfernen
- Das Duo S hat einen **Umschalter für den Start von ARM / RISC-V**; passt die Firmware nicht zur Schalterstellung, bootet es nicht. Steht im seriellen Log als erstes Zeichen ein `C`, startet es von RISC-V, bei `B` von ARM
- Beim Duo S lassen sich Type-C (USB-NCM) und Type-A (USB HOST) **nicht gleichzeitig** nutzen; umgeschaltet wird über einen Symlink auf `/mnt/system/usb.sh`

---

## 5. Images von Drittanbietern (von der Community gepflegt, nach Board gegliedert)

Die offizielle Download-Seite enthält eine [Tabelle der Drittanbieter-Images](https://milkv.io/docs/duo/getting-started/download); hier ist sie nach Board aufgeschlüsselt, damit sich alles direkt anklicken lässt.

### Duo (CV1800B, 64 MB)

- [Fedora-41-Mirror](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo/images/latest/) – von Fedora-V Force gepflegt, folgt dem Upstream
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) – Skript zum Bauen von Images, kann auch das Duo 256M bauen
- [Debian-/Ubuntu-Image-Builder](https://github.com/logicethos/Milk-V_Duo_Linux2SD) – damit erstellen Sie eigene Images
- [Arch Linux](https://community.milkv.io/t/arch-linux-on-milkv-duo-milkv-duo-arch-linux/329) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1) · [Debian-Vollimage](https://community.milkv.io/t/milkv-duo-duo-debian-full-7z-519m-download/862)
- [OpenWrt / VizOS](https://github.com/Pillar1989/VizOS) · [Zephyr (Hilfskern)](https://github.com/kinsamanka/milkv-zephyros) · [Yocto-Layer](https://github.com/kinsamanka/meta-milkv)
- [RT-Thread cvitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) ([Programmierhandbuch zu RISC-V mit RT-Thread](https://riscv-rtthread-programming-manual.readthedocs.io/zh-cn/latest/)) · [ThreadX-Portierung](https://github.com/saicogn/ThreadX-to-RISC-V64)

### Duo 256M (SG2002)

- [Fedora-41-Mirror](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo256M/images/latest/)
- [Debian (Fishwaldo / sophgo-sg200x-debian)](https://github.com/Fishwaldo/sophgo-sg200x-debian/releases/tag/v1.2.0)
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) · [Arch Linux](https://community.milkv.io/t/debian-arch-linux-on-milkv-duo-256m-milkv-duo-256m-debian-arch-linux/1110) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1)

### Duo S (SG2000)

- [Fedora-41-Mirror](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/DuoS/images/latest/) – Standardkonto `root` / Passwort `riscv`
- [Debian (scpcom)](https://github.com/scpcom/sophgo-sg200x-debian/releases) – zwei Kontosätze: `root`/`rv` und `debian`/`rv`
- [NuttX (lupyuen)](https://github.com/lupyuen/nuttx-sg2000/releases) – fertiges Image, um NuttX auf dem Duo S zu betreiben

---

## 6. SDK, Toolchain und Beispiele

- SDK-Quellcode: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [Host-Toolchain](https://github.com/milkv-duo/host-tools)
- [duo-examples](https://github.com/milkv-duo/duo-examples) – offizielle C/C++-Beispiele: [GPIO-Blinken](https://github.com/milkv-duo/duo-examples/tree/main/blink) · [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c) · [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) · [Anleitung zur Peripherietreiber-Nutzung (PDF)](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) (Pin-Multiplexing) · [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) (wiringX-Portierung) · [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) (LVGL-Framebuffer) · [duo-accessories](https://github.com/milkv-duo/accessories) (offizielles Zubehör)
- Arduino: [archivierte offizielle Core-Bibliothek](https://github.com/milkv-duo/duo-arduino) (das Repository verweist inzwischen auf [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)) · [Arduino-Beispiele für das Duo](https://github.com/milkv-duo/duo-arduino-examples)
- Werkzeuge auf der SoC-Seite: [CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x) · [TPU-MLIR-Modellkonvertierung](https://github.com/milkv-duo/tpu-mlir)
- TDL (Deep-Learning-Beispiele): [CV180X / Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SG200X / Duo 256M & Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [TDL-Beispiele für SDK V2](https://github.com/milkv-duo/duo-tdl-examples) · [YOLO-Deployment](https://github.com/milkv-duo/duo-yolo-deployment)
- Multimedia: [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples)

---

## 7. Offizielle Organisation, Community und Austausch

- [GitHub-Organisation milkv-duo](https://github.com/milkv-duo) – hier liegen die offiziellen SDKs, Beispiele und Hardware-Dateien
- [Duo-Kategorie der Milk-V-Community](https://community.milkv.io/c/duo/5) – die zentrale Anlaufstelle für Fragen und Erfahrungsberichte
- [Dokumentation zum Evaluierungsboard Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- Das frühere `forum.sophgo.com` ist nicht mehr erreichbar (Verbindungstest im Oktober 2026 fehlgeschlagen); Chip-Unterlagen beziehen Sie jetzt über [sophgo-doc](https://github.com/sophgo/sophgo-doc/releases)

---

## 8. Videos: Bilibili (48 Stück)

Alle Einträge wurden einzeln geprüft: Die Seite existiert (HTTP 200), und Titel bzw. Beschreibung weisen tatsächlich auf die Duo-Familie hin; die Aufrufzahlen sind eine Momentaufnahme vom 31.10.2026 und dienen nur als Hinweis auf die Beliebtheit.

**Reihe von Lehrer Dongdong (eastdong) – ideal, um bei null anzufangen**

- 《零压力上手 RISC-V：东东老师带你玩转 milk-v duo》01. RVOS on Duo — [BV1vm421E7R6](https://www.bilibili.com/video/BV1vm421E7R6/) · 9578
- 02. RT-Thread on Duo — [BV1ym411z7Qo](https://www.bilibili.com/video/BV1ym411z7Qo/) · 3558
- 04. Camera 和 YOLOv5 图像识别 — [BV1mt421A7tL](https://www.bilibili.com/video/BV1mt421A7tL/) · 2972
- 05. TPU 使用 — [BV1Wi421Q7b4](https://www.bilibili.com/video/BV1Wi421Q7b4/) · 2171
- 06. 完结（补讲 Duo 256M 的新变化）— [BV1Fx4y1W7x9](https://www.bilibili.com/video/BV1Fx4y1W7x9/) · 2212

**苦芽科技 – der komplette Lernpfad des offiziellen Duo-S-Kurses**

- 00. 认识 Milk-V Duo S — [BV1PNDoYeEpT](https://www.bilibili.com/video/BV1PNDoYeEpT/) · 2307
- 01. Windows 下安装及启动 — [BV1u3DYYGES7](https://www.bilibili.com/video/BV1u3DYYGES7/) · 376
- macOS 下安装及启动 — [BV1U5qqYUEAm](https://www.bilibili.com/video/BV1U5qqYUEAm/) · 233
- 02. SPI 演示 — [BV1vYqHYnE8G](https://www.bilibili.com/video/BV1vYqHYnE8G/) · 186

**Einstieg und Tests**

- 35 块带 TPU、1GHz 的 Linux 开发板，还玩啥树莓派（科学中国）— [BV19h4y1t7Ct](https://www.bilibili.com/video/BV19h4y1t7Ct/) · 19.000
- 镜像烧写教程：带 TPU 的 RISC-V Linux 板（斑梨电子）— [BV1uM4y1n763](https://www.bilibili.com/video/BV1uM4y1n763/) · 9098
- 能跑轻量 AI 的最便宜 RISC-V Linux 开发板？Duo 64M（捡个肥仔上战场）— [BV11w411j71u](https://www.bilibili.com/video/BV11w411j71u/) · 9365
- RISC-V 峰会现场 Duo 开箱（半导体都市隶人 Ayla）— [BV1oh4y1K724](https://www.bilibili.com/video/BV1oh4y1K724/) · 8415
- 野生的开发板性能再强又有何用，软件适配稀烂：Duo 256M 尝试 Arduino 彻底失败（沈洁 Eacc）— [BV1sZZHYdEPP](https://www.bilibili.com/video/BV1sZZHYdEPP/) · 8026 ← **negative Bewertung, sehenswert**
- 35 元的 milkv-duo Linux 单片机还要啥自行车（开源社区的二掌柜）— [BV1tM4y1Y7kh](https://www.bilibili.com/video/BV1tM4y1Y7kh/) · 2792
- 学习 RISC-V 能跑 Debian & Linux 的最便宜开发板之一（蘭雅 sRGB）— [BV1XQ4y1E7Tj](https://www.bilibili.com/video/BV1XQ4y1E7Tj/) · 3054
- 好玩！RISC-V duo256M 开发板测玩（蘭雅 sRGB）— [BV1Zw411V7bK](https://www.bilibili.com/video/BV1Zw411V7bK/) · 2257
- 麻雀虽小五脏俱全：超高性价比开发板 Milk-V Duo S（qinyunti）— [BV1hyKmzJEw5](https://www.bilibili.com/video/BV1hyKmzJEw5/) · 664

**Umgebung einrichten und Flashen**

- Linux 下开发环境搭建（future 待续）— [BV1B8411m7jR](https://www.bilibili.com/video/BV1B8411m7jR/) · 3192
- 烧写 Linux 系统 + USB 虚拟 RNDIS 网卡登录（蘭雅 sRGB）— [BV1G14y1k7V4](https://www.bilibili.com/video/BV1G14y1k7V4/) · 1062
- Duo-debian 初体验（蘭雅 sRGB）— [BV11c411o76T](https://www.bilibili.com/video/BV11c411o76T/) · 3416
- Duo 简介和开发环境搭建（谁说现在是冬天呢）— [BV1PF411S7To](https://www.bilibili.com/video/BV1PF411S7To/) · 1959
- Buildroot SDK 简介和编译镜像的方法（谁说现在是冬天呢）— [BV1xc411s7qk](https://www.bilibili.com/video/BV1xc411s7qk/) · 462
- 安装 Hyper-V & 配置 Docker 开发环境（_1dentity）— [BV1nC4y117WS](https://www.bilibili.com/video/BV1nC4y117WS/) · 1826

**Peripherie, Display und Dual-Core**

- LVGL 库实战教程 — 刘文涛（群芯闪耀），lazyparser 频道 — [BV1Mp421m7qJ](https://www.bilibili.com/video/BV1Mp421m7qJ/) · 966
- 通过 SPI 驱动 ST7789V 跑 LVGL（谁说现在是冬天呢）— [BV1gLeueWEWr](https://www.bilibili.com/video/BV1gLeueWEWr/) · 2239
- Duo 256M 基于 TinyDRM 驱动 ST7796s 4.0 寸屏并移植 LVGL 8.3（二掌柜）— [BV1Tv421k71W](https://www.bilibili.com/video/BV1Tv421k71W/) · 1230
- USB & Ethernet IO-Board 简介和使用方法（谁说现在是冬天呢）— [BV1Ga4y1Z7oM](https://www.bilibili.com/video/BV1Ga4y1Z7oM/) · 1096
- 通过大核控制小核点亮 LED（谁说现在是冬天呢）— [BV1nH4y1y7CM](https://www.bilibili.com/video/BV1nH4y1y7CM/) · 1057
- 用 Duo 驱动 DF9GMS 微型舵机（谁说现在是冬天呢）— [BV1Dj411E7yD](https://www.bilibili.com/video/BV1Dj411E7yD/) · 571
- Duo S 硬件解码 MP4 并在 LCD 上播放（一只御坂美琴）— [BV1ktvseWEhr](https://www.bilibili.com/video/BV1ktvseWEhr/) · 519

**Systemportierung**

- 在 Duo 上运行 ThreadX（谁说现在是冬天呢）— [BV1yi421C7SK](https://www.bilibili.com/video/BV1yi421C7SK/) · 419
- 在小核上运行 Zephyr OS（谁说现在是冬天呢）— [BV1uK421Y7x9](https://www.bilibili.com/video/BV1uK421Y7x9/) · 435
- 在 Duo 256M 上运行 Arch Linux（谁说现在是冬天呢）— [BV1j8yyYTEp2](https://www.bilibili.com/video/BV1j8yyYTEp2/) · 1274
- 在 Duo S 上启动 NuttX（悲伤的黑山羊）— [BV1RMUeYjELe](https://www.bilibili.com/video/BV1RMUeYjELe/) · 75
- 罗君：Duo 的 UniProton 适配（PLCT 内部报告）（lazyparser）— [BV1RD421G773](https://www.bilibili.com/video/BV1RD421G773/) · 903
- Duo S 启动！（谁说现在是冬天呢）— [BV1Bm421N72y](https://www.bilibili.com/video/BV1Bm421N72y/) · 564
- 使用 Wi-Fi 连接 Duo S（谁说现在是冬天呢）— [BV11r421T7Sk](https://www.bilibili.com/video/BV11r421T7Sk/) · 318
- 在 Duo S 上部署 Caddy 服务器（谁说现在是冬天呢）— [BV1poBzYQEoC](https://www.bilibili.com/video/BV1poBzYQEoC/) · 214
- Duo 256M 部署相册文件管理器和博客笔记（蘭雅 sRGB）— [BV1cC4y1e7uk](https://www.bilibili.com/video/BV1cC4y1e7uk/) · 1455

**KI / Vision**

- Duo 256M 锁头测试：官方脚本跑人脸检测并拉流到电脑（Judehahh）— [BV1w4421A7A2](https://www.bilibili.com/video/BV1w4421A7A2/) · 36.000
- 基于 Duo 和 YOLOv5 的目标检测（谁说现在是冬天呢）— [BV1iG41197qa](https://www.bilibili.com/video/BV1iG41197qa/) · 1211
- 基于 TDL SDK 实现 YOLOv5 目标检测（谁说现在是冬天呢）— [BV1Vw4m1U71C](https://www.bilibili.com/video/BV1Vw4m1U71C/) · 446
- YOLOv8 目标检测（谁说现在是冬天呢）— [BV1AWqUYGEaS](https://www.bilibili.com/video/BV1AWqUYGEaS/) · 269
- 测试通过 VLC 显示 CAM-GC2083 摄像头画面（谁说现在是冬天呢）— [BV188411v7tc](https://www.bilibili.com/video/BV188411v7tc/) · 1159
- Duo S 运行故事机 baby llama2（谁说现在是冬天呢）— [BV1dn4y197UW](https://www.bilibili.com/video/BV1dn4y197UW/) · 621
- Duo S 上用 TDL SDK 部署人脸检测（谁说现在是冬天呢）— [BV1AM4m1m7fe](https://www.bilibili.com/video/BV1AM4m1m7fe/) · 522
- YOLO 实战：车牌识别效果展示（谁说现在是冬天呢）— [BV1uYAHerEbL](https://www.bilibili.com/video/BV1uYAHerEbL/) · 1272

---

## 9. Videos: YouTube (37 Stück)

Seiten im Ausland, die sich nur über einen Proxy öffnen lassen; auch hier wurde jeder Eintrag einzeln geprüft, die Seite existiert und der Inhalt befasst sich tatsächlich mit dem Duo.

**Tests und Erste Schritte**

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

**Einstieg, Flashen und Netzwerk**

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

**Peripherie und KI**

- Anton Maltsev — Is it good for computer vision? How to start a neural network on it — [dkIVDOd_Fa4](https://www.youtube.com/watch?v=dkIVDOd_Fa4) · Duo
- Mark Birss — Milk-V Duo USB input ST7789 240×240 SPI display — [Swo-zJ6brQI](https://www.youtube.com/watch?v=Swo-zJ6brQI) · Duo
- Sonny Cruz — I²C demo, source in the description — [85uglOz48Pg](https://www.youtube.com/watch?v=85uglOz48Pg) · Duo
- Sonny Cruz — RC servo demo using PWM — [1u2LZJWPtNU](https://www.youtube.com/watch?v=1u2LZJWPtNU) · Duo
- Leigh — Duo + CAM-GC2083: fix RTSP streaming to VLC — [PjiUDsoWCvo](https://www.youtube.com/watch?v=PjiUDsoWCvo) · Duo
- Muhammad Yunus — YOLOX inference on Duo S using TDL SDK + VPSS — [wzUTGK4TuqA](https://www.youtube.com/watch?v=wzUTGK4TuqA) · Duo S

**Systemportierung und Komplettprojekte**

- Muhammad Yunus — RT-Thread on Duo S: the best RTOS for cheap RISC-V? — [WjWM5YoAq-c](https://www.youtube.com/watch?v=WjWM5YoAq-c) · Duo S
- RISC-V Developers — S1E2 Enjoy RISC-V with Milk-V Duo: RT-Thread — [B7EXWE6l9xE](https://www.youtube.com/watch?v=B7EXWE6l9xE) · Duo
- Chris McDonough — NixOS 71: NixOS on RISC-V (Milk-V Duo / Duo 256M) — [-ydXjEWUlGE](https://www.youtube.com/watch?v=-ydXjEWUlGE) · Duo-Serie
- admin ka — Running Ubuntu glibc 24.04.4 on the Duo 256M — [0Dqbdtjt8Ro](https://www.youtube.com/watch?v=0Dqbdtjt8Ro) · Duo 256M
- 福田重夫 — Running Linux on the Duo 256M (RISC-V + ARM) — [Ga3HX-d8GHQ](https://www.youtube.com/watch?v=Ga3HX-d8GHQ) · Duo 256M
- Nch-Lab — Milk-V Duo 256M を買ったので Linux を動かしてみる — [tcAqYCwbqeU](https://www.youtube.com/watch?v=tcAqYCwbqeU) · Duo 256M
- Mark Birss — Duo 256 CyberDeck LoRa communicator (TLMVC) — [9qOJ3fKwfC0](https://www.youtube.com/watch?v=9qOJ3fKwfC0) · Duo 256M

---

## 10. Open-Source-Projekte auf GitHub

Nach Einsatzzweck gegliedert. Star-Zahlen und Datum des letzten Commits sind eine Momentaufnahme vom 31.10.2026 und ändern sich; mit „offiziell“ gekennzeichnete Repositories gehören zur Organisation milkv-duo.

**Offizielle SDKs, Firmware und Werkzeuge**

- [duo-buildroot-sdk](https://github.com/milkv-duo/duo-buildroot-sdk) — offizielles Buildroot SDK V1 (Duo/CV1800B) · 495★
- [duo-buildroot-sdk-v2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) — offizielles SDK V2 (Duo 256M / Duo S, SG200x) · 154★
- [duo-examples](https://github.com/milkv-duo/duo-examples) — offizielle C/C++-Beispiele für Peripherie · 159★
- [duo-sdk](https://github.com/milkv-duo/duo-sdk) — Cross-Compile-SDK für den Host (duo-app-sdk) · 5★
- [host-tools](https://github.com/milkv-duo/host-tools) — vorkompilierte gcc-Toolchain für den Host · 9★
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) — Konfigurationswerkzeug für Pin-Multiplexing · 7★
- [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) — wiringX-Portierung für das Duo · 11★
- [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples) — Beispiele für die Multimedia-Kette · 6★
- [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) — LVGL auf dem Framebuffer · 10★
- [duo-arduino](https://github.com/milkv-duo/duo-arduino) — offizielle Arduino-Unterstützung (archiviert, verweist auf [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)) · 20★
- [duo-arduino-examples](https://github.com/milkv-duo/duo-arduino-examples) — Arduino-Beispiele
- [duo-tdl-examples](https://github.com/milkv-duo/duo-tdl-examples) — TDL-Beispiele für SDK V2 · 13★
- [cvitek-tdl-sdk-sg200x](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) — TDL-SDK-Beispiele für SG200x · 30★
- [cvitek-tdl-sdk-cv180x](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) — TDL-SDK-Beispiele für CV180x
- [tpu-sdk-sg200x](https://github.com/milkv-duo/tpu-sdk-sg200x) — TPU SDK für SG200x · 5★
- [tpu-sdk-cv180x](https://github.com/milkv-duo/tpu-sdk-cv180x) — TPU SDK für CV180x
- [tpu-mlir](https://github.com/milkv-duo/tpu-mlir) — TPU-MLIR-Modellkonvertierung · 9★
- [duo-yolo-deployment](https://github.com/milkv-duo/duo-yolo-deployment) — Beispiel für YOLO-Deployment
- [milkv-duo-linux](https://github.com/milkv-duo/milkv-duo-linux) — offizieller Kernel-Baum · 1★
- [milkv-duo-u-boot](https://github.com/milkv-duo/milkv-duo-u-boot) — offizieller U-Boot-Baum · 4★
- [milkv-duo-opensbi](https://github.com/milkv-duo/milkv-duo-opensbi) — offizielle OpenSBI-Portierung · 2★
- [milkv-duo-smallcore-freertos](https://github.com/milkv-duo/milkv-duo-smallcore-freertos) — FreeRTOS auf dem kleinen C906-Kern · 17★
- [duo-8051](https://github.com/milkv-duo/duo-8051) — Beispiele für den integrierten 8051-Kern · 8★

**Offizielle Dokumentation und Hardware-Unterlagen**

- [duo-files](https://github.com/milkv-duo/duo-files) — Gesamtarchiv für Schaltpläne, Datenblätter und mechanische Zeichnungen · 203★
- [accessories](https://github.com/milkv-duo/accessories) — Unterlagen zum offiziellen Zubehör · 14★
- [milkv.io](https://github.com/milk-v/milkv.io) — Quellcode von Website und Dokumentationsseite · 4★
- [sophgo-doc](https://github.com/sophgo/sophgo-doc) — Ausgabekanal für die Upstream-Chip-Dokumentation
- [datasheet-en](https://github.com/taspenwall/datasheet-en) — englische Übersetzung des SG2002-Datenblatts · 5★
- [riscv-rtthread-programming-manual](https://github.com/flyingcys/riscv-rtthread-programming-manual) — Begleitcode zu „RISC-V-Programmierhandbuch: mit RT-Thread und Milk-V Duo“ · 10★
- [MilkV-Duo-Resources](https://github.com/robtech21/MilkV-Duo-Resources) — Ressourcensammlung
- [johandevlabs/milk-v-duo-s-notes](https://github.com/johandevlabs/milk-v-duo-s-notes) — Notizen zum Herumexperimentieren mit dem Duo S · 5★
- [Mirrorium227/MilkvDuo_Basic](https://github.com/Mirrorium227/MilkvDuo_Basic) — Fehlersuche und Beispiele für den CV1800B
- [imagineeeinc/things-on-milkv-duo](https://github.com/imagineeeinc/things-on-milkv-duo) — mit Nim auf dem Duo experimentieren

**Bootloader und Firmware**

- [u-boot/u-boot](https://github.com/u-boot/u-boot) — Mainline enthält bereits `board/sophgo/milkv_duo` · 5309★
- [sg_boot](https://github.com/platform-system-interface/sg_boot) — in Rust geschriebener Bootloader für CV1800B/SG200x · 12★
- [gtxzsxxk/milkv-duo-firmware-fsbl](https://github.com/gtxzsxxk/milkv-duo-firmware-fsbl) — FSBL-Implementierung · 6★
- [Taumille/uboot-milkv](https://github.com/Taumille/uboot-milkv) — Community-Fork des verschwundenen offiziellen u-boot-Repositories

**Distributionen und System-Images**

- [armbian/build](https://github.com/armbian/build) — enthält bereits die Boardtypen `milkv-duos-riscv` / `milkv-duos-arm` · 5499★
- [Fishwaldo/sophgo-sg200x-debian](https://github.com/Fishwaldo/sophgo-sg200x-debian) — der aktivste Debian-Build für SG200x · 219★
- [ambraglow/milkv-duo-ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) — Ubuntu für das Duo · 68★
- [olivaw448/milkv-duo-s-512mb-debian](https://github.com/olivaw448/milkv-duo-s-512mb-debian) — Debian für Duo S 512MB (mit WiFi/Bluetooth/USB host/Kamera) · 11★
- [eznix86/milkv-duo-s-alpine-linux](https://github.com/eznix86/milkv-duo-s-alpine-linux) — Alpine für das Duo S · 9★
- [CrocNet/duo-docker-builder](https://github.com/CrocNet/duo-docker-builder) — Ubuntu-Images mit Docker bauen · 9★
- [logicethos/Milk-V_Duo_Linux2SD](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — bauen und direkt auf die Karte schreiben · 21★
- [RawFish69/ubuntu-milkv-duos](https://github.com/RawFish69/ubuntu-milkv-duos) — Ubuntu 22.04 für das Duo S
- [draftbottle/Milkv-duo-openwrt](https://github.com/draftbottle/Milkv-duo-openwrt) — OpenWrt auf Basis von VizOS
- [Pillar1989/VizOS](https://github.com/Pillar1989/VizOS) — das OpenWrt-/VizOS-Projekt
- [georgewhewell/nixos-nanokvm](https://github.com/georgewhewell/nixos-nanokvm) — NixOS-Konfiguration für SG2000/SG2002
- [kinsamanka/meta-milkv](https://github.com/kinsamanka/meta-milkv) — Yocto-/OpenEmbedded-Layer

**RTOS und Bare-Metal**

- [RT-Thread/rt-thread](https://github.com/RT-Thread/rt-thread) — `bsp/cvitek` enthält milkv-duo / duo256m / duos · 12318★
- [lupyuen/nuttx-sg2000](https://github.com/lupyuen/nuttx-sg2000) — NuttX auf dem Duo S · 45★
- [kinsamanka/milkv-zephyros](https://github.com/kinsamanka/milkv-zephyros) — Zephyr auf dem kleinen Kern · 35★
- [saicogn/ThreadX-to-RISC-V64](https://github.com/saicogn/ThreadX-to-RISC-V64) — ThreadX-Portierung · 8★
- [Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK](https://github.com/Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK) — Bare-Metal auf beiden Kernen ohne SDK · 11★
- [zuki/xv6-milkv-duo](https://github.com/zuki/xv6-milkv-duo) — xv6 on Duo · 7★
- [jiegegena/milkv-sg2002-xv6](https://github.com/jiegegena/milkv-sg2002-xv6) — xv6 on SG2002
- [Lam920/xv6-cv1800b](https://github.com/Lam920/xv6-cv1800b) — xv6 on CV1800B
- [rota1001/milkv-baremetal-toolkit](https://github.com/rota1001/milkv-baremetal-toolkit) — Bare-Metal-Images mit einem Befehl erzeugen · 8★
- [PeterForth/MILKV-FORTH](https://github.com/PeterForth/MILKV-FORTH) — Forth auf dem Duo · 8★
- [xingrz/milkv-duo-zephyr-mailbox-example](https://github.com/xingrz/milkv-duo-zephyr-mailbox-example) — Mailbox-Kommunikation zwischen Zephyr und Linux

**Toolchain und Build-Umgebung**

- [aidancrowther/Milk-V-Duo-Docker-Compile](https://github.com/aidancrowther/Milk-V-Duo-Docker-Compile) — Docker-Image mit vorinstallierter Toolchain · 24★
- [Tosainu/docker-milkv-duo-linux](https://github.com/Tosainu/docker-milkv-duo-linux) — Linux im Container bauen
- [boberace/milkv_duo_dc](https://github.com/boberace/milkv_duo_dc) — VS Code Dev Container
- [kitnerboy/milkv-duo-buildroot](https://github.com/kitnerboy/milkv-duo-buildroot) — Buildroot-BSP nach Mainline-Vorbild

**Treiber und Peripherie**

- [hexdump0815/linux-cvitek-cv18xx-kernel](https://github.com/hexdump0815/linux-cvitek-cv18xx-kernel) — Kernel-Baum der Community (Kernelquelle mehrerer Images)
- [ret7020/CVI_HW_OpenCV](https://github.com/ret7020/CVI_HW_OpenCV) — OpenCV-Portierung mit NPU-Beschleunigung · 7★
- [pavelanni/gpiod-milkvduo](https://github.com/pavelanni/gpiod-milkvduo) — Verwendung von libgpiod · 3★
- [Satharus/I2C-WiringX-Milk-V](https://github.com/Satharus/I2C-WiringX-Milk-V) — I²C über wiringX · 2★
- [KuLvo/milk-v_duo_oled_driver](https://github.com/KuLvo/milk-v_duo_oled_driver) — Treiber für 0,96-Zoll-OLED · 3★
- [queenkjuul/aic8800-milkv-duos](https://github.com/queenkjuul/aic8800-milkv-duos) — Anpassung für AIC8800 WiFi+BT
- [GrootLiu/milkv-duo-rtl8723du](https://github.com/GrootLiu/milkv-duo-rtl8723du) — RTL8723DU-WiFi-Portierung
- [Tactical-TV-Remote/infrared_milkv](https://github.com/Tactical-TV-Remote/infrared_milkv) — Infrarot-Senden und -Empfangen (Rust)
- [harshareddy1611/milkv-duo-s-baremetal-drivers](https://github.com/harshareddy1611/milkv-duo-s-baremetal-drivers) — Bare-Metal GPIO/UART für das Duo S
- [wanghengZzz/Milkv-Duo-FreeRTOS-DMA](https://github.com/wanghengZzz/Milkv-Duo-FreeRTOS-DMA) — FreeRTOS-DMA-HAL

**Projekte aus der Praxis**

- [pavelanni/milkv-duo-experiments](https://github.com/pavelanni/milkv-duo-experiments) — Sammlung von Experimenten in Go · 27★
- [driver1998/DiscEmu](https://github.com/driver1998/DiscEmu) — CD-ROM-Emulator mit dem Duo · 11★
- [0x1iii1ii/Pwn-V-Duo](https://github.com/0x1iii1ii/Pwn-V-Duo) — Portierung des PPPwn-Exploits · 6★
- [aceraoc/MilkV-Duo_TPU](https://github.com/aceraoc/MilkV-Duo_TPU) — Beispiele für TPU-Inferenz · 8★
- [xmdjy/milkv-car](https://github.com/xmdjy/milkv-car) — intelligentes Fahrzeug auf Basis des Duo
- [Arielfoever/milkv-duo-yolo11](https://github.com/Arielfoever/milkv-duo-yolo11) — YOLO11-Deployment
- [Basicname/SG200x_GC2083_Yolov8_11](https://github.com/Basicname/SG200x_GC2083_Yolov8_11) — YOLOv8/11 + GC2083 in einer einzigen Datei
- [chius-me/globi-v](https://github.com/chius-me/globi-v) — Sehassistenz-System für das Duo S
- [f3jry/milkv-duo-xmrsigner](https://github.com/f3jry/milkv-duo-xmrsigner) — Monero-Cold-Wallet auf das Duo portiert
- [sdwood68/MilkV_Duo_S_Camera](https://github.com/sdwood68/MilkV_Duo_S_Camera) — Kameraknoten für Frigate / Home Assistant
- [ar90n/ptp-server-milkv-duos](https://github.com/ar90n/ptp-server-milkv-duos) — PTP-Master-Clock-Server
- [avalitan/MilkV-Duo-S-NTP-UPS-Server](https://github.com/avalitan/MilkV-Duo-S-NTP-UPS-Server) — NTP- und NUT-UPS-Überwachung
- [vojinvukcevic/boot-time-optimization-milkv](https://github.com/vojinvukcevic/boot-time-optimization-milkv) — vollständige Dokumentation: Kaltstart von 14,1 s auf 3,2 s verkürzt

**Hardware und Gehäuse**

- [iyegoroff/milkv-duo-s-case](https://github.com/iyegoroff/milkv-duo-s-case) — parametrisches 3D-Druck-Gehäuse für das Duo S · 12★
- [pauleffect90/MilkVDuoKicad](https://github.com/pauleffect90/MilkVDuoKicad) — KiCad-Symbole und -Footprints · 4★
- [Tosainu/milkv-duo-iob](https://github.com/Tosainu/milkv-duo-iob) — Designdateien für das IO-Erweiterungsboard

---

## 11. Gitee-Projekte und chinesischsprachige Anleitungen

**Gitee (19 Stück)**

- [tinylab/milkv-buildroot](https://gitee.com/tinylab/milkv-buildroot) — Buildroot-Buildprojekt für die Images der TinyLab-Community
- [tinylab/duo-buildroot-sdk](https://gitee.com/tinylab/duo-buildroot-sdk) — in China gehosteter Mirror des offiziellen V1 SDK
- [tinylab/duo-examples](https://gitee.com/tinylab/duo-examples) — in China gehosteter Mirror der offiziellen Beispiele
- [tinylab/i2c-lsm6dsr](https://gitee.com/tinylab/i2c-lsm6dsr) — I²C-Beispiel für den LSM6DSR-Sensor
- [weilinfox/pinpong-milkv-duo-doc](https://gitee.com/weilinfox/pinpong-milkv-duo-doc) — pinpong auf dem Duo ausführen · 3★
- [lan-ruixin/duo-buildroot-sdk](https://gitee.com/lan-ruixin/duo-buildroot-sdk) — persönlich gepflegter V1-Zweig mit ergänzter chinesischer Build-Anleitung
- [lan-ruixin/milkv-duo-rtl8723du](https://gitee.com/lan-ruixin/milkv-duo-rtl8723du) — Anpassung für RTL8723DU WiFi/Bluetooth
- [qhw136/milkv_duo_sdk](https://gitee.com/qhw136/milkv_duo_sdk) — erweitertes SDK mit LCD/Touch/WiFi/Bluetooth
- [zhidao101/Milkv_duo_Ubuntu_image](https://gitee.com/zhidao101/Milkv_duo_Ubuntu_image) — Ubuntu-22.04-Images für 256M und 512MB
- [tiberium/duosdk2yocto](https://gitee.com/tiberium/duosdk2yocto) — das SDK in einen Yocto-Build umwandeln
- [tiberium/meta-milkv-duo-sdk](https://gitee.com/tiberium/meta-milkv-duo-sdk) — zugehöriger Meta-Layer
- [fixxer2020/duo-multimedia-examples](https://gitee.com/fixxer2020/duo-multimedia-examples) — Mirror der Multimedia-Beispiele
- [dongshan-community/DongShanPiExtboard](https://gitee.com/dongshan-community/DongShanPiExtboard) — mini-ITX-Erweiterungsboard für das Duo 256M
- [linux-proj/Milkv-duo_Cross_Compile_software](https://gitee.com/linux-proj/Milkv-duo_Cross_Compile_software) — vorkompilierte Cross-Compile-Abhängigkeitspakete
- [atari/opencv-mobile](https://gitee.com/atari/opencv-mobile) — synchronisierter Stand von opencv-mobile (riscv64-musl, Hardware-JPG-Dekodierung, MIPI CSI) · 5★
- [unicornx/riscv-operating-system-mooc](https://gitee.com/unicornx/riscv-operating-system-mooc) — Kurs-Code des RVOS (bereits auf das Duo portiert) · 541★
- [openeuler/UniProton](https://gitee.com/openeuler/UniProton) — enthält `demos/milkv-duo` mit Beispielen für großen und kleinen Kern · 73★ (das Repository ist inzwischen zu AtomGit umgezogen)
- [k0059/duo-buildroot-sdk-v2](https://gitee.com/k0059/duo-buildroot-sdk-v2) — sg200x-evb-Zweig von SDK V2
- [xju_kjc/duo-buildroot-sdk](https://gitee.com/xju_kjc/duo-buildroot-sdk) — vollständiger Mirror des V1 SDK (README auf Chinesisch/Japanisch/Englisch)

**Chinesischsprachige Anleitungen und Artikel (22 Stück)**

- 博客园 [milkv-duo 启动流程分析：手动构建 fip.bin [1/2]](https://www.cnblogs.com/maomaotou-thu/p/17765721.html) · [2/2](https://www.cnblogs.com/maomaotou-thu/p/17766024.html) · [手动构建 boot.sd](https://www.cnblogs.com/maomaotou-thu/p/17767315.html) — Pflichtlektüre, wenn Sie die Boot-Kette verstehen wollen
- 博客园 [Milk-V Duo S 使用报告](https://www.cnblogs.com/BiaoZyx/p/18956632) — vom Auspacken bis zum Test der Peripherie, inklusive Stolperfallen
- 博客园 [大作业：milkv-duo 小车设计工作日志](https://www.cnblogs.com/Cybersites/p/18859275)
- 博客园 [小核引导 RTOS —— RISC-V C906](https://www.cnblogs.com/gaoyang3513/articles/18854508)
- 博客园 [集成构建流程之根文件系统 Buildroot](https://www.cnblogs.com/gaoyang3513/p/18854502) · [网络升级固件](https://www.cnblogs.com/gaoyang3513/p/18854509) · [以太网使用与配置](https://www.cnblogs.com/gaoyang3513/p/18854518) · [Docker 开发环境搭建](https://www.cnblogs.com/gaoyang3513/p/18854511)
- 博客园 [milkv duo 256M 使用 Debian 系统](https://www.cnblogs.com/GrootStudy/p/18225934)
- 博客园 [milkV-duo 的 Linux 开发环境搭建](https://www.cnblogs.com/yzh0526/p/18098794)
- 博客园 [milk-v duo 开机引导进入 rust 程序](https://www.cnblogs.com/longxiangam/p/19640491)
- 掘金 [milkv-duo 开发环境搭建 & 烧录](https://juejin.cn/post/7269416466314821668) · [打包 SDK 时遇到的问题及解决](https://juejin.cn/post/7269417409370505235) · [小奶板点灯 & sensor bring up](https://juejin.cn/post/7269644295588659261) · [image burn](https://juejin.cn/post/7269424598260334648) · [milkv 256duo 初品](https://juejin.cn/post/7355829021311238182)
- Bilibili-Kolumnen [Milk-v Duo：35 块带 TPU 1GHz 的 Linux 开发板](https://www.bilibili.com/read/cv24253633) · [Linux 与 RTOS 双核开发实践](https://www.bilibili.com/read/cv27449966) · [Duo S 部署 PicoClaw 完整教程](https://www.bilibili.com/read/cv46804507) · [Ubuntu 20.04 详细编译环境搭建指南](https://www.bilibili.com/read/cv24743710)

> **CSDN und Zhihu fehlen noch**: Beide Seiten antworten in diesem Netz mit 521 / 403 (auch der direkte Aufruf im Browser wird blockiert) und bestehen die Prüfung „Seite existiert tatsächlich“ daher nicht; ungeprüfte Links werden deshalb nicht aufgenommen. Auch die RT-Thread-Q&A-Community `club.rt-thread.org` wird von einer WAF blockiert. Ergänzung folgt, sobald die Seiten direkt erreichbar sind.

---

## 12. Wie dieser Index gepflegt wird

- Täglich um 14:00 Uhr läuft automatisch ein inkrementeller Scan des gesamten Netzes (offizielle Releases, neue Seiten der Dokumentation, neue Videos, neue Repositories); bei Änderungen wird ein Update eingereicht
- Aufgenommen werden nur Links, die sich **öffnen lassen**; bei jeder Aktualisierung läuft eine vollständige Linkprüfung, tote Links werden entfernt oder durch neue Adressen ersetzt
- Bei Videos muss das Duo tatsächlich verwendet worden sein; bei Projekten muss das Repository diese Boards wirklich unterstützen (nicht nur nebenbei erwähnen)
- Die Aufnahme ist keine Empfehlung. Sicherheit, Lizenz und Wartungsstand von Images und Projekten Dritter sind selbst zu beurteilen
- Fehlende Ressourcen gern als Issue oder PR melden; beim PR bitte in die vorhandene Gliederung einsortieren und das passende Board angeben (Duo / Duo 256M / Duo S)

[Zurück zum Sprachindex](README.md)
