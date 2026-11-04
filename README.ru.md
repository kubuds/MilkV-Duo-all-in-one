# Сводный указатель ресурсов семейства Milk-V Duo (Duo · Duo 256M · Duo S)

Всё, что удалось найти по семейству Milk-V Duo, собрано на этой странице: официальная документация и даташиты, образы для прямой загрузки, SDK и инструментальные цепочки, открытые проекты на GitHub и Gitee, а также видео на Bilibili и YouTube, в которых эти платы действительно используются.

Страница не копирует и не зеркалирует прошивки и документы: указаны только источники и сопровождающие. **Образы и проекты сообщества не тестировались и не одобрялись Milk-V**, поэтому перед прошивкой самостоятельно сверяйте модель платы, SoC, объём памяти, носитель и примечания к выпуску.

> **Сначала определите, какая плата у вас в руках.** Три поколения — это не одно и то же: в Duo используется CV1800B (64 МБ памяти), в Duo 256M — SG2002 (256 МБ и дополнительное ядро Cortex-A53), в Duo S — SG2000 (512 МБ, опционально Wi-Fi 6 / BT5 и опционально eMMC). **Оригинальный Duo официально помечен как снятый с производства (EOL)**, поэтому новые проекты лучше сразу строить на 256M или Duo S.

---

## 1. Платы и варианты

| Модель | SoC | Память | Накопитель | Беспроводная связь | Ethernet | TPU | Статус |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Duo** | CVITEK CV1800B | 64 MB | microSD или SD NAND на плате | нет | 100M (PHY) | 0.5 TOPS@INT8 | снят с производства, EOL |
| **Duo 256M** | SG2002 | 256 MB | microSD или SD NAND на плате | нет | 100M (PHY) | 1.0 TOPS@INT8 | в продаже |
| **Duo S** | SG2000 | 512 MB | microSD + место под eMMC на плате | **опционально** Wi-Fi 6 / BT5 | 100M (RJ45, поддержка PoE HAT) | 0.5 TOPS@INT8 | в продаже |
| **Duo Module 01** (ядро + отладочная плата) | SG2000 | 512 MB | 8 GB eMMC на плате | Wi-Fi 6 / BT5.4 на плате | 2× 100M | 0.5 TOPS@INT8 | в продаже |

**Четыре комбинации Duo S**: с припаянным eMMC или без него × с припаянным модулем Wi-Fi или без него — всего четыре SKU. При покупке уточняйте, какой именно вариант указан на странице товара.

Образы **различаются только по носителю загрузки** (`-sd` / `-emmc`) и не различаются по наличию Wi-Fi: среди семи файлов официального релиза v2.0.1 нет ни одного образа со словом wifi в имени (см. таблицу ниже). Отсюда следует:

- Платы Duo S с Wi-Fi и без него прошиваются одним и тем же образом: беспроводная связь работает только при наличии припаянного модуля на плате
- Плату с eMMC можно прошить образом `-sd` и загружаться с карты TF, а можно образом `-emmc` — в бортовую память
- Плата **без** eMMC может загружаться только с карты TF

---

## 2. Где купить

В магазине Kubuds (苦芽企业店) на Taobao продаются эти три варианта (для просмотра карточки нужен вход в Taobao; сами ссылки отдают 200):

- **Milk-V Duo 256M** (SG2002, 256 MB, без Wi-Fi): https://item.taobao.com/item.htm?id=842972320584&skuId=5661357677549
- **Milk-V Duo S, базовая версия** (SG2000, 512 MB, без Wi-Fi и без eMMC): https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544644
- **Milk-V Duo S Wi-Fi** (SG2000, 512 MB, с Wi-Fi 6 / BT, без eMMC): https://item.taobao.com/item.htm?id=842237425635&skuId=5659147544645

Две позиции Duo S — это **два SKU одного товара** (одинаковый `id`, разные `skuId`); при заказе проверяйте, есть ли Wi-Fi в названии SKU. eMMC нет ни у одной, поэтому для бортовой памяти ищите версию с eMMC отдельно. Оригинальный Duo (CV1800B) снят с производства, ссылки на покупку для него нет.

Это единственная коммерческая часть страницы; всё остальное указывает только на первоисточники.

---

## 3. Официальная документация, даташиты и аппаратные материалы

**Сайт документации: постраничный указатель**

- Начало: [обзор семейства Duo и сравнение характеристик](https://milkv.io/docs/duo/overview) (полная таблица характеристик всех четырёх продуктов, оттуда же взято заявление об EOL) · [главная страница документации](https://milkv.io/docs/duo/getting-started)
- Руководства по платам: [Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos) · [Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- Питание и прошивка: [загрузка системы](https://milkv.io/docs/duo/getting-started/boot) · [первое подключение и USB-сеть](https://milkv.io/docs/duo/getting-started/setup) · [сводная таблица образов](https://milkv.io/docs/duo/getting-started/download) · [сборка Buildroot SDK](https://milkv.io/docs/duo/getting-started/buildroot-sdk)
- Два ядра и низкий уровень: [разработка для вспомогательного ядра 8051](https://milkv.io/docs/duo/getting-started/8051core) · [разработка RTOS для малого ядра](https://milkv.io/docs/duo/getting-started/rtoscore) · [поддержка Arduino](https://milkv.io/docs/duo/getting-started/arduino) · [низкоуровневая разработка](https://milkv.io/docs/duo/low-level-dev) ([MIPI DSI](https://milkv.io/docs/duo/low-level-dev/mipi-dsi))
- Разработка приложений: [обзор](https://milkv.io/docs/duo/application-development) · [GPIO sysfs](https://milkv.io/docs/duo/application-development/gpio-sysfs) · [мультиплексирование выводов](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [pinpong](https://milkv.io/docs/duo/application-development/pinpong) · [мультимедийный фреймворк](https://milkv.io/docs/duo/application-development/multimedia)
- Камеры: [USB-камера](https://milkv.io/docs/duo/camera/usb) · [датчик GC2083](https://milkv.io/docs/duo/camera/gc2083) · [ISP tuning](https://milkv.io/docs/duo/camera/tuning)
- TPU и TDL: [введение в TPU](https://milkv.io/docs/duo/application-development/tpu/tpu-introduction) · [введение в TDL SDK](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-introduction) · YOLO: [v5](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov5) · [v8](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov8) · [v11](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo11) · [v12](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo12) · [обнаружение лиц](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-face-detection) · [обнаружение пешеходов](https://milkv.io/docs/duo/application-development/tdl-sdk/pedestrian-detection) · [обнаружение людей и домашних животных](https://milkv.io/docs/duo/application-development/tdl-sdk/yolov8-person-pets-detection)
- Платы расширения IO: [обзор IO Board](https://milkv.io/docs/duo/io-board) · [Duo S PoE HAT](https://milkv.io/docs/duo/io-board/duos-poe-hat) · [IO-плата USB Ethernet](https://milkv.io/docs/duo/io-board/usb-ethernet-iob)
- Официальная подборка ресурсов и состояние экосистемы: [сводная таблица полезных ресурсов](https://milkv.io/docs/duo/useful-resources) · [состояние поддержки в mainline-ядре](https://milkv.io/docs/duo/resources/mainline) · [текущее состояние поддержки в upstream](https://milkv.io/docs/duo/resources/upstream-status) · [мультимедийный фреймворк MMF](https://milkv.io/docs/duo/resources/mmf) · [OpenCV Mobile](https://milkv.io/docs/duo/resources/opencv-mobile) · [SPILVGL](https://milkv.io/docs/duo/resources/spilvgl) · [Visuino](https://milkv.io/docs/duo/resources/visuino) · [заметки xyzdims](https://milkv.io/docs/duo/resources/xyzdims)
- [Исходный код сайта документации](https://github.com/milk-v/milkv.io) — сюда отправляйте PR, если нашли ошибку в документации или хотите добавить перевод

**Страницы продуктов**

- [Duo (страница серии)](https://milkv.io/duo) · [Duo S](https://milkv.io/duo-s) · [Duo Module 01](https://milkv.io/duo-module-01)
- У Duo 256M нет отдельной страницы товара: характеристики приведены на странице серии и в [документации](https://milkv.io/docs/duo/getting-started/duo256m)

**Аппаратные файлы и документация на микросхемы**

- [duo-files](https://github.com/milkv-duo/duo-files) — общее хранилище официальных файлов плат: схемы, даташиты, механические чертежи, шелкография
- Схемы: [Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)
- Даташиты: [CV1800B/CV1801B, английский](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf) ([китайский](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf)) · [SG2002, китайский](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000, китайский](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 TRM, английский](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)
- [Страница публикации документации Sophgo](https://github.com/sophgo/sophgo-doc/releases) — официальный канал документации на микросхемы от upstream

---

## 4. Официальные образы и прошивка

Все официальные образы основаны на Buildroot и делятся на две ветки — V1 и V2. **Для Duo с 64 МБ рекомендуется V1** (примеры ИИ из V2 на 64 МБ не работают); для Duo 256M и Duo S используется V2.

### V2 (рекомендуется для Duo 256M / Duo S) · [v2.0.1, 2025-05-30](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)

| Файл образа | Плата | Носитель загрузки | C-библиотека / архитектура |
| --- | --- | --- | --- |
| `milkv-duo-musl-riscv64-sd_v2.0.1.img.zip` | Duo | карта TF | musl / riscv64 |
| `milkv-duo256m-musl-riscv64-sd_v2.0.1.img.zip` | Duo 256M | карта TF | musl / riscv64 |
| `milkv-duo256m-glibc-arm64-sd_v2.0.1.img.zip` | Duo 256M | карта TF | glibc / arm64 (через A53) |
| `milkv-duos-musl-riscv64-sd_v2.0.1.img.zip` | Duo S | карта TF | musl / riscv64 |
| `milkv-duos-glibc-arm64-sd_v2.0.1.img.zip` | Duo S | карта TF | glibc / arm64 (через A53) |
| `milkv-duos-musl-riscv64-emmc_v2.0.1.zip` | Duo S (требуется eMMC) | eMMC на плате | musl / riscv64 |
| `milkv-duos-glibc-arm64-emmc_v2.0.1.zip` | Duo S (требуется eMMC) | eMMC на плате | glibc / arm64 |

### V1 · [v1.1.4, 2024-11-22](https://github.com/milkv-duo/duo-buildroot-sdk/releases)

| Файл образа | Плата | Носитель загрузки |
| --- | --- | --- |
| `milkv-duo-sd-v1.1.4.img.zip` | Duo | карта TF |
| `milkv-duo256m-sd-v1.1.4.img.zip` | Duo 256M | карта TF |
| `milkv-duos-sd-v1.1.4.img.zip` | Duo S | карта TF |
| `milkv-duos-emmc-v1.1.4.zip` | Duo S (требуется eMMC) | eMMC на плате |
| `arduino-milkv-duo-sd-v1.1.4.img.zip` и ещё 3 | три платы | та же схема имён, образы с предустановленным Arduino |

### Ключевые моменты прошивки

- Образ для карты TF: распакуйте и запишите через balenaEtcher / `dd`, вставьте карту и подайте питание; **SSH и сетевой интерфейс USB-NCM включены по умолчанию, пароль root — `milkv`**
- Образ для eMMC: это **не** то же самое, что запись образа на карту TF. На Duo S нужно удерживать кнопку Recovery и подключить плату к компьютеру кабелем Type-C, после чего прошить через USB утилитой CVITEK `usb_dl.exe` (Windows) или `CviBurn`; перед прошивкой обязательно извлеките карту TF
- На Duo S есть **переключатель загрузки ARM / RISC-V**; если прошивка не соответствует положению переключателя, плата не загрузится. Первый символ в журнале последовательного порта — `C` при загрузке с RISC-V и `B` при загрузке с ARM
- На Duo S порты Type-C (USB-NCM) и Type-A (USB HOST) **не могут работать одновременно**; переключение выполняется через символическую ссылку `/mnt/system/usb.sh`

---

## 5. Сторонние образы (поддерживаются сообществом, сгруппированы по платам)

На официальной странице загрузки есть [таблица сторонних образов](https://milkv.io/docs/duo/getting-started/download); здесь она развёрнута по платам, чтобы по ссылкам можно было переходить сразу.

### Duo (CV1800B, 64 MB)

- [Зеркало Fedora 41](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo/images/latest/) — поддерживается Fedora-V Force, следует за upstream
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) — скрипты сборки образа, подходят и для Duo 256M
- [Сборщик образов Debian / Ubuntu](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — используйте его для сборки собственных образов
- [Arch Linux](https://community.milkv.io/t/arch-linux-on-milkv-duo-milkv-duo-arch-linux/329) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1) · [полный образ Debian](https://community.milkv.io/t/milkv-duo-duo-debian-full-7z-519m-download/862)
- [OpenWrt / VizOS](https://github.com/Pillar1989/VizOS) · [Zephyr (вспомогательное ядро)](https://github.com/kinsamanka/milkv-zephyros) · [слой Yocto](https://github.com/kinsamanka/meta-milkv)
- [RT-Thread cvitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) ([руководство по программированию на RISC-V RT-Thread](https://riscv-rtthread-programming-manual.readthedocs.io/zh-cn/latest/)) · [порт ThreadX](https://github.com/saicogn/ThreadX-to-RISC-V64)

### Duo 256M (SG2002)

- [Зеркало Fedora 41](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo256M/images/latest/)
- [Debian (Fishwaldo / sophgo-sg200x-debian)](https://github.com/Fishwaldo/sophgo-sg200x-debian/releases/tag/v1.2.0)
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) · [Arch Linux](https://community.milkv.io/t/debian-arch-linux-on-milkv-duo-256m-milkv-duo-256m-debian-arch-linux/1110) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1)

### Duo S (SG2000)

- [Зеркало Fedora 41](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/DuoS/images/latest/) — учётная запись по умолчанию `root`, пароль `riscv`
- [Debian (scpcom)](https://github.com/scpcom/sophgo-sg200x-debian/releases) — два набора учётных данных: `root`/`rv` и `debian`/`rv`
- [NuttX (lupyuen)](https://github.com/lupyuen/nuttx-sg2000/releases) — готовый образ с NuttX для Duo S

---

## 6. SDK, инструментальные цепочки и примеры

- Исходный код SDK: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [инструментальная цепочка для хост-системы](https://github.com/milkv-duo/host-tools)
- [duo-examples](https://github.com/milkv-duo/duo-examples) — официальные примеры на C/C++: [мигание GPIO](https://github.com/milkv-duo/duo-examples/tree/main/blink) · [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c) · [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) · [руководство по работе с драйверами периферии (PDF)](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) (мультиплексирование выводов) · [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) (порт wiringX) · [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) (LVGL framebuffer) · [duo-accessories](https://github.com/milkv-duo/accessories) (официальные аксессуары)
- Arduino: [архивированная официальная библиотека ядра](https://github.com/milkv-duo/duo-arduino) (репозиторий перенаправляет на [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)) · [примеры Arduino для Duo](https://github.com/milkv-duo/duo-arduino-examples)
- Инструменты для SoC: [CV180X TPU SDK](https://github.com/milkv-duo/tpu-sdk-cv180x) · [SG200X TPU SDK](https://github.com/milkv-duo/tpu-sdk-sg200x) · [преобразование моделей TPU-MLIR](https://github.com/milkv-duo/tpu-mlir)
- TDL (примеры глубокого обучения): [CV180X / Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SG200X / Duo 256M & Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [примеры TDL для SDK V2](https://github.com/milkv-duo/duo-tdl-examples) · [развёртывание YOLO](https://github.com/milkv-duo/duo-yolo-deployment)
- Мультимедиа: [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples)

---

## 7. Официальная организация, сообщество и общение

- [Организация milkv-duo на GitHub](https://github.com/milkv-duo) — здесь собраны официальные SDK, примеры и аппаратные файлы
- [Раздел Duo в сообществе Milk-V](https://community.milkv.io/c/duo/5) — основное место для вопросов и обмена опытом
- [Документация отладочной платы Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- Прежний `forum.sophgo.com` больше недоступен (в 2026-10 проверено: соединение не устанавливается), материалы по микросхемам теперь берутся из [sophgo-doc](https://github.com/sophgo/sophgo-doc/releases)

---

## 8. Видео: Bilibili (50 роликов)

Для каждого ролика проверено, что страница существует (HTTP 200), а заголовок и описание действительно относятся к семейству Duo; число просмотров — снимок на 2026-10-31, приводится только как ориентир по популярности.

**Серия 东东老师 (eastdong) — лучше всего подходит для старта с нуля**

- 《零压力上手 RISC-V：东东老师带你玩转 milk-v duo》01. RVOS on Duo — [BV1vm421E7R6](https://www.bilibili.com/video/BV1vm421E7R6/) · 9578
- 02. RT-Thread on Duo — [BV1ym411z7Qo](https://www.bilibili.com/video/BV1ym411z7Qo/) · 3558
- 04. Camera 和 YOLOv5 图像识别 — [BV1mt421A7tL](https://www.bilibili.com/video/BV1mt421A7tL/) · 2972
- 05. TPU 使用 — [BV1Wi421Q7b4](https://www.bilibili.com/video/BV1Wi421Q7b4/) · 2171
- 06. 完结（补讲 Duo 256M 的新变化）— [BV1Fx4y1W7x9](https://www.bilibili.com/video/BV1Fx4y1W7x9/) · 2212

**苦芽科技 — полный цикл официального курса по Duo S**

- 00. 认识 Milk-V Duo S — [BV1PNDoYeEpT](https://www.bilibili.com/video/BV1PNDoYeEpT/) · 2307
- 01. Windows 下安装及启动 — [BV1u3DYYGES7](https://www.bilibili.com/video/BV1u3DYYGES7/) · 376
- macOS 下安装及启动 — [BV1U5qqYUEAm](https://www.bilibili.com/video/BV1U5qqYUEAm/) · 233
- 02. SPI 演示 — [BV1vYqHYnE8G](https://www.bilibili.com/video/BV1vYqHYnE8G/) · 186

**Знакомство и обзоры**

- 35 块带 TPU、1GHz 的 Linux 开发板，还玩啥树莓派（科学中国）— [BV19h4y1t7Ct](https://www.bilibili.com/video/BV19h4y1t7Ct/) · 1.9 万
- 镜像烧写教程：带 TPU 的 RISC-V Linux 板（斑梨电子）— [BV1uM4y1n763](https://www.bilibili.com/video/BV1uM4y1n763/) · 9098
- 能跑轻量 AI 的最便宜 RISC-V Linux 开发板？Duo 64M（捡个肥仔上战场）— [BV11w411j71u](https://www.bilibili.com/video/BV11w411j71u/) · 9365
- RISC-V 峰会现场 Duo 开箱（半导体都市隶人 Ayla）— [BV1oh4y1K724](https://www.bilibili.com/video/BV1oh4y1K724/) · 8415
- 野生的开发板性能再强又有何用，软件适配稀烂：Duo 256M 尝试 Arduino 彻底失败（沈洁 Eacc）— [BV1sZZHYdEPP](https://www.bilibili.com/video/BV1sZZHYdEPP/) · 8026 ← **негативный обзор, стоит посмотреть**
- 35 元的 milkv-duo Linux 单片机还要啥自行车（开源社区的二掌柜）— [BV1tM4y1Y7kh](https://www.bilibili.com/video/BV1tM4y1Y7kh/) · 2792
- 学习 RISC-V 能跑 Debian & Linux 的最便宜开发板之一（蘭雅 sRGB）— [BV1XQ4y1E7Tj](https://www.bilibili.com/video/BV1XQ4y1E7Tj/) · 3054
- 好玩！RISC-V duo256M 开发板测玩（蘭雅 sRGB）— [BV1Zw411V7bK](https://www.bilibili.com/video/BV1Zw411V7bK/) · 2257
- 麻雀虽小五脏俱全：超高性价比开发板 Milk-V Duo S（qinyunti）— [BV1hyKmzJEw5](https://www.bilibili.com/video/BV1hyKmzJEw5/) · 664

**Настройка окружения и прошивка**

- Linux 下开发环境搭建（future 待续）— [BV1B8411m7jR](https://www.bilibili.com/video/BV1B8411m7jR/) · 3192
- 烧写 Linux 系统 + USB 虚拟 RNDIS 网卡登录（蘭雅 sRGB）— [BV1G14y1k7V4](https://www.bilibili.com/video/BV1G14y1k7V4/) · 1062
- Duo-debian 初体验（蘭雅 sRGB）— [BV11c411o76T](https://www.bilibili.com/video/BV11c411o76T/) · 3416
- Duo 简介和开发环境搭建（谁说现在是冬天呢）— [BV1PF411S7To](https://www.bilibili.com/video/BV1PF411S7To/) · 1959
- Buildroot SDK 简介和编译镜像的方法（谁说现在是冬天呢）— [BV1xc411s7qk](https://www.bilibili.com/video/BV1xc411s7qk/) · 462
- 安装 Hyper-V & 配置 Docker 开发环境（_1dentity）— [BV1nC4y117WS](https://www.bilibili.com/video/BV1nC4y117WS/) · 1826

**Периферия, дисплей и два ядра**

- LVGL 库实战教程 — 刘文涛（群芯闪耀），lazyparser 频道 — [BV1Mp421m7qJ](https://www.bilibili.com/video/BV1Mp421m7qJ/) · 966
- 通过 SPI 驱动 ST7789V 跑 LVGL（谁说现在是冬天呢）— [BV1gLeueWEWr](https://www.bilibili.com/video/BV1gLeueWEWr/) · 2239
- Duo 256M 基于 TinyDRM 驱动 ST7796s 4.0 寸屏并移植 LVGL 8.3（二掌柜）— [BV1Tv421k71W](https://www.bilibili.com/video/BV1Tv421k71W/) · 1230
- USB & Ethernet IO-Board 简介和使用方法（谁说现在是冬天呢）— [BV1Ga4y1Z7oM](https://www.bilibili.com/video/BV1Ga4y1Z7oM/) · 1096
- 通过大核控制小核点亮 LED（谁说现在是冬天呢）— [BV1nH4y1y7CM](https://www.bilibili.com/video/BV1nH4y1y7CM/) · 1057
- 用 Duo 驱动 DF9GMS 微型舵机（谁说现在是冬天呢）— [BV1Dj411E7yD](https://www.bilibili.com/video/BV1Dj411E7yD/) · 571
- Duo S 硬件解码 MP4 并在 LCD 上播放（一只御坂美琴）— [BV1ktvseWEhr](https://www.bilibili.com/video/BV1ktvseWEhr/) · 519

**Портирование систем**

- 在 Duo 上运行 ThreadX（谁说现在是冬天呢）— [BV1yi421C7SK](https://www.bilibili.com/video/BV1yi421C7SK/) · 419
- 在小核上运行 Zephyr OS（谁说现在是冬天呢）— [BV1uK421Y7x9](https://www.bilibili.com/video/BV1uK421Y7x9/) · 435
- 在 Duo 256M 上运行 Arch Linux（谁说现在是冬天呢）— [BV1j8yyYTEp2](https://www.bilibili.com/video/BV1j8yyYTEp2/) · 1274
- 在 Duo S 上启动 NuttX（悲伤的黑山羊）— [BV1RMUeYjELe](https://www.bilibili.com/video/BV1RMUeYjELe/) · 75
- 罗君：Duo 的 UniProton 适配（PLCT 内部报告）（lazyparser）— [BV1RD421G773](https://www.bilibili.com/video/BV1RD421G773/) · 903
- Duo S 启动！（谁说现在是冬天呢）— [BV1Bm421N72y](https://www.bilibili.com/video/BV1Bm421N72y/) · 564
- 使用 Wi-Fi 连接 Duo S（谁说现在是冬天呢）— [BV11r421T7Sk](https://www.bilibili.com/video/BV11r421T7Sk/) · 318
- 在 Duo S 上部署 Caddy 服务器（谁说现在是冬天呢）— [BV1poBzYQEoC](https://www.bilibili.com/video/BV1poBzYQEoC/) · 214
- Duo 256M 部署相册文件管理器和博客笔记（蘭雅 sRGB）— [BV1cC4y1e7uk](https://www.bilibili.com/video/BV1cC4y1e7uk/) · 1455
- Дневник разработки GameOS: самодельная ОС запускает Doom и проигрывает ролики Bilibili по BV-номеру через встроенный клиент «маленький телевизор» (我的大可乐呢; автор не указывает модель платы) — [BV1iZx46BEV7](https://www.bilibili.com/video/BV1iZx46BEV7/) · 38

**ИИ / компьютерное зрение**

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

## 9. Видео: YouTube (37 роликов)

Зарубежный сайт, открывается только через прокси; каждая страница также проверена по отдельности — она существует, и её содержание действительно касается Duo.

**Обзоры и первые шаги**

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

**Начало работы, прошивка и сеть**

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

**Периферия и ИИ**

- Anton Maltsev — Is it good for computer vision? How to start a neural network on it — [dkIVDOd_Fa4](https://www.youtube.com/watch?v=dkIVDOd_Fa4) · Duo
- Mark Birss — Milk-V Duo USB input ST7789 240×240 SPI display — [Swo-zJ6brQI](https://www.youtube.com/watch?v=Swo-zJ6brQI) · Duo
- Sonny Cruz — I²C demo, source in the description — [85uglOz48Pg](https://www.youtube.com/watch?v=85uglOz48Pg) · Duo
- Sonny Cruz — RC servo demo using PWM — [1u2LZJWPtNU](https://www.youtube.com/watch?v=1u2LZJWPtNU) · Duo
- Leigh — Duo + CAM-GC2083: fix RTSP streaming to VLC — [PjiUDsoWCvo](https://www.youtube.com/watch?v=PjiUDsoWCvo) · Duo
- Muhammad Yunus — YOLOX inference on Duo S using TDL SDK + VPSS — [wzUTGK4TuqA](https://www.youtube.com/watch?v=wzUTGK4TuqA) · Duo S

**Портирование систем и проекты на базе платы**

- Muhammad Yunus — RT-Thread on Duo S: the best RTOS for cheap RISC-V? — [WjWM5YoAq-c](https://www.youtube.com/watch?v=WjWM5YoAq-c) · Duo S
- RISC-V Developers — S1E2 Enjoy RISC-V with Milk-V Duo: RT-Thread — [B7EXWE6l9xE](https://www.youtube.com/watch?v=B7EXWE6l9xE) · Duo
- Chris McDonough — NixOS 71: NixOS on RISC-V (Milk-V Duo / Duo 256M) — [-ydXjEWUlGE](https://www.youtube.com/watch?v=-ydXjEWUlGE) · серия Duo
- admin ka — Running Ubuntu glibc 24.04.4 on the Duo 256M — [0Dqbdtjt8Ro](https://www.youtube.com/watch?v=0Dqbdtjt8Ro) · Duo 256M
- 福田重夫 — Running Linux on the Duo 256M (RISC-V + ARM) — [Ga3HX-d8GHQ](https://www.youtube.com/watch?v=Ga3HX-d8GHQ) · Duo 256M
- Nch-Lab — Milk-V Duo 256M を買ったので Linux を動かしてみる — [tcAqYCwbqeU](https://www.youtube.com/watch?v=tcAqYCwbqeU) · Duo 256M
- Mark Birss — Duo 256 CyberDeck LoRa communicator (TLMVC) — [9qOJ3fKwfC0](https://www.youtube.com/watch?v=9qOJ3fKwfC0) · Duo 256M

---

## 10. Открытые проекты на GitHub

Проекты сгруппированы по назначению. Число звёзд и дата последнего коммита — снимок на 2026-10-31, они меняются; пометка «официальный» означает репозиторий в организации milkv-duo.

**Официальные SDK, прошивки и инструменты**

- [duo-buildroot-sdk](https://github.com/milkv-duo/duo-buildroot-sdk) — официальный Buildroot SDK V1 (Duo/CV1800B) · 495★
- [duo-buildroot-sdk-v2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) — официальный SDK V2 (Duo 256M / Duo S, SG200x) · 154★
- [duo-examples](https://github.com/milkv-duo/duo-examples) — официальные примеры периферии на C/C++ · 159★
- [duo-sdk](https://github.com/milkv-duo/duo-sdk) — SDK кросс-компиляции на стороне хост-системы (duo-app-sdk) · 5★
- [host-tools](https://github.com/milkv-duo/host-tools) — предварительно собранная хост-цепочка gcc · 9★
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) — утилита настройки мультиплексирования выводов · 7★
- [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) — порт wiringX для Duo · 11★
- [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples) — примеры мультимедийного конвейера · 6★
- [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) — LVGL on framebuffer · 10★
- [duo-arduino](https://github.com/milkv-duo/duo-arduino) — официальная поддержка Arduino (архивирована, ведёт на [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)) · 20★
- [duo-arduino-examples](https://github.com/milkv-duo/duo-arduino-examples) — примеры Arduino
- [duo-tdl-examples](https://github.com/milkv-duo/duo-tdl-examples) — примеры TDL для SDK V2 · 13★
- [cvitek-tdl-sdk-sg200x](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) — примеры TDL-SDK для SG200x · 30★
- [cvitek-tdl-sdk-cv180x](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) — примеры TDL-SDK для CV180x
- [tpu-sdk-sg200x](https://github.com/milkv-duo/tpu-sdk-sg200x) — SG200x TPU SDK · 5★
- [tpu-sdk-cv180x](https://github.com/milkv-duo/tpu-sdk-cv180x) — CV180x TPU SDK
- [tpu-mlir](https://github.com/milkv-duo/tpu-mlir) — преобразование моделей TPU-MLIR · 9★
- [duo-yolo-deployment](https://github.com/milkv-duo/duo-yolo-deployment) — пример развёртывания YOLO
- [milkv-duo-linux](https://github.com/milkv-duo/milkv-duo-linux) — официальное дерево ядра · 1★
- [milkv-duo-u-boot](https://github.com/milkv-duo/milkv-duo-u-boot) — официальное дерево U-Boot · 4★
- [milkv-duo-opensbi](https://github.com/milkv-duo/milkv-duo-opensbi) — официальный порт OpenSBI · 2★
- [milkv-duo-smallcore-freertos](https://github.com/milkv-duo/milkv-duo-smallcore-freertos) — FreeRTOS на малом ядре C906 · 17★
- [duo-8051](https://github.com/milkv-duo/duo-8051) — примеры для встроенного ядра 8051 · 8★

**Официальная документация и аппаратные материалы**

- [duo-files](https://github.com/milkv-duo/duo-files) — хранилище схем, даташитов и механических чертежей · 203★
- [accessories](https://github.com/milkv-duo/accessories) — материалы по официальным аксессуарам · 14★
- [milkv.io](https://github.com/milk-v/milkv.io) — исходный код сайта и документации · 4★
- [sophgo-doc](https://github.com/sophgo/sophgo-doc) — канал публикации документации на микросхемы от upstream
- [datasheet-en](https://github.com/taspenwall/datasheet-en) — английский перевод даташита SG2002 · 5★
- [riscv-rtthread-programming-manual](https://github.com/flyingcys/riscv-rtthread-programming-manual) — сопроводительный код к книге 《RISC-V 编程指南：基于 RT-Thread 与 Milk-V Duo》 · 10★
- [MilkV-Duo-Resources](https://github.com/robtech21/MilkV-Duo-Resources) — подборка ресурсов
- [johandevlabs/milk-v-duo-s-notes](https://github.com/johandevlabs/milk-v-duo-s-notes) — заметки об экспериментах с Duo S · 5★
- [Mirrorium227/MilkvDuo_Basic](https://github.com/Mirrorium227/MilkvDuo_Basic) — диагностика неполадок и примеры для CV1800B
- [imagineeeinc/things-on-milkv-duo](https://github.com/imagineeeinc/things-on-milkv-duo) — Duo на Nim

**Загрузчики и прошивки**

- [u-boot/u-boot](https://github.com/u-boot/u-boot) — в mainline уже есть `board/sophgo/milkv_duo` · 5309★
- [sg_boot](https://github.com/platform-system-interface/sg_boot) — загрузчик для CV1800B/SG200x на Rust · 12★
- [gtxzsxxk/milkv-duo-firmware-fsbl](https://github.com/gtxzsxxk/milkv-duo-firmware-fsbl) — реализация FSBL · 6★
- [Taumille/uboot-milkv](https://github.com/Taumille/uboot-milkv) — форк сообщества, появившийся после исчезновения официального репозитория u-boot

**Дистрибутивы и системные образы**

- [armbian/build](https://github.com/armbian/build) — уже содержит платы `milkv-duos-riscv` / `milkv-duos-arm` · 5499★
- [Fishwaldo/sophgo-sg200x-debian](https://github.com/Fishwaldo/sophgo-sg200x-debian) — самая активная сборка Debian для SG200x · 219★
- [ambraglow/milkv-duo-ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) — Ubuntu для Duo · 68★
- [olivaw448/milkv-duo-s-512mb-debian](https://github.com/olivaw448/milkv-duo-s-512mb-debian) — Debian для Duo S 512MB (с WiFi/Bluetooth/USB host/камерой) · 11★
- [eznix86/milkv-duo-s-alpine-linux](https://github.com/eznix86/milkv-duo-s-alpine-linux) — Alpine для Duo S · 9★
- [hkcfs/alpine-milk-v](https://github.com/hkcfs/alpine-milk-v) — образы Alpine для Duo 256M (SG2002): сборка в Docker сразу выдаёт варианты для RISC-V (C906) и ARM64 (A53) и следует за последним релизом Alpine · 0★
- [CrocNet/duo-docker-builder](https://github.com/CrocNet/duo-docker-builder) — сборка образа Ubuntu в Docker · 9★
- [logicethos/Milk-V_Duo_Linux2SD](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — сборка с записью сразу на карту · 21★
- [RawFish69/ubuntu-milkv-duos](https://github.com/RawFish69/ubuntu-milkv-duos) — Ubuntu 22.04 для Duo S
- [draftbottle/Milkv-duo-openwrt](https://github.com/draftbottle/Milkv-duo-openwrt) — OpenWrt на базе VizOS
- [Pillar1989/VizOS](https://github.com/Pillar1989/VizOS) — проект OpenWrt / VizOS
- [georgewhewell/nixos-nanokvm](https://github.com/georgewhewell/nixos-nanokvm) — конфигурация NixOS для SG2000/SG2002
- [kinsamanka/meta-milkv](https://github.com/kinsamanka/meta-milkv) — слой Yocto / OpenEmbedded

**RTOS и bare-metal**

- [RT-Thread/rt-thread](https://github.com/RT-Thread/rt-thread) — в `bsp/cvitek` есть milkv-duo / duo256m / duos · 12318★
- [lupyuen/nuttx-sg2000](https://github.com/lupyuen/nuttx-sg2000) — NuttX на Duo S · 45★
- [kinsamanka/milkv-zephyros](https://github.com/kinsamanka/milkv-zephyros) — Zephyr на малом ядре · 35★
- [saicogn/ThreadX-to-RISC-V64](https://github.com/saicogn/ThreadX-to-RISC-V64) — порт ThreadX · 8★
- [Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK](https://github.com/Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK) — bare-metal на двух ядрах без SDK · 11★
- [zuki/xv6-milkv-duo](https://github.com/zuki/xv6-milkv-duo) — xv6 on Duo · 7★
- [jiegegena/milkv-sg2002-xv6](https://github.com/jiegegena/milkv-sg2002-xv6) — xv6 on SG2002
- [Lam920/xv6-cv1800b](https://github.com/Lam920/xv6-cv1800b) — xv6 on CV1800B
- [rota1001/milkv-baremetal-toolkit](https://github.com/rota1001/milkv-baremetal-toolkit) — генерация bare-metal образа одной командой · 8★
- [PeterForth/MILKV-FORTH](https://github.com/PeterForth/MILKV-FORTH) — Forth на Duo · 8★
- [xingrz/milkv-duo-zephyr-mailbox-example](https://github.com/xingrz/milkv-duo-zephyr-mailbox-example) — обмен через mailbox между Zephyr и Linux
- [DivByDiamond/OnyxOS](https://github.com/DivByDiamond/OnyxOS) — монолитное ядро RISC-V на Rust (около 272 KB вместе с загрузчиком на C++ и самодостаточным компилятором C); содержит драйверы платформы SG2000, среди целевых плат указан Duo S · 0★

**Инструментальные цепочки и окружение сборки**

- [aidancrowther/Milk-V-Duo-Docker-Compile](https://github.com/aidancrowther/Milk-V-Duo-Docker-Compile) — Docker-образ с предустановленной инструментальной цепочкой · 24★
- [Tosainu/docker-milkv-duo-linux](https://github.com/Tosainu/docker-milkv-duo-linux) — сборка Linux в контейнере
- [boberace/milkv_duo_dc](https://github.com/boberace/milkv_duo_dc) — VS Code Dev Container
- [kitnerboy/milkv-duo-buildroot](https://github.com/kitnerboy/milkv-duo-buildroot) — Buildroot BSP в стиле mainline

**Драйверы и периферия**

- [hexdump0815/linux-cvitek-cv18xx-kernel](https://github.com/hexdump0815/linux-cvitek-cv18xx-kernel) — дерево ядра от сообщества (источник ядра для многих образов)
- [leafpmpmp/sg200x-camera-dkms](https://github.com/leafpmpmp/sg200x-camera-dkms) — DKMS-пакет драйверов камеры SG200x из mainline (`cv1800-csi2`, `cv1800-vi`); Armbian встраивает их в своё ядро. Проверено на Duo S с Linux 7.2 на обоих ядрах: Camera Module 3 / v1 на J2, Milk-V CAM-GC2083 на J1 (только riscv64) · 0★
- [ret7020/CVI_HW_OpenCV](https://github.com/ret7020/CVI_HW_OpenCV) — порт OpenCV с ускорением на NPU · 7★
- [pavelanni/gpiod-milkvduo](https://github.com/pavelanni/gpiod-milkvduo) — примеры использования libgpiod · 3★
- [Satharus/I2C-WiringX-Milk-V](https://github.com/Satharus/I2C-WiringX-Milk-V) — работа с I²C через wiringX · 2★
- [KuLvo/milk-v_duo_oled_driver](https://github.com/KuLvo/milk-v_duo_oled_driver) — драйвер OLED 0,96 дюйма · 3★
- [queenkjuul/aic8800-milkv-duos](https://github.com/queenkjuul/aic8800-milkv-duos) — поддержка AIC8800 WiFi+BT
- [GrootLiu/milkv-duo-rtl8723du](https://github.com/GrootLiu/milkv-duo-rtl8723du) — порт WiFi RTL8723DU
- [Tactical-TV-Remote/infrared_milkv](https://github.com/Tactical-TV-Remote/infrared_milkv) — приём и передача ИК (Rust)
- [harshareddy1611/milkv-duo-s-baremetal-drivers](https://github.com/harshareddy1611/milkv-duo-s-baremetal-drivers) — bare-metal GPIO/UART для Duo S
- [wanghengZzz/Milkv-Duo-FreeRTOS-DMA](https://github.com/wanghengZzz/Milkv-Duo-FreeRTOS-DMA) — FreeRTOS DMA HAL

**Практические проекты**
- [tidesense](https://github.com/HumpbackLab/tidesense) — стерео визуально-инерционная одометрия на SG2002 (собственная плата, не Duo 256M): два глобальных затвора OV9281 плюс IMU SC7U22, SchurVINS с визуальной коррекцией 20 Гц и предсказанием 200 Гц, плюс сравнение с OpenVINS, калибровка и средства работы с датасетами; VIO работает на Cortex-A53 и загружается только с SD-карты. Аппаратная часть открыта под CC BY-NC-SA 4.0 (ссылка в README репозитория) · 142★

- [pavelanni/milkv-duo-experiments](https://github.com/pavelanni/milkv-duo-experiments) — набор экспериментов на Go · 27★
- [driver1998/DiscEmu](https://github.com/driver1998/DiscEmu) — эмулятор CD-ROM на Duo · 11★
- [0x1iii1ii/Pwn-V-Duo](https://github.com/0x1iii1ii/Pwn-V-Duo) — порт эксплойта PPPwn · 6★
- [aceraoc/MilkV-Duo_TPU](https://github.com/aceraoc/MilkV-Duo_TPU) — примеры инференса на TPU · 8★
- [xmdjy/milkv-car](https://github.com/xmdjy/milkv-car) — умная машинка на базе Duo
- [Arielfoever/milkv-duo-yolo11](https://github.com/Arielfoever/milkv-duo-yolo11) — развёртывание YOLO11
- [Basicname/SG200x_GC2083_Yolov8_11](https://github.com/Basicname/SG200x_GC2083_Yolov8_11) — развёртывание YOLOv8/11 + GC2083 в одном файле
- [chius-me/globi-v](https://github.com/chius-me/globi-v) — система компьютерного зрения для помощи слабовидящим на Duo S
- [f3jry/milkv-duo-xmrsigner](https://github.com/f3jry/milkv-duo-xmrsigner) — порт холодного кошелька Monero на Duo
- [sdwood68/MilkV_Duo_S_Camera](https://github.com/sdwood68/MilkV_Duo_S_Camera) — узел камеры с поддержкой Frigate / Home Assistant
- [ar90n/ptp-server-milkv-duos](https://github.com/ar90n/ptp-server-milkv-duos) — сервер точного времени PTP
- [avalitan/MilkV-Duo-S-NTP-UPS-Server](https://github.com/avalitan/MilkV-Duo-S-NTP-UPS-Server) — мониторинг NTP + NUT UPS
- [vojinvukcevic/boot-time-optimization-milkv](https://github.com/vojinvukcevic/boot-time-optimization-milkv) — полный разбор ускорения холодной загрузки с 14,1 s до 3,2 s
- [manio/milkv-duos-hwcodec-test](https://github.com/manio/milkv-duos-hwcodec-test) — минимальный самотест аппаратного кодека H.264 на Duo S: напрямую вызывает libsys / libvenc / libvdec из cvi_mpi, минуя VI/VPSS/VO, кодирует синтетические кадры и декодирует их обратно для сравнения PSNR (по умолчанию 1280×720, 60 кадров); измерено на образе Buildroot (ядро 5.10.4) · 0★
- [Tom-game-project/MilkV-DuoS-rust-tpu-example](https://github.com/Tom-game-project/MilkV-DuoS-rust-tpu-example) — матричные вычисления на TPU из Rust на Duo S: Makefile сам подтягивает host-tools, tpu-sdk-sg200x и tpu-mlir, собирает .cvimodel из ONNX, кросс-компилирует Rust под riscv64 musl и копирует на плату через scp · 0★
- [lukaszsobala/duos-camera](https://github.com/lukaszsobala/duos-camera) — подробный отчёт о запуске CAM-GC2083 на Duo S: 1080p при 29.7 fps на J1, драйверы уже в основной ветке Armbian (PR #10936), H.265 пока в работе · 0★
- [leafpmpmp/duos-llm](https://github.com/leafpmpmp/duos-llm) — SmolLM2-135M на Duo S: TPU работает с ядра ARM, декодирование 12.7 tok/s (префилл 41.1 tok/s); есть сборки llama.cpp для ARM и RISC-V, на C906 с ядрами XTheadVector · 0★
- [leafpmpmp/duos-detect](https://github.com/leafpmpmp/duos-detect) — детекция людей на YOLO11 на Duo S с Camera Module 3: 60 fps, 35 мс от кадра до результата, JSON API / SSE / MJPEG-превью, пакеты Debian и служба systemd · 0★

**Аппаратная часть и корпуса**

- [iyegoroff/milkv-duo-s-case](https://github.com/iyegoroff/milkv-duo-s-case) — параметрический корпус для 3D-печати для Duo S · 12★
- [pauleffect90/MilkVDuoKicad](https://github.com/pauleffect90/MilkVDuoKicad) — символы и посадочные места KiCad · 4★
- [Tosainu/milkv-duo-iob](https://github.com/Tosainu/milkv-duo-iob) — файлы проекта платы расширения IO

---

## 11. Проекты на Gitee и китайские руководства

**Gitee (19 проектов)**

- [tinylab/milkv-buildroot](https://gitee.com/tinylab/milkv-buildroot) — проект сборки Buildroot для зеркала сообщества TinyLab
- [tinylab/duo-buildroot-sdk](https://gitee.com/tinylab/duo-buildroot-sdk) — китайское зеркало официального SDK V1
- [tinylab/duo-examples](https://gitee.com/tinylab/duo-examples) — китайское зеркало официальных примеров
- [tinylab/i2c-lsm6dsr](https://gitee.com/tinylab/i2c-lsm6dsr) — пример работы с датчиком LSM6DSR по I²C
- [weilinfox/pinpong-milkv-duo-doc](https://gitee.com/weilinfox/pinpong-milkv-duo-doc) — pinpong на Duo · 3★
- [lan-ruixin/duo-buildroot-sdk](https://gitee.com/lan-ruixin/duo-buildroot-sdk) — личная ветка V1 с добавленными китайскими инструкциями по сборке
- [lan-ruixin/milkv-duo-rtl8723du](https://gitee.com/lan-ruixin/milkv-duo-rtl8723du) — поддержка WiFi/Bluetooth RTL8723DU
- [qhw136/milkv_duo_sdk](https://gitee.com/qhw136/milkv_duo_sdk) — расширенный SDK с LCD/тачскрином/WiFi/Bluetooth
- [zhidao101/Milkv_duo_Ubuntu_image](https://gitee.com/zhidao101/Milkv_duo_Ubuntu_image) — образы Ubuntu 22.04 для 256M и 512MB
- [tiberium/duosdk2yocto](https://gitee.com/tiberium/duosdk2yocto) — переделка SDK в сборку Yocto
- [tiberium/meta-milkv-duo-sdk](https://gitee.com/tiberium/meta-milkv-duo-sdk) — сопутствующий meta layer
- [fixxer2020/duo-multimedia-examples](https://gitee.com/fixxer2020/duo-multimedia-examples) — зеркало мультимедийных примеров
- [dongshan-community/DongShanPiExtboard](https://gitee.com/dongshan-community/DongShanPiExtboard) — плата расширения mini-ITX для Duo 256M
- [linux-proj/Milkv-duo_Cross_Compile_software](https://gitee.com/linux-proj/Milkv-duo_Cross_Compile_software) — предварительно собранные пакеты зависимостей для кросс-компиляции
- [atari/opencv-mobile](https://gitee.com/atari/opencv-mobile) — синхронизированное зеркало opencv-mobile (riscv64-musl, аппаратное декодирование JPG, MIPI CSI) · 5★
- [unicornx/riscv-operating-system-mooc](https://gitee.com/unicornx/riscv-operating-system-mooc) — код курса RVOS (портирован на Duo) · 541★
- [openeuler/UniProton](https://gitee.com/openeuler/UniProton) — примеры для большого и малого ядер, включая `demos/milkv-duo` · 73★ (репозиторий переехал на AtomGit)
- [k0059/duo-buildroot-sdk-v2](https://gitee.com/k0059/duo-buildroot-sdk-v2) — ветка sg200x-evb SDK V2
- [xju_kjc/duo-buildroot-sdk](https://gitee.com/xju_kjc/duo-buildroot-sdk) — полное зеркало SDK V1 (README на китайском/японском/английском)

**Китайские руководства и статьи (22 материала)**

- 博客园 [milkv-duo 启动流程分析：手动构建 fip.bin [1/2]](https://www.cnblogs.com/maomaotou-thu/p/17765721.html) · [2/2](https://www.cnblogs.com/maomaotou-thu/p/17766024.html) · [手动构建 boot.sd](https://www.cnblogs.com/maomaotou-thu/p/17767315.html) — обязательно к прочтению, если хотите разобраться в цепочке загрузки
- 博客园 [Milk-V Duo S 使用报告](https://www.cnblogs.com/BiaoZyx/p/18956632) — от распаковки до проверки периферии, включая подводные камни
- 博客园 [大作业：milkv-duo 小车设计工作日志](https://www.cnblogs.com/Cybersites/p/18859275)
- 博客园 [小核引导 RTOS —— RISC-V C906](https://www.cnblogs.com/gaoyang3513/articles/18854508)
- 博客园 [集成构建流程之根文件系统 Buildroot](https://www.cnblogs.com/gaoyang3513/p/18854502) · [网络升级固件](https://www.cnblogs.com/gaoyang3513/p/18854509) · [以太网使用与配置](https://www.cnblogs.com/gaoyang3513/p/18854518) · [Docker 开发环境搭建](https://www.cnblogs.com/gaoyang3513/p/18854511)
- 博客园 [milkv duo 256M 使用 Debian 系统](https://www.cnblogs.com/GrootStudy/p/18225934)
- 博客园 [milkV-duo 的 Linux 开发环境搭建](https://www.cnblogs.com/yzh0526/p/18098794)
- 博客园 [milk-v duo 开机引导进入 rust 程序](https://www.cnblogs.com/longxiangam/p/19640491)
- 掘金 [milkv-duo 开发环境搭建 & 烧录](https://juejin.cn/post/7269416466314821668) · [打包 SDK 时遇到的问题及解决](https://juejin.cn/post/7269417409370505235) · [小奶板点灯 & sensor bring up](https://juejin.cn/post/7269644295588659261) · [image burn](https://juejin.cn/post/7269424598260334648) · [milkv 256duo 初品](https://juejin.cn/post/7355829021311238182)
- B 站专栏 [Milk-v Duo：35 块带 TPU 1GHz 的 Linux 开发板](https://www.bilibili.com/read/cv24253633) · [Linux 与 RTOS 双核开发实践](https://www.bilibili.com/read/cv27449966) · [Duo S 部署 PicoClaw 完整教程](https://www.bilibili.com/read/cv46804507) · [Ubuntu 20.04 详细编译环境搭建指南](https://www.bilibili.com/read/cv24743710)

> **CSDN и 知乎 пока отсутствуют**: в этой сети оба сайта отвечают 521 / 403 (прямой заход из браузера тоже блокируется), поэтому проверку «страница действительно существует» они не проходят, и непроверенные ссылки не добавляются. Вопросно-ответное сообщество RT-Thread `club.rt-thread.org` также блокируется WAF. Добавим, когда появится прямой доступ.

---

## 12. Как поддерживается этот указатель

- Каждый день в 14:00 автоматически выполняется инкрементальный обход сети (официальные релизы, новые страницы документации, новые видео, новые репозитории); при изменениях готовится обновление
- Принимаются только **работающие** ссылки; при каждом обновлении выполняется полная проверка ссылок, мёртвые ссылки удаляются или заменяются новыми адресами
- От видео требуется, чтобы в нём действительно использовалась плата семейства Duo; от проекта — чтобы репозиторий действительно поддерживал эти платы, а не просто упоминал их
- Включение в список не означает одобрения. Безопасность, лицензию и состояние поддержки сторонних образов и проектов оценивайте самостоятельно
- Если нашли пропущенный ресурс — создайте issue или PR; в PR размещайте материал в существующем разделе и указывайте поддерживаемые платы (Duo / Duo 256M / Duo S)

[Вернуться к списку языков](README.md)
