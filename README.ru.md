# Справочник ресурсов Milk-V Duo, Duo 256M и Duo S

Здесь собраны официальная документация, прошивки, исходный код, аппаратные материалы, руководства и проекты сообщества для семейства Milk-V Duo. Полноту всех ресурсов в интернете гарантировать невозможно; мы приветствуем исправления и новые ссылки.

> **Перед использованием проверьте совместимость.** В оригинальном Duo установлен CV1800B и 64 МБ памяти; в Duo 256M — SG2002 и 256 МБ; в Duo S — SG2000 и 512 МБ. У этих плат различаются аппаратные средства и программные цели. В официальном обзоре оригинальный Duo отмечен как снятый с производства (EOL). Сторонние системы и образы поддерживаются сообществом и могут быть не протестированы.

## Официальные продукты и документация

- [Обзор и характеристики семейства Duo](https://milkv.io/docs/duo/overview) — сравнение плат, функции и сведения о жизненном цикле.
- Руководства по платам: [Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos).
- Начало работы: [загрузка платы](https://milkv.io/docs/duo/getting-started/boot) · [загрузка и выбор образа](https://milkv.io/docs/duo/getting-started/download) · [руководство по Buildroot SDK](https://milkv.io/docs/duo/getting-started/buildroot-sdk).
- Страницы продуктов: [Duo](https://milkv.io/duo) · [Duo 256M](https://milkv.io/duo256m) · [Duo S](https://milkv.io/duos).
- [Исходный код официальной документации](https://github.com/milk-v/milkv.io) — сюда можно отправлять исправления и переводы.

## Прошивки, SDK и инструментарий

- [Каталог официальных образов и примечания о совместимости](https://milkv.io/docs/duo/getting-started/download).
- Официальные выпуски прошивок: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk/releases) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases).
- Исходный код SDK: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [инструменты для хост-системы](https://github.com/milkv-duo/host-tools).
- Официальное руководство рекомендует V1 для Duo с 64 МБ памяти, а V2 — для Duo 256M и Duo S. Всегда проверяйте примечания к выпуску и название целевой платы.
- [Официальные примеры на C/C++ и настройка кросс-компилятора](https://github.com/milkv-duo/duo-examples): [мигание GPIO](https://github.com/milkv-duo/duo-examples/tree/main/blink), [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c), [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) и [руководство по периферии (PDF)](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf).

## Аппаратная часть, периферия и разработка приложений

- [Официальные файлы плат: схемы, спецификации и механические чертежи](https://github.com/milkv-duo/duo-files).
- Схемы плат: [Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf).
- [Техническая документация и спецификации микросхем Sophgo](https://github.com/sophgo/sophgo-doc/releases).
- Документация SoC: [предварительная спецификация CV1800B/CV1801B (английский)](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf) и [китайская версия](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf) · [предварительная спецификация SG2002 (китайский)](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [предварительная спецификация SG2000 (китайский)](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) и [справочное руководство (английский)](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf).
- Официальные проекты для разработки: [мультиплексирование выводов](https://github.com/milkv-duo/duo-pinmux) · [wiringX](https://github.com/milkv-duo/duo-wiringx) · [аксессуары](https://github.com/milkv-duo/accessories) · [демонстрация LVGL framebuffer](https://github.com/milkv-duo/duo-lvgl-fb-demo).
- Документация: [GPIO и мультиплексирование выводов](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [USB-камеры](https://milkv.io/docs/duo/camera/usb) · [мультимедийный фреймворк](https://milkv.io/docs/duo/application-development/multimedia).
- Arduino: старая [библиотека Milk-V Arduino](https://github.com/milkv-duo/duo-arduino) архивирована; в её репозитории предлагается [Sophgo Arduino](https://github.com/kubuds/sophgo-arduino). Также доступны [примеры Arduino для Duo](https://github.com/milkv-duo/duo-arduino-examples); перед использованием проверьте поддержку платы и ядра.

## ИИ, компьютерное зрение и мультимедиа

- Примеры TDL: [SDK V1 для CV180X / оригинального Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SDK V1 для SG200X / Duo 256M и Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [примеры SDK V2](https://github.com/milkv-duo/duo-tdl-examples).
- TPU и инструменты моделей: [TPU SDK для CV180X](https://github.com/milkv-duo/tpu-sdk-cv180x) · [преобразование моделей TPU-MLIR](https://github.com/milkv-duo/tpu-mlir) · [TPU SDK для SG200X](https://github.com/milkv-duo/tpu-sdk-sg200x).
- [Официальные примеры мультимедиа](https://github.com/milkv-duo/duo-multimedia-examples) · [развёртывание моделей TDL](https://github.com/milkv-duo/duo-yolo-deployment).
- В [официальном руководстве по загрузке](https://milkv.io/docs/duo/getting-started/download) также перечислены сторонние образы для разных плат. Учитывайте предупреждения, проверяйте сопровождающих и совместимую ревизию оборудования.

## Сторонние ОС и учебные материалы

Это независимые проекты сообщества, а не официальные прошивки. Совместимость и поддержка могут измениться; перед установкой изучите документацию проекта.

- Дистрибутивы Linux: [зеркало образов Fedora](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/) · [Debian для Sophgo SG200X](https://github.com/scpcom/sophgo-sg200x-debian) · [сборщик образов Ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) · [проект OpenWrt/VizOS](https://github.com/Pillar1989/VizOS).
- Системы сборки и RTOS: [слой Yocto/OpenEmbedded](https://github.com/kinsamanka/meta-milkv) · [Zephyr на вспомогательном ядре Duo](https://github.com/kinsamanka/milkv-zephyros) · [NuttX для SG2000 / Duo S](https://github.com/lupyuen/nuttx-sg2000) · [RT-Thread BSP для CVitek](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) · [порт ThreadX](https://github.com/saicogn/ThreadX-to-RISC-V64).
- [Форум сообщества Milk-V Duo](https://community.milkv.io/c/duo/5) · [форум Sophgo](https://forum.sophgo.com/) · [организация Milk-V Duo на GitHub](https://github.com/milkv-duo).

## Участие и актуальность ссылок

Если ссылка не работает, ресурс отсутствует или проект изменил список поддерживаемых плат, создайте issue или pull request. Отдавайте предпочтение документации и выпускам от разработчиков, не размещайте копии прошивок. Перед записью образа проверьте модель платы, SoC, объём памяти, тип накопителя, режим загрузки и инструкции к образу; сделайте резервную копию и соблюдайте правила безопасного питания и подключения.

[Вернуться к списку языков](README.md)
