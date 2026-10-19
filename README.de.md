# Ressourcen zu Milk-V Duo, Duo 256M und Duo S

Diese Sammlung bündelt offizielle Dokumentation, Firmware, Quellcode, Hardware-Unterlagen, Anleitungen und Community-Projekte für die Milk-V-Duo-Familie. Eine vollständige Erfassung aller Online-Ressourcen ist nicht möglich; Ergänzungen und Hinweise auf defekte Links sind willkommen.

> **Vor der Nutzung die Kompatibilität prüfen.** Das ursprüngliche Duo verwendet den CV1800B und hat 64 MB RAM; das Duo 256M verwendet den SG2002 und hat 256 MB; das Duo S verwendet den SG2000 und hat 512 MB. Hardware und Software-Ziele unterscheiden sich zwischen den Boards. In der offiziellen Übersicht ist das ursprüngliche Duo als abgekündigt (EOL) gekennzeichnet. Betriebssysteme und Images von Drittanbietern werden von der Community gepflegt und sind möglicherweise nicht getestet.

## Offizielle Produkte und Dokumentation

- [Übersicht und Spezifikationen der Duo-Familie](https://milkv.io/docs/duo/overview) — Board-Vergleich, Funktionen und Hinweise zum Produktlebenszyklus.
- Board-Anleitungen: [Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos).
- Erste Schritte: [Booten](https://milkv.io/docs/duo/getting-started/boot) · [Images herunterladen und auswählen](https://milkv.io/docs/duo/getting-started/download) · [Buildroot-SDK-Anleitung](https://milkv.io/docs/duo/getting-started/buildroot-sdk).
- Produktseiten: [Duo](https://milkv.io/duo) · [Duo 256M](https://milkv.io/duo256m) · [Duo S](https://milkv.io/duos).
- [Quellcode der offiziellen Dokumentation](https://github.com/milk-v/milkv.io) — Beiträge für Korrekturen und Übersetzungen.

## Firmware, SDKs und Toolchains

- [Katalog offizieller Images und Kompatibilitätshinweise](https://milkv.io/docs/duo/getting-started/download).
- Offizielle Firmware-Releases: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk/releases) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases).
- SDK-Quellcode: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [Host-Tools](https://github.com/milkv-duo/host-tools).
- Laut offizieller Download-Anleitung wird V1 für das Duo mit 64 MB und V2 für Duo 256M und Duo S empfohlen. Release-Hinweise und Zielnamen trotzdem immer prüfen.
- [Offizielle C/C++-Beispiele und Einrichtung der Cross-Toolchain](https://github.com/milkv-duo/duo-examples), darunter [GPIO-Blinken](https://github.com/milkv-duo/duo-examples/tree/main/blink), [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c), [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) und der [Peripherie-Leitfaden (PDF)](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf).

## Hardware, Peripherie und Anwendungsentwicklung

- [Offizielle Board-Dateien, Schaltpläne, Datenblätter und mechanische Zeichnungen](https://github.com/milkv-duo/duo-files).
- Board-Schaltpläne: [Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf).
- [Datenblätter und technische Unterlagen zu Sophgo-Chips](https://github.com/sophgo/sophgo-doc/releases).
- SoC-Unterlagen: [vorläufiges CV1800B/CV1801B-Datenblatt (Englisch)](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf) und [chinesische Ausgabe](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf) · [vorläufiges SG2002-Datenblatt (Chinesisch)](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [vorläufiges SG2000-Datenblatt (Chinesisch)](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) und [Technical Reference Manual (Englisch)](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf).
- Offizielle Entwicklungsprojekte: [Pin-Multiplexing](https://github.com/milkv-duo/duo-pinmux) · [wiringX](https://github.com/milkv-duo/duo-wiringx) · [Zubehör](https://github.com/milkv-duo/accessories) · [LVGL-Framebuffer-Demo](https://github.com/milkv-duo/duo-lvgl-fb-demo).
- Dokumentation: [GPIO und Pin-Multiplexing](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [USB-Kameras](https://milkv.io/docs/duo/camera/usb) · [Multimedia-Framework](https://milkv.io/docs/duo/application-development/multimedia).
- Arduino: Der alte [Milk-V-Arduino-Core](https://github.com/milkv-duo/duo-arduino) ist archiviert; das Repository verweist auf [Sophgo Arduino](https://github.com/kubuds/sophgo-arduino). Zusätzlich gibt es [Duo-Arduino-Beispiele](https://github.com/milkv-duo/duo-arduino-examples). Vor der Nutzung die Unterstützung von Board und Core prüfen.

## KI, Computer Vision und Medien

- TDL-Beispiele: [SDK V1 für CV180X / das ursprüngliche Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SDK V1 für SG200X / Duo 256M und Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [SDK-V2-Beispiele](https://github.com/milkv-duo/duo-tdl-examples).
- TPU- und Modellwerkzeuge: [CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [TPU-MLIR-Modellkonvertierung](https://github.com/milkv-duo/tpu-mlir) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x).
- [Offizielle Multimedia-Beispiele](https://github.com/milkv-duo/duo-multimedia-examples) · [TDL-Modellbereitstellung](https://github.com/milkv-duo/duo-yolo-deployment).
- Die [offizielle Download-Anleitung](https://milkv.io/docs/duo/getting-started/download) führt außerdem Community-Images nach Board auf. Warnhinweise beachten und Maintainer sowie unterstützte Hardware-Revision prüfen.

## Community-Betriebssysteme und Lernmaterial

Dies sind unabhängige Community-Projekte und keine offizielle Firmware. Kompatibilität und Pflege können sich ändern; vor der Installation die jeweilige Projektdokumentation lesen.

- Linux-Distributionen: [Fedora-Image-Spiegel](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/) · [Debian für Sophgo SG200X](https://github.com/scpcom/sophgo-sg200x-debian) · [Ubuntu-Image-Builder](https://github.com/ambraglow/milkv-duo-ubuntu) · [OpenWrt/VizOS-Projekt](https://github.com/Pillar1989/VizOS).
- Buildsysteme und RTOS: [Yocto-/OpenEmbedded-Layer](https://github.com/kinsamanka/meta-milkv) · [Zephyr auf dem Zweitkern des Duo](https://github.com/kinsamanka/milkv-zephyros) · [NuttX für SG2000 / Duo S](https://github.com/lupyuen/nuttx-sg2000) · [RT-Thread-CVitek-BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) · [ThreadX-Port](https://github.com/saicogn/ThreadX-to-RISC-V64).
- [Milk-V-Duo-Community-Forum](https://community.milkv.io/c/duo/5) · [Sophgo-Forum](https://forum.sophgo.com/) · [Milk-V-Duo-GitHub-Organisation](https://github.com/milkv-duo).

## Mitwirken und Links aktuell halten

Bitte ein Issue oder einen Pull Request eröffnen, wenn ein Link nicht funktioniert, eine Ressource fehlt oder sich die unterstützten Boards eines Projekts geändert haben. Möglichst auf Dokumentation und Release-Seiten der Maintainer verweisen und Firmware nicht erneut hosten. Vor dem Flashen Board, SoC, Speichergröße, Speichertyp, Bootmodus und Image-Anleitung prüfen, Daten sichern und auf sichere Stromversorgung und Verkabelung achten.

[Zurück zum Sprachindex](README.md)
