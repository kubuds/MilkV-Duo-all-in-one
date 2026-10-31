# Índice de recursos de la familia Milk-V Duo (Duo · Duo 256M · Duo S)

Todos los recursos de la familia Milk-V Duo que hemos podido encontrar están reunidos en esta página: documentación oficial y hojas de datos, imágenes listas para descargar, SDK y cadenas de herramientas, proyectos de código abierto en GitHub y Gitee, y vídeos de Bilibili y YouTube en los que realmente se ha usado esta placa.

Esta página no copia ni replica ningún firmware ni documento: solo indica la fuente y el mantenedor. **Las imágenes y los proyectos de la comunidad no han sido probados ni respaldados por Milk-V**; antes de grabar una imagen, comprueba por tu cuenta el modelo de placa, el SoC, la memoria, el medio de almacenamiento y las notas de la versión.

> **Primero confirma qué placa tienes.** Las tres generaciones no son lo mismo: el Duo usa el CV1800B (64 MB de RAM), el Duo 256M usa el SG2002 (256 MB y un Cortex-A53 adicional) y el Duo S usa el SG2000 (512 MB, con Wi-Fi 6 / BT5 opcional y eMMC opcional). **El Duo original está marcado oficialmente como descatalogado (EOL)**; para proyectos nuevos conviene ir directamente al 256M o al Duo S.

---

## 1. Modelos y variantes

| Modelo | SoC | Memoria | Almacenamiento | Inalámbrico | Ethernet | TPU | Estado |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Duo** | CVITEK CV1800B | 64 MB | microSD o SD NAND integrada | No | 100M (PHY) | 0.5 TOPS@INT8 | Descatalogado (EOL) |
| **Duo 256M** | SG2002 | 256 MB | microSD o SD NAND integrada | No | 100M (PHY) | 1.0 TOPS@INT8 | En venta |
| **Duo S** | SG2000 | 512 MB | microSD + zócalo eMMC en placa | Wi-Fi 6 / BT5 **opcional** | 100M (RJ45, admite PoE HAT) | 0.5 TOPS@INT8 | En venta |
| **Duo Module 01** (módulo principal + placa de evaluación) | SG2000 | 512 MB | 8 GB eMMC integrada | Wi-Fi 6 / BT5.4 integrados | 2× 100M | 0.5 TOPS@INT8 | En venta |

**Las cuatro combinaciones del Duo S**: con o sin eMMC soldado × con o sin módulo Wi-Fi, cuatro SKU en total. Al comprar, fíjate bien en cuál de ellas indica la página del producto.

Las imágenes **solo se distinguen por el medio de arranque** (`-sd` / `-emmc`), no por el Wi-Fi: entre los siete archivos de la versión oficial v2.0.1 no hay ninguna imagen con la palabra wifi (véase la tabla siguiente). Por lo tanto:

- Los Duo S con y sin Wi-Fi usan la misma imagen; la función inalámbrica depende de si la placa lleva o no ese módulo
- Una placa con eMMC puede arrancar desde la tarjeta TF con la imagen `-sd` o grabar en el almacenamiento integrado con la `-emmc`
- Una placa **sin** eMMC solo puede usar la tarjeta TF

---

## 2. Documentación oficial, hojas de datos y material de hardware

**Sitio de documentación: índice página por página**

- Punto de partida: [visión general de la familia Duo y comparación de especificaciones](https://milkv.io/docs/duo/overview) (tabla completa de especificaciones de los cuatro productos y origen del aviso de EOL) · [portada del sitio de documentación](https://milkv.io/docs/duo/getting-started)
- Guías por placa: [Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos) · [Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- Encendido y grabación: [arranque del sistema](https://milkv.io/docs/duo/getting-started/boot) · [primera conexión y red por USB](https://milkv.io/docs/duo/getting-started/setup) · [tabla general de descarga de imágenes](https://milkv.io/docs/duo/getting-started/download) · [compilación con el SDK de Buildroot](https://milkv.io/docs/duo/getting-started/buildroot-sdk)
- Doble núcleo y bajo nivel: [desarrollo en el núcleo auxiliar 8051](https://milkv.io/docs/duo/getting-started/8051core) · [desarrollo de RTOS en el núcleo pequeño](https://milkv.io/docs/duo/getting-started/rtoscore) · [compatibilidad con Arduino](https://milkv.io/docs/duo/getting-started/arduino) · [desarrollo de bajo nivel](https://milkv.io/docs/duo/low-level-dev) ([MIPI DSI](https://milkv.io/docs/duo/low-level-dev/mipi-dsi))
- Desarrollo de aplicaciones: [visión general](https://milkv.io/docs/duo/application-development) · [GPIO sysfs](https://milkv.io/docs/duo/application-development/gpio-sysfs) · [multiplexación de pines](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [pinpong](https://milkv.io/docs/duo/application-development/pinpong) · [framework multimedia](https://milkv.io/docs/duo/application-development/multimedia)
- Cámaras: [cámara USB](https://milkv.io/docs/duo/camera/usb) · [sensor GC2083](https://milkv.io/docs/duo/camera/gc2083) · [ajuste de ISP (tuning)](https://milkv.io/docs/duo/camera/tuning)
- TPU y TDL: [introducción al TPU](https://milkv.io/docs/duo/application-development/tpu/tpu-introduction) · [introducción al TDL SDK](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-introduction) · YOLO: [v5](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov5) · [v8](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolov8) · [v11](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo11) · [v12](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-yolo12) · [detección de rostros](https://milkv.io/docs/duo/application-development/tdl-sdk/tdl-sdk-face-detection) · [detección de peatones](https://milkv.io/docs/duo/application-development/tdl-sdk/pedestrian-detection) · [detección de personas y mascotas](https://milkv.io/docs/duo/application-development/tdl-sdk/yolov8-person-pets-detection)
- Placas de expansión IO: [visión general de la IO Board](https://milkv.io/docs/duo/io-board) · [Duo S PoE HAT](https://milkv.io/docs/duo/io-board/duos-poe-hat) · [placa IO con Ethernet USB](https://milkv.io/docs/duo/io-board/usb-ethernet-iob)
- Recursos y avances del ecosistema recopilados por el fabricante: [tabla de recursos útiles](https://milkv.io/docs/duo/useful-resources) · [estado del soporte en el kernel principal](https://milkv.io/docs/duo/resources/mainline) · [situación del soporte upstream](https://milkv.io/docs/duo/resources/upstream-status) · [framework multimedia MMF](https://milkv.io/docs/duo/resources/mmf) · [OpenCV Mobile](https://milkv.io/docs/duo/resources/opencv-mobile) · [SPILVGL](https://milkv.io/docs/duo/resources/spilvgl) · [Visuino](https://milkv.io/docs/duo/resources/visuino) · [notas de xyzdims](https://milkv.io/docs/duo/resources/xyzdims)
- [Código fuente del sitio de documentación](https://github.com/milk-v/milkv.io) — si hay errores en la documentación o quieres añadir traducciones, envía un PR aquí

**Páginas de producto**

- [Duo (página de la familia)](https://milkv.io/duo) · [Duo S](https://milkv.io/duo-s) · [Duo Module 01](https://milkv.io/duo-module-01)
- El Duo 256M no tiene página de producto propia; sus especificaciones están en la página de la familia y en la [documentación](https://milkv.io/docs/duo/getting-started/duo256m)

**Archivos de hardware y manuales de los chips**

- [duo-files](https://github.com/milkv-duo/duo-files) — repositorio oficial de archivos de las placas: esquemáticos, hojas de datos, planos mecánicos y serigrafía
- Esquemáticos: [Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf)
- Hojas de datos: [CV1800B/CV1801B en inglés](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf) ([en chino](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf)) · [SG2002 en chino](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 en chino](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [SG2000 TRM en inglés](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf)
- [Página de publicaciones de documentación de Sophgo](https://github.com/sophgo/sophgo-doc/releases) — canal oficial de la documentación de los chips upstream

---

## 3. Imágenes oficiales y grabación

Todas las imágenes oficiales se basan en Buildroot y se dividen en dos líneas, V1 y V2. **Para el Duo de 64 MB se recomienda V1** (los ejemplos de IA de V2 no funcionan en 64 MB); para el Duo 256M y el Duo S, usa V2.

### V2 (recomendada para Duo 256M / Duo S) · [v2.0.1, 2025-05-30](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases)

| Archivo | Placa | Medio de arranque | Biblioteca C / arquitectura |
| --- | --- | --- | --- |
| `milkv-duo-musl-riscv64-sd_v2.0.1.img.zip` | Duo | Tarjeta TF | musl / riscv64 |
| `milkv-duo256m-musl-riscv64-sd_v2.0.1.img.zip` | Duo 256M | Tarjeta TF | musl / riscv64 |
| `milkv-duo256m-glibc-arm64-sd_v2.0.1.img.zip` | Duo 256M | Tarjeta TF | glibc / arm64 (vía A53) |
| `milkv-duos-musl-riscv64-sd_v2.0.1.img.zip` | Duo S | Tarjeta TF | musl / riscv64 |
| `milkv-duos-glibc-arm64-sd_v2.0.1.img.zip` | Duo S | Tarjeta TF | glibc / arm64 (vía A53) |
| `milkv-duos-musl-riscv64-emmc_v2.0.1.zip` | Duo S (requiere eMMC) | eMMC integrada | musl / riscv64 |
| `milkv-duos-glibc-arm64-emmc_v2.0.1.zip` | Duo S (requiere eMMC) | eMMC integrada | glibc / arm64 |

### V1 · [v1.1.4, 2024-11-22](https://github.com/milkv-duo/duo-buildroot-sdk/releases)

| Archivo | Placa | Medio de arranque |
| --- | --- | --- |
| `milkv-duo-sd-v1.1.4.img.zip` | Duo | Tarjeta TF |
| `milkv-duo256m-sd-v1.1.4.img.zip` | Duo 256M | Tarjeta TF |
| `milkv-duos-sd-v1.1.4.img.zip` | Duo S | Tarjeta TF |
| `milkv-duos-emmc-v1.1.4.zip` | Duo S (requiere eMMC) | eMMC integrada |
| `arduino-milkv-duo-sd-v1.1.4.img.zip` y otras 3 variantes (4 en total) | Las tres placas | Misma regla de nombres, imágenes con Arduino preinstalado |

### Puntos clave de la grabación

- Imágenes para tarjeta TF: descomprime y escribe con balenaEtcher o `dd`; inserta la tarjeta y enciende. **SSH y la tarjeta de red USB-NCM vienen activados por defecto; la contraseña de root es `milkv`**
- Imágenes para eMMC: **no** se graban como las de tarjeta TF. En el Duo S hay que mantener pulsada la tecla Recovery, conectar la placa al ordenador con un cable Type-C y grabar por USB con `usb_dl.exe` de CVITEK (Windows) o con la herramienta `CviBurn`; antes de grabar, quita siempre la tarjeta TF
- El Duo S tiene un **conmutador de arranque ARM / RISC-V**; si el firmware y el conmutador no coinciden, no arranca. Si el primer carácter del registro serie es `C`, el arranque fue desde RISC-V; si es `B`, desde ARM
- En el Duo S, el Type-C (USB-NCM) y el Type-A (USB HOST) **no pueden usarse a la vez**; se alternan mediante el enlace simbólico `/mnt/system/usb.sh`

---

## 4. Imágenes de terceros (mantenidas por la comunidad, por placa)

La página oficial de descargas incluye una [tabla de imágenes de terceros](https://milkv.io/docs/duo/getting-started/download); aquí están ordenadas por placa para poder abrirlas directamente.

### Duo (CV1800B, 64 MB)

- [Espejo de Fedora 41](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo/images/latest/) — mantenido por Fedora-V Force, que sigue el despliegue upstream
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) — scripts de compilación de imágenes; también sirven para el Duo 256M
- [Generador de imágenes Debian / Ubuntu](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — úsalo si quieres crear tus propias imágenes
- [Arch Linux](https://community.milkv.io/t/arch-linux-on-milkv-duo-milkv-duo-arch-linux/329) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1) · [imagen completa de Debian](https://community.milkv.io/t/milkv-duo-duo-debian-full-7z-519m-download/862)
- [OpenWrt / VizOS](https://github.com/Pillar1989/VizOS) · [Zephyr (núcleo auxiliar)](https://github.com/kinsamanka/milkv-zephyros) · [capa de Yocto](https://github.com/kinsamanka/meta-milkv)
- [RT-Thread cvitek BSP](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) ([guía de programación de RT-Thread en RISC-V](https://riscv-rtthread-programming-manual.readthedocs.io/zh-cn/latest/)) · [port de ThreadX](https://github.com/saicogn/ThreadX-to-RISC-V64)

### Duo 256M (SG2002)

- [Espejo de Fedora 41](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/Duo256M/images/latest/)
- [Debian (Fishwaldo / sophgo-sg200x-debian)](https://github.com/Fishwaldo/sophgo-sg200x-debian/releases/tag/v1.2.0)
- [Ubuntu 22.04](https://github.com/bassusteur/milkv-duo-ubuntu) · [Arch Linux](https://community.milkv.io/t/debian-arch-linux-on-milkv-duo-256m-milkv-duo-256m-debian-arch-linux/1110) · [Alpine Linux](https://github.com/cwt/duo-buildroot-sdk/releases/tag/poc1)

### Duo S (SG2000)

- [Espejo de Fedora 41](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/DuoS/images/latest/) — cuenta por defecto `root` / contraseña `riscv`
- [Debian (scpcom)](https://github.com/scpcom/sophgo-sg200x-debian/releases) — dos juegos de cuentas: `root`/`rv` y `debian`/`rv`
- [NuttX (lupyuen)](https://github.com/lupyuen/nuttx-sg2000/releases) — imagen lista para ejecutar NuttX en el Duo S

---

## 5. SDK, cadenas de herramientas y ejemplos

- Código fuente del SDK: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [herramientas de compilación del host](https://github.com/milkv-duo/host-tools)
- [duo-examples](https://github.com/milkv-duo/duo-examples) — ejemplos oficiales en C/C++: [parpadeo de GPIO](https://github.com/milkv-duo/duo-examples/tree/main/blink) · [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c) · [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) · [guía de uso de controladores de periféricos (PDF)](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf)
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) (multiplexación de pines) · [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) (port de wiringX) · [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) (LVGL sobre framebuffer) · [duo-accessories](https://github.com/milkv-duo/accessories) (accesorios oficiales)
- Arduino: [núcleo oficial archivado](https://github.com/milkv-duo/duo-arduino) (el repositorio ya apunta a [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)) · [ejemplos de Arduino para Duo](https://github.com/milkv-duo/duo-arduino-examples)
- Herramientas del lado del SoC: [SDK TPU para CV180X](https://github.com/milkv-duo/tpu-sdk-cv180x) · [SDK TPU para SG200X](https://github.com/milkv-duo/tpu-sdk-sg200x) · [conversión de modelos TPU-MLIR](https://github.com/milkv-duo/tpu-mlir)
- TDL (ejemplos de aprendizaje profundo): [CV180X / Duo](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SG200X / Duo 256M y Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [ejemplos TDL del SDK V2](https://github.com/milkv-duo/duo-tdl-examples) · [despliegue de YOLO](https://github.com/milkv-duo/duo-yolo-deployment)
- Multimedia: [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples)

---

## 6. Organización oficial, comunidad e interacción

- [Organización de milkv-duo en GitHub](https://github.com/milkv-duo) — aquí están el SDK oficial, los ejemplos y los archivos de hardware
- [Categoría Duo de la comunidad Milk-V](https://community.milkv.io/c/duo/5) — el lugar principal para preguntas y experiencias
- [Documentación de la placa de evaluación Duo Module 01](https://milkv.io/docs/duo/getting-started/duo-module-01)
- El antiguo `forum.sophgo.com` ya no es accesible (la conexión falló en una prueba real en octubre de 2026); el material del chip se obtiene ahora de [sophgo-doc](https://github.com/sophgo/sophgo-doc/releases)

---

## 7. Vídeos: Bilibili (48)

Se comprobó uno por uno que cada página existe (HTTP 200) y que el título o la descripción remiten realmente a la familia Duo; las reproducciones son una instantánea del 2026-10-31 y solo sirven como referencia de popularidad.

**Serie de 东东老师 (eastdong) — la más adecuada para empezar desde cero**

- 《零压力上手 RISC-V：东东老师带你玩转 milk-v duo》01. RVOS on Duo — [BV1vm421E7R6](https://www.bilibili.com/video/BV1vm421E7R6/) · 9578
- 02. RT-Thread on Duo — [BV1ym411z7Qo](https://www.bilibili.com/video/BV1ym411z7Qo/) · 3558
- 04. Camera 和 YOLOv5 图像识别 — [BV1mt421A7tL](https://www.bilibili.com/video/BV1mt421A7tL/) · 2972
- 05. TPU 使用 — [BV1Wi421Q7b4](https://www.bilibili.com/video/BV1Wi421Q7b4/) · 2171
- 06. 完结（补讲 Duo 256M 的新变化）— [BV1Fx4y1W7x9](https://www.bilibili.com/video/BV1Fx4y1W7x9/) · 2212

**苦芽科技 — la cadena completa del curso oficial del Duo S**

- 00. 认识 Milk-V Duo S — [BV1PNDoYeEpT](https://www.bilibili.com/video/BV1PNDoYeEpT/) · 2307
- 01. Windows 下安装及启动 — [BV1u3DYYGES7](https://www.bilibili.com/video/BV1u3DYYGES7/) · 376
- macOS 下安装及启动 — [BV1U5qqYUEAm](https://www.bilibili.com/video/BV1U5qqYUEAm/) · 233
- 02. SPI 演示 — [BV1vYqHYnE8G](https://www.bilibili.com/video/BV1vYqHYnE8G/) · 186

**Iniciación y análisis**

- 35 块带 TPU、1GHz 的 Linux 开发板，还玩啥树莓派（科学中国）— [BV19h4y1t7Ct](https://www.bilibili.com/video/BV19h4y1t7Ct/) · 19 000
- 镜像烧写教程：带 TPU 的 RISC-V Linux 板（斑梨电子）— [BV1uM4y1n763](https://www.bilibili.com/video/BV1uM4y1n763/) · 9098
- 能跑轻量 AI 的最便宜 RISC-V Linux 开发板？Duo 64M（捡个肥仔上战场）— [BV11w411j71u](https://www.bilibili.com/video/BV11w411j71u/) · 9365
- RISC-V 峰会现场 Duo 开箱（半导体都市隶人 Ayla）— [BV1oh4y1K724](https://www.bilibili.com/video/BV1oh4y1K724/) · 8415
- 野生的开发板性能再强又有何用，软件适配稀烂：Duo 256M 尝试 Arduino 彻底失败（沈洁 Eacc）— [BV1sZZHYdEPP](https://www.bilibili.com/video/BV1sZZHYdEPP/) · 8026 ← **análisis negativo, merece la pena verlo**
- 35 元的 milkv-duo Linux 单片机还要啥自行车（开源社区的二掌柜）— [BV1tM4y1Y7kh](https://www.bilibili.com/video/BV1tM4y1Y7kh/) · 2792
- 学习 RISC-V 能跑 Debian & Linux 的最便宜开发板之一（蘭雅 sRGB）— [BV1XQ4y1E7Tj](https://www.bilibili.com/video/BV1XQ4y1E7Tj/) · 3054
- 好玩！RISC-V duo256M 开发板测玩（蘭雅 sRGB）— [BV1Zw411V7bK](https://www.bilibili.com/video/BV1Zw411V7bK/) · 2257
- 麻雀虽小五脏俱全：超高性价比开发板 Milk-V Duo S（qinyunti）— [BV1hyKmzJEw5](https://www.bilibili.com/video/BV1hyKmzJEw5/) · 664

**Preparación del entorno y grabación**

- Linux 下开发环境搭建（future 待续）— [BV1B8411m7jR](https://www.bilibili.com/video/BV1B8411m7jR/) · 3192
- 烧写 Linux 系统 + USB 虚拟 RNDIS 网卡登录（蘭雅 sRGB）— [BV1G14y1k7V4](https://www.bilibili.com/video/BV1G14y1k7V4/) · 1062
- Duo-debian 初体验（蘭雅 sRGB）— [BV11c411o76T](https://www.bilibili.com/video/BV11c411o76T/) · 3416
- Duo 简介和开发环境搭建（谁说现在是冬天呢）— [BV1PF411S7To](https://www.bilibili.com/video/BV1PF411S7To/) · 1959
- Buildroot SDK 简介和编译镜像的方法（谁说现在是冬天呢）— [BV1xc411s7qk](https://www.bilibili.com/video/BV1xc411s7qk/) · 462
- 安装 Hyper-V & 配置 Docker 开发环境（_1dentity）— [BV1nC4y117WS](https://www.bilibili.com/video/BV1nC4y117WS/) · 1826

**Periféricos, pantalla y doble núcleo**

- LVGL 库实战教程 — 刘文涛（群芯闪耀），lazyparser 频道 — [BV1Mp421m7qJ](https://www.bilibili.com/video/BV1Mp421m7qJ/) · 966
- 通过 SPI 驱动 ST7789V 跑 LVGL（谁说现在是冬天呢）— [BV1gLeueWEWr](https://www.bilibili.com/video/BV1gLeueWEWr/) · 2239
- Duo 256M 基于 TinyDRM 驱动 ST7796s 4.0 寸屏并移植 LVGL 8.3（二掌柜）— [BV1Tv421k71W](https://www.bilibili.com/video/BV1Tv421k71W/) · 1230
- USB & Ethernet IO-Board 简介和使用方法（谁说现在是冬天呢）— [BV1Ga4y1Z7oM](https://www.bilibili.com/video/BV1Ga4y1Z7oM/) · 1096
- 通过大核控制小核点亮 LED（谁说现在是冬天呢）— [BV1nH4y1y7CM](https://www.bilibili.com/video/BV1nH4y1y7CM/) · 1057
- 用 Duo 驱动 DF9GMS 微型舵机（谁说现在是冬天呢）— [BV1Dj411E7yD](https://www.bilibili.com/video/BV1Dj411E7yD/) · 571
- Duo S 硬件解码 MP4 并在 LCD 上播放（一只御坂美琴）— [BV1ktvseWEhr](https://www.bilibili.com/video/BV1ktvseWEhr/) · 519

**Portes de sistemas**

- 在 Duo 上运行 ThreadX（谁说现在是冬天呢）— [BV1yi421C7SK](https://www.bilibili.com/video/BV1yi421C7SK/) · 419
- 在小核上运行 Zephyr OS（谁说现在是冬天呢）— [BV1uK421Y7x9](https://www.bilibili.com/video/BV1uK421Y7x9/) · 435
- 在 Duo 256M 上运行 Arch Linux（谁说现在是冬天呢）— [BV1j8yyYTEp2](https://www.bilibili.com/video/BV1j8yyYTEp2/) · 1274
- 在 Duo S 上启动 NuttX（悲伤的黑山羊）— [BV1RMUeYjELe](https://www.bilibili.com/video/BV1RMUeYjELe/) · 75
- 罗君：Duo 的 UniProton 适配（PLCT 内部报告）（lazyparser）— [BV1RD421G773](https://www.bilibili.com/video/BV1RD421G773/) · 903
- Duo S 启动！（谁说现在是冬天呢）— [BV1Bm421N72y](https://www.bilibili.com/video/BV1Bm421N72y/) · 564
- 使用 Wi-Fi 连接 Duo S（谁说现在是冬天呢）— [BV11r421T7Sk](https://www.bilibili.com/video/BV11r421T7Sk/) · 318
- 在 Duo S 上部署 Caddy 服务器（谁说现在是冬天呢）— [BV1poBzYQEoC](https://www.bilibili.com/video/BV1poBzYQEoC/) · 214
- Duo 256M 部署相册文件管理器和博客笔记（蘭雅 sRGB）— [BV1cC4y1e7uk](https://www.bilibili.com/video/BV1cC4y1e7uk/) · 1455

**IA / visión**

- Duo 256M 锁头测试：官方脚本跑人脸检测并拉流到电脑（Judehahh）— [BV1w4421A7A2](https://www.bilibili.com/video/BV1w4421A7A2/) · 36 000
- 基于 Duo 和 YOLOv5 的目标检测（谁说现在是冬天呢）— [BV1iG41197qa](https://www.bilibili.com/video/BV1iG41197qa/) · 1211
- 基于 TDL SDK 实现 YOLOv5 目标检测（谁说现在是冬天呢）— [BV1Vw4m1U71C](https://www.bilibili.com/video/BV1Vw4m1U71C/) · 446
- YOLOv8 目标检测（谁说现在是冬天呢）— [BV1AWqUYGEaS](https://www.bilibili.com/video/BV1AWqUYGEaS/) · 269
- 测试通过 VLC 显示 CAM-GC2083 摄像头画面（谁说现在是冬天呢）— [BV188411v7tc](https://www.bilibili.com/video/BV188411v7tc/) · 1159
- Duo S 运行故事机 baby llama2（谁说现在是冬天呢）— [BV1dn4y197UW](https://www.bilibili.com/video/BV1dn4y197UW/) · 621
- Duo S 上用 TDL SDK 部署人脸检测（谁说现在是冬天呢）— [BV1AM4m1m7fe](https://www.bilibili.com/video/BV1AM4m1m7fe/) · 522
- YOLO 实战：车牌识别效果展示（谁说现在是冬天呢）— [BV1uYAHerEbL](https://www.bilibili.com/video/BV1uYAHerEbL/) · 1272

---

## 8. Vídeos: YouTube (37)

Sitio extranjero: hace falta un proxy para abrirlo; también se comprobó uno por uno que la página existe y que el contenido trata realmente del Duo.

**Análisis y primeros pasos**

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

**Iniciación, grabación y red**

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

**Periféricos e IA**

- Anton Maltsev — Is it good for computer vision? How to start a neural network on it — [dkIVDOd_Fa4](https://www.youtube.com/watch?v=dkIVDOd_Fa4) · Duo
- Mark Birss — Milk-V Duo USB input ST7789 240×240 SPI display — [Swo-zJ6brQI](https://www.youtube.com/watch?v=Swo-zJ6brQI) · Duo
- Sonny Cruz — I²C demo, source in the description — [85uglOz48Pg](https://www.youtube.com/watch?v=85uglOz48Pg) · Duo
- Sonny Cruz — RC servo demo using PWM — [1u2LZJWPtNU](https://www.youtube.com/watch?v=1u2LZJWPtNU) · Duo
- Leigh — Duo + CAM-GC2083: fix RTSP streaming to VLC — [PjiUDsoWCvo](https://www.youtube.com/watch?v=PjiUDsoWCvo) · Duo
- Muhammad Yunus — YOLOX inference on Duo S using TDL SDK + VPSS — [wzUTGK4TuqA](https://www.youtube.com/watch?v=wzUTGK4TuqA) · Duo S

**Portes de sistemas y proyectos completos**

- Muhammad Yunus — RT-Thread on Duo S: the best RTOS for cheap RISC-V? — [WjWM5YoAq-c](https://www.youtube.com/watch?v=WjWM5YoAq-c) · Duo S
- RISC-V Developers — S1E2 Enjoy RISC-V with Milk-V Duo: RT-Thread — [B7EXWE6l9xE](https://www.youtube.com/watch?v=B7EXWE6l9xE) · Duo
- Chris McDonough — NixOS 71: NixOS on RISC-V (Milk-V Duo / Duo 256M) — [-ydXjEWUlGE](https://www.youtube.com/watch?v=-ydXjEWUlGE) · familia Duo
- admin ka — Running Ubuntu glibc 24.04.4 on the Duo 256M — [0Dqbdtjt8Ro](https://www.youtube.com/watch?v=0Dqbdtjt8Ro) · Duo 256M
- 福田重夫 — Running Linux on the Duo 256M (RISC-V + ARM) — [Ga3HX-d8GHQ](https://www.youtube.com/watch?v=Ga3HX-d8GHQ) · Duo 256M
- Nch-Lab — Milk-V Duo 256M を買ったので Linux を動かしてみる — [tcAqYCwbqeU](https://www.youtube.com/watch?v=tcAqYCwbqeU) · Duo 256M
- Mark Birss — Duo 256 CyberDeck LoRa communicator (TLMVC) — [9qOJ3fKwfC0](https://www.youtube.com/watch?v=9qOJ3fKwfC0) · Duo 256M

---

## 9. Proyectos de código abierto en GitHub

Clasificados por uso. El número de estrellas y la fecha del último commit son una instantánea del 2026-10-31 y cambian con el tiempo; los marcados como «oficiales» son repositorios de la organización milkv-duo.

**SDK, firmware y herramientas oficiales**

- [duo-buildroot-sdk](https://github.com/milkv-duo/duo-buildroot-sdk) — SDK oficial de Buildroot V1 (Duo/CV1800B) · 495★
- [duo-buildroot-sdk-v2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) — SDK oficial V2 (Duo 256M / Duo S, SG200x) · 154★
- [duo-examples](https://github.com/milkv-duo/duo-examples) — ejemplos oficiales de periféricos en C/C++ · 159★
- [duo-sdk](https://github.com/milkv-duo/duo-sdk) — SDK de compilación cruzada para el host (duo-app-sdk) · 5★
- [host-tools](https://github.com/milkv-duo/host-tools) — cadena de herramientas gcc del host precompilada · 9★
- [duo-pinmux](https://github.com/milkv-duo/duo-pinmux) — herramienta de configuración de la multiplexación de pines · 7★
- [duo-wiringx](https://github.com/milkv-duo/duo-wiringx) — port de wiringX para el Duo · 11★
- [duo-multimedia-examples](https://github.com/milkv-duo/duo-multimedia-examples) — ejemplos de la cadena multimedia · 6★
- [duo-lvgl-fb-demo](https://github.com/milkv-duo/duo-lvgl-fb-demo) — LVGL sobre framebuffer · 10★
- [duo-arduino](https://github.com/milkv-duo/duo-arduino) — compatibilidad oficial con Arduino (archivado, apunta a [sophgo-arduino](https://github.com/kubuds/sophgo-arduino)) · 20★
- [duo-arduino-examples](https://github.com/milkv-duo/duo-arduino-examples) — ejemplos de Arduino
- [duo-tdl-examples](https://github.com/milkv-duo/duo-tdl-examples) — ejemplos TDL del SDK V2 · 13★
- [cvitek-tdl-sdk-sg200x](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) — ejemplos del TDL-SDK para SG200x · 30★
- [cvitek-tdl-sdk-cv180x](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) — ejemplos del TDL-SDK para CV180x
- [tpu-sdk-sg200x](https://github.com/milkv-duo/tpu-sdk-sg200x) — SDK TPU para SG200x · 5★
- [tpu-sdk-cv180x](https://github.com/milkv-duo/tpu-sdk-cv180x) — SDK TPU para CV180x
- [tpu-mlir](https://github.com/milkv-duo/tpu-mlir) — conversión de modelos TPU-MLIR · 9★
- [duo-yolo-deployment](https://github.com/milkv-duo/duo-yolo-deployment) — ejemplos de despliegue de YOLO
- [milkv-duo-linux](https://github.com/milkv-duo/milkv-duo-linux) — árbol del kernel oficial · 1★
- [milkv-duo-u-boot](https://github.com/milkv-duo/milkv-duo-u-boot) — árbol de U-Boot oficial · 4★
- [milkv-duo-opensbi](https://github.com/milkv-duo/milkv-duo-opensbi) — port oficial de OpenSBI · 2★
- [milkv-duo-smallcore-freertos](https://github.com/milkv-duo/milkv-duo-smallcore-freertos) — FreeRTOS en el núcleo pequeño C906 · 17★
- [duo-8051](https://github.com/milkv-duo/duo-8051) — ejemplos para el núcleo 8051 integrado · 8★

**Documentación oficial y material de hardware**

- [duo-files](https://github.com/milkv-duo/duo-files) — repositorio general de esquemáticos, hojas de datos y planos mecánicos · 203★
- [accessories](https://github.com/milkv-duo/accessories) — documentación de accesorios oficiales · 14★
- [milkv.io](https://github.com/milk-v/milkv.io) — código fuente del sitio web y de la documentación · 4★
- [sophgo-doc](https://github.com/sophgo/sophgo-doc) — canal de publicación de la documentación del chip upstream
- [datasheet-en](https://github.com/taspenwall/datasheet-en) — traducción al inglés de la hoja de datos del SG2002 · 5★
- [riscv-rtthread-programming-manual](https://github.com/flyingcys/riscv-rtthread-programming-manual) — código de acompañamiento de «RISC-V 编程指南：基于 RT-Thread 与 Milk-V Duo» · 10★
- [MilkV-Duo-Resources](https://github.com/robtech21/MilkV-Duo-Resources) — recopilación de recursos
- [johandevlabs/milk-v-duo-s-notes](https://github.com/johandevlabs/milk-v-duo-s-notes) — notas de experimentos con el Duo S · 5★
- [Mirrorium227/MilkvDuo_Basic](https://github.com/Mirrorium227/MilkvDuo_Basic) — resolución de problemas y ejemplos para el CV1800B
- [imagineeeinc/things-on-milkv-duo](https://github.com/imagineeeinc/things-on-milkv-duo) — usar Nim en el Duo

**Arranque y firmware**

- [u-boot/u-boot](https://github.com/u-boot/u-boot) — la línea principal ya incluye `board/sophgo/milkv_duo` · 5309★
- [sg_boot](https://github.com/platform-system-interface/sg_boot) — cargador de arranque para CV1800B/SG200x escrito en Rust · 12★
- [gtxzsxxk/milkv-duo-firmware-fsbl](https://github.com/gtxzsxxk/milkv-duo-firmware-fsbl) — implementación de FSBL · 6★
- [Taumille/uboot-milkv](https://github.com/Taumille/uboot-milkv) — fork comunitario del repositorio oficial de u-boot desaparecido

**Distribuciones e imágenes de sistema**

- [armbian/build](https://github.com/armbian/build) — ya incluye las placas `milkv-duos-riscv` / `milkv-duos-arm` · 5499★
- [Fishwaldo/sophgo-sg200x-debian](https://github.com/Fishwaldo/sophgo-sg200x-debian) — la compilación de Debian para SG200x más activa · 219★
- [ambraglow/milkv-duo-ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) — Ubuntu para el Duo · 68★
- [olivaw448/milkv-duo-s-512mb-debian](https://github.com/olivaw448/milkv-duo-s-512mb-debian) — Debian para Duo S 512MB (con WiFi/Bluetooth/USB host/cámara) · 11★
- [eznix86/milkv-duo-s-alpine-linux](https://github.com/eznix86/milkv-duo-s-alpine-linux) — Alpine para el Duo S · 9★
- [CrocNet/duo-docker-builder](https://github.com/CrocNet/duo-docker-builder) — compilación de imágenes Ubuntu con Docker · 9★
- [logicethos/Milk-V_Duo_Linux2SD](https://github.com/logicethos/Milk-V_Duo_Linux2SD) — compila y escribe directamente en la tarjeta · 21★
- [RawFish69/ubuntu-milkv-duos](https://github.com/RawFish69/ubuntu-milkv-duos) — Ubuntu 22.04 para el Duo S
- [draftbottle/Milkv-duo-openwrt](https://github.com/draftbottle/Milkv-duo-openwrt) — OpenWrt basado en VizOS
- [Pillar1989/VizOS](https://github.com/Pillar1989/VizOS) — proyecto OpenWrt / VizOS
- [georgewhewell/nixos-nanokvm](https://github.com/georgewhewell/nixos-nanokvm) — configuración de NixOS para SG2000/SG2002
- [kinsamanka/meta-milkv](https://github.com/kinsamanka/meta-milkv) — capa de Yocto / OpenEmbedded

**RTOS y bare metal**

- [RT-Thread/rt-thread](https://github.com/RT-Thread/rt-thread) — `bsp/cvitek` incluye milkv-duo / duo256m / duos · 12318★
- [lupyuen/nuttx-sg2000](https://github.com/lupyuen/nuttx-sg2000) — NuttX en el Duo S · 45★
- [kinsamanka/milkv-zephyros](https://github.com/kinsamanka/milkv-zephyros) — Zephyr en el núcleo pequeño · 35★
- [saicogn/ThreadX-to-RISC-V64](https://github.com/saicogn/ThreadX-to-RISC-V64) — port de ThreadX · 8★
- [Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK](https://github.com/Chalandi/Baremetal_Milk-V_Duo_Dual_RV64_Cores_NoSDK) — bare metal en ambos núcleos sin SDK · 11★
- [zuki/xv6-milkv-duo](https://github.com/zuki/xv6-milkv-duo) — xv6 on Duo · 7★
- [jiegegena/milkv-sg2002-xv6](https://github.com/jiegegena/milkv-sg2002-xv6) — xv6 on SG2002
- [Lam920/xv6-cv1800b](https://github.com/Lam920/xv6-cv1800b) — xv6 on CV1800B
- [rota1001/milkv-baremetal-toolkit](https://github.com/rota1001/milkv-baremetal-toolkit) — genera imágenes bare metal con un solo comando · 8★
- [PeterForth/MILKV-FORTH](https://github.com/PeterForth/MILKV-FORTH) — Forth en el Duo · 8★
- [xingrz/milkv-duo-zephyr-mailbox-example](https://github.com/xingrz/milkv-duo-zephyr-mailbox-example) — comunicación por mailbox entre Zephyr y Linux

**Cadenas de herramientas y entornos de compilación**

- [aidancrowther/Milk-V-Duo-Docker-Compile](https://github.com/aidancrowther/Milk-V-Duo-Docker-Compile) — imagen Docker con la cadena de herramientas preinstalada · 24★
- [Tosainu/docker-milkv-duo-linux](https://github.com/Tosainu/docker-milkv-duo-linux) — compilación de Linux en contenedor
- [boberace/milkv_duo_dc](https://github.com/boberace/milkv_duo_dc) — Dev Container de VS Code
- [kitnerboy/milkv-duo-buildroot](https://github.com/kitnerboy/milkv-duo-buildroot) — BSP de Buildroot al estilo de la línea principal

**Controladores y periféricos**

- [hexdump0815/linux-cvitek-cv18xx-kernel](https://github.com/hexdump0815/linux-cvitek-cv18xx-kernel) — árbol del kernel de la comunidad (origen del kernel de varias imágenes)
- [ret7020/CVI_HW_OpenCV](https://github.com/ret7020/CVI_HW_OpenCV) — port de OpenCV acelerado con la NPU · 7★
- [pavelanni/gpiod-milkvduo](https://github.com/pavelanni/gpiod-milkvduo) — uso de libgpiod · 3★
- [Satharus/I2C-WiringX-Milk-V](https://github.com/Satharus/I2C-WiringX-Milk-V) — manejo de I²C con wiringX · 2★
- [KuLvo/milk-v_duo_oled_driver](https://github.com/KuLvo/milk-v_duo_oled_driver) — controlador para OLED de 0,96 pulgadas · 3★
- [queenkjuul/aic8800-milkv-duos](https://github.com/queenkjuul/aic8800-milkv-duos) — adaptación del AIC8800 WiFi+BT
- [GrootLiu/milkv-duo-rtl8723du](https://github.com/GrootLiu/milkv-duo-rtl8723du) — port del RTL8723DU WiFi
- [Tactical-TV-Remote/infrared_milkv](https://github.com/Tactical-TV-Remote/infrared_milkv) — transmisor/receptor de infrarrojos (Rust)
- [harshareddy1611/milkv-duo-s-baremetal-drivers](https://github.com/harshareddy1611/milkv-duo-s-baremetal-drivers) — GPIO/UART bare metal en el Duo S
- [wanghengZzz/Milkv-Duo-FreeRTOS-DMA](https://github.com/wanghengZzz/Milkv-Duo-FreeRTOS-DMA) — HAL de DMA para FreeRTOS

**Proyectos prácticos**

- [pavelanni/milkv-duo-experiments](https://github.com/pavelanni/milkv-duo-experiments) — colección de experimentos escritos en Go · 27★
- [driver1998/DiscEmu](https://github.com/driver1998/DiscEmu) — emulador de CD-ROM con el Duo · 11★
- [0x1iii1ii/Pwn-V-Duo](https://github.com/0x1iii1ii/Pwn-V-Duo) — port del exploit PPPwn · 6★
- [aceraoc/MilkV-Duo_TPU](https://github.com/aceraoc/MilkV-Duo_TPU) — ejemplo de inferencia en la TPU · 8★
- [xmdjy/milkv-car](https://github.com/xmdjy/milkv-car) — coche inteligente basado en el Duo
- [Arielfoever/milkv-duo-yolo11](https://github.com/Arielfoever/milkv-duo-yolo11) — despliegue de YOLO11
- [Basicname/SG200x_GC2083_Yolov8_11](https://github.com/Basicname/SG200x_GC2083_Yolov8_11) — despliegue en un solo archivo de YOLOv8/11 + GC2083
- [chius-me/globi-v](https://github.com/chius-me/globi-v) — sistema de visión asistiva para personas con discapacidad visual en el Duo S
- [f3jry/milkv-duo-xmrsigner](https://github.com/f3jry/milkv-duo-xmrsigner) — monedero frío de Monero portado al Duo
- [sdwood68/MilkV_Duo_S_Camera](https://github.com/sdwood68/MilkV_Duo_S_Camera) — nodo de cámara compatible con Frigate / Home Assistant
- [ar90n/ptp-server-milkv-duos](https://github.com/ar90n/ptp-server-milkv-duos) — servidor de reloj maestro PTP
- [avalitan/MilkV-Duo-S-NTP-UPS-Server](https://github.com/avalitan/MilkV-Duo-S-NTP-UPS-Server) — monitorización de NTP + UPS con NUT
- [vojinvukcevic/boot-time-optimization-milkv](https://github.com/vojinvukcevic/boot-time-optimization-milkv) — registro completo del arranque en frío de 14.1 s → 3.2 s

**Hardware y carcasas**

- [iyegoroff/milkv-duo-s-case](https://github.com/iyegoroff/milkv-duo-s-case) — carcasa imprimible en 3D paramétrica para el Duo S · 12★
- [pauleffect90/MilkVDuoKicad](https://github.com/pauleffect90/MilkVDuoKicad) — símbolos y footprints de KiCad · 4★
- [Tosainu/milkv-duo-iob](https://github.com/Tosainu/milkv-duo-iob) — archivos de diseño de la placa de expansión IO

---

## 10. Proyectos en Gitee y tutoriales en chino

**Gitee (19)**

- [tinylab/milkv-buildroot](https://gitee.com/tinylab/milkv-buildroot) — proyecto de compilación con Buildroot del espejo de la comunidad 泰晓
- [tinylab/duo-buildroot-sdk](https://gitee.com/tinylab/duo-buildroot-sdk) — espejo nacional del SDK V1 oficial
- [tinylab/duo-examples](https://gitee.com/tinylab/duo-examples) — espejo nacional de los ejemplos oficiales
- [tinylab/i2c-lsm6dsr](https://gitee.com/tinylab/i2c-lsm6dsr) — ejemplo del sensor I²C LSM6DSR
- [weilinfox/pinpong-milkv-duo-doc](https://gitee.com/weilinfox/pinpong-milkv-duo-doc) — ejecutar pinpong en el Duo · 3★
- [lan-ruixin/duo-buildroot-sdk](https://gitee.com/lan-ruixin/duo-buildroot-sdk) — rama V1 mantenida por un particular, con instrucciones de compilación en chino añadidas
- [lan-ruixin/milkv-duo-rtl8723du](https://gitee.com/lan-ruixin/milkv-duo-rtl8723du) — adaptación del RTL8723DU WiFi/Bluetooth
- [qhw136/milkv_duo_sdk](https://gitee.com/qhw136/milkv_duo_sdk) — SDK mejorado con LCD/táctil/WiFi/Bluetooth
- [zhidao101/Milkv_duo_Ubuntu_image](https://gitee.com/zhidao101/Milkv_duo_Ubuntu_image) — imágenes Ubuntu 22.04 para 256M y 512MB
- [tiberium/duosdk2yocto](https://gitee.com/tiberium/duosdk2yocto) — convierte el SDK en una compilación Yocto
- [tiberium/meta-milkv-duo-sdk](https://gitee.com/tiberium/meta-milkv-duo-sdk) — capa meta correspondiente
- [fixxer2020/duo-multimedia-examples](https://gitee.com/fixxer2020/duo-multimedia-examples) — espejo de los ejemplos multimedia
- [dongshan-community/DongShanPiExtboard](https://gitee.com/dongshan-community/DongShanPiExtboard) — placa de expansión mini-ITX para el Duo 256M
- [linux-proj/Milkv-duo_Cross_Compile_software](https://gitee.com/linux-proj/Milkv-duo_Cross_Compile_software) — paquetes de dependencias de compilación cruzada precompilados
- [atari/opencv-mobile](https://gitee.com/atari/opencv-mobile) — espejo sincronizado de opencv-mobile (riscv64-musl, decodificación JPG por hardware, MIPI CSI) · 5★
- [unicornx/riscv-operating-system-mooc](https://gitee.com/unicornx/riscv-operating-system-mooc) — código del curso RVOS (ya portado al Duo) · 541★
- [openeuler/UniProton](https://gitee.com/openeuler/UniProton) — incluye ejemplos de doble núcleo en `demos/milkv-duo` · 73★ (el repositorio se ha trasladado a AtomGit)
- [k0059/duo-buildroot-sdk-v2](https://gitee.com/k0059/duo-buildroot-sdk-v2) — rama sg200x-evb del SDK V2
- [xju_kjc/duo-buildroot-sdk](https://gitee.com/xju_kjc/duo-buildroot-sdk) — espejo completo del SDK V1 (README en chino/japonés/inglés)

**Tutoriales y artículos en chino (22)**

- 博客园 [Análisis del proceso de arranque de milkv-duo: compilar fip.bin a mano [1/2]](https://www.cnblogs.com/maomaotou-thu/p/17765721.html) · [2/2](https://www.cnblogs.com/maomaotou-thu/p/17766024.html) · [compilar boot.sd a mano](https://www.cnblogs.com/maomaotou-thu/p/17767315.html) — lectura imprescindible para entender la cadena de arranque
- 博客园 [Informe de uso del Milk-V Duo S](https://www.cnblogs.com/BiaoZyx/p/18956632) — del unboxing a las pruebas de periféricos, con los problemas encontrados
- 博客园 [Trabajo final: diario de diseño del coche con milkv-duo](https://www.cnblogs.com/Cybersites/p/18859275)
- 博客园 [Arrancar un RTOS en el núcleo pequeño — RISC-V C906](https://www.cnblogs.com/gaoyang3513/articles/18854508)
- 博客园 [El sistema de archivos raíz Buildroot en el proceso de compilación integrado](https://www.cnblogs.com/gaoyang3513/p/18854502) · [actualización de firmware por red](https://www.cnblogs.com/gaoyang3513/p/18854509) · [uso y configuración de Ethernet](https://www.cnblogs.com/gaoyang3513/p/18854518) · [preparación del entorno de desarrollo con Docker](https://www.cnblogs.com/gaoyang3513/p/18854511)
- 博客园 [Uso de Debian en el milkv duo 256M](https://www.cnblogs.com/GrootStudy/p/18225934)
- 博客园 [Preparación del entorno de desarrollo Linux para el milkV-duo](https://www.cnblogs.com/yzh0526/p/18098794)
- 博客园 [Arrancar directamente un programa en Rust en el milk-v duo](https://www.cnblogs.com/longxiangam/p/19640491)
- 掘金 [Preparación del entorno y grabación del milkv-duo](https://juejin.cn/post/7269416466314821668) · [Problemas al empaquetar el SDK y cómo resolverlos](https://juejin.cn/post/7269417409370505235) · [Encender un LED y poner en marcha el sensor en la placa 小奶板](https://juejin.cn/post/7269644295588659261) · [image burn](https://juejin.cn/post/7269424598260334648) · [Primeras impresiones del milkv 256duo](https://juejin.cn/post/7355829021311238182)
- Columna de Bilibili [Milk-v Duo: una placa de desarrollo Linux de 35 yuanes con TPU a 1 GHz](https://www.bilibili.com/read/cv24253633) · [Desarrollo de doble núcleo con Linux y RTOS en la práctica](https://www.bilibili.com/read/cv27449966) · [Tutorial completo para desplegar PicoClaw en el Duo S](https://www.bilibili.com/read/cv46804507) · [Guía detallada para preparar el entorno de compilación en Ubuntu 20.04](https://www.bilibili.com/read/cv24743710)

> **CSDN y Zhihu están pendientes**: desde la red de este equipo ambos sitios devuelven 521 / 403 (el acceso directo desde el navegador también queda bloqueado), así que no superan la comprobación de «la página existe realmente» y no se incluyen enlaces sin verificar. La comunidad de preguntas de RT-Thread, `club.rt-thread.org`, también está bloqueada por un WAF. Se añadirán cuando sea posible conectarse directamente.

---

## 11. Cómo se mantiene este índice

- Cada día a las 14:00 se ejecuta automáticamente un escaneo incremental de toda la web (releases oficiales, páginas nuevas del sitio de documentación, vídeos nuevos, repositorios nuevos) y, si hay cambios, se envía una actualización
- Solo se recogen enlaces **que se pueden abrir**; en cada actualización se ejecuta una comprobación completa de enlaces y los enlaces muertos se retiran o se sustituyen por la dirección nueva
- En los vídeos se exige que realmente se use la familia Duo; en los proyectos, que el repositorio dé soporte real a estas placas (no solo una mención de pasada)
- Aparecer en la lista no implica respaldo. La seguridad, la licencia y el estado de mantenimiento de las imágenes y proyectos de terceros debes juzgarlos tú mismo
- Si encuentras un recurso que falta, puedes abrir un issue o enviar un PR; al enviar un PR, colócalo en la sección correspondiente e indica las placas compatibles (Duo / Duo 256M / Duo S)

[Volver al índice de idiomas](README.md)
