# Guía de recursos de Milk-V Duo, Duo 256M y Duo S

Este directorio reúne documentación oficial, firmware, código fuente, materiales de hardware, tutoriales y proyectos de la comunidad para la familia Milk-V Duo. No es posible garantizar que incluya todos los recursos disponibles en Internet; se agradecen las correcciones y los enlaces nuevos.

> **Comprueba la compatibilidad antes de usar los recursos.** El Duo original usa el CV1800B y tiene 64 MB de RAM; el Duo 256M usa el SG2002 y tiene 256 MB; el Duo S usa el SG2000 y tiene 512 MB. El hardware y los objetivos de software varían entre placas. La descripción oficial indica que el Duo original está descatalogado (EOL). Los sistemas e imágenes de terceros son mantenidos por la comunidad y quizá no estén probados.

## Productos y documentación oficiales

- [Descripción general y especificaciones de la familia Duo](https://milkv.io/docs/duo/overview) — comparación de placas, funciones y ciclo de vida.
- Guías de las placas: [Duo](https://milkv.io/docs/duo/getting-started/duo) · [Duo 256M](https://milkv.io/docs/duo/getting-started/duo256m) · [Duo S](https://milkv.io/docs/duo/getting-started/duos).
- Primeros pasos: [arranque](https://milkv.io/docs/duo/getting-started/boot) · [descarga y selección de imágenes](https://milkv.io/docs/duo/getting-started/download) · [guía del SDK de Buildroot](https://milkv.io/docs/duo/getting-started/buildroot-sdk).
- Páginas de producto: [Duo](https://milkv.io/duo) · [Duo 256M](https://milkv.io/duo256m) · [Duo S](https://milkv.io/duos).
- [Código fuente de la documentación oficial](https://github.com/milk-v/milkv.io) — contribuye con correcciones o traducciones.

## Firmware, SDK y herramientas

- [Catálogo de imágenes oficiales y notas de compatibilidad](https://milkv.io/docs/duo/getting-started/download).
- Versiones oficiales de firmware: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk/releases) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2/releases).
- Código fuente del SDK: [Buildroot SDK V1](https://github.com/milkv-duo/duo-buildroot-sdk) · [Buildroot SDK V2](https://github.com/milkv-duo/duo-buildroot-sdk-v2) · [herramientas del host](https://github.com/milkv-duo/host-tools).
- La guía oficial recomienda V1 para el Duo de 64 MB y V2 para Duo 256M y Duo S. Comprueba siempre las notas de la versión y el nombre del objetivo.
- [Ejemplos oficiales en C/C++ y configuración de la herramienta de compilación cruzada](https://github.com/milkv-duo/duo-examples), incluidos [parpadeo GPIO](https://github.com/milkv-duo/duo-examples/tree/main/blink), [I²C](https://github.com/milkv-duo/duo-examples/tree/main/i2c), [SPI](https://github.com/milkv-duo/duo-examples/tree/main/spi) y la [guía de periféricos (PDF)](https://github.com/milkv-duo/duo-examples/blob/main/adc/PeripheralDriverOperationGuide_en.pdf).

## Hardware, periféricos y desarrollo de aplicaciones

- [Archivos oficiales de las placas: esquemas, hojas de datos y planos mecánicos](https://github.com/milkv-duo/duo-files).
- Esquemas de las placas: [Duo](https://github.com/milkv-duo/duo-files/blob/main/duo/hardware/duo-schematic-v1.2.pdf) · [Duo 256M](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/hardware/duo-256m-v1.01-schematic.pdf) · [Duo S](https://github.com/milkv-duo/duo-files/blob/main/duo-s/hardware/duo_s_SCH_v1.1.pdf).
- [Hojas de datos y documentación de chips Sophgo](https://github.com/sophgo/sophgo-doc/releases).
- Documentación de los SoC: [hoja de datos preliminar CV1800B/CV1801B (inglés)](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-en.pdf) y [edición en chino](https://github.com/milkv-duo/duo-files/blob/main/duo/datasheet/CV1800B-CV1801B-Preliminary-Datasheet-full-zh.pdf) · [hoja de datos preliminar SG2002 (chino)](https://github.com/milkv-duo/duo-files/blob/main/duo-256M/datasheet/SG2002_Preliminary_Datasheet_V1.0-alpha_CN.pdf) · [hoja de datos preliminar SG2000 (chino)](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_Preliminary_Datasheet_V1.0-alpha_CN.pdf) y [manual de referencia técnica (inglés)](https://github.com/milkv-duo/duo-files/blob/main/duo-s/datasheet/SG2000_TRM_V1.0-alpha.pdf).
- Proyectos oficiales de desarrollo: [multiplexación de pines](https://github.com/milkv-duo/duo-pinmux) · [wiringX](https://github.com/milkv-duo/duo-wiringx) · [accesorios](https://github.com/milkv-duo/accessories) · [demostración LVGL framebuffer](https://github.com/milkv-duo/duo-lvgl-fb-demo).
- Documentación: [GPIO y multiplexación de pines](https://milkv.io/docs/duo/application-development/pinmux) · [wiringX](https://milkv.io/docs/duo/application-development/wiringx) · [cámaras USB](https://milkv.io/docs/duo/camera/usb) · [framework multimedia](https://milkv.io/docs/duo/application-development/multimedia).
- Arduino: el antiguo [núcleo Milk-V Arduino](https://github.com/milkv-duo/duo-arduino) está archivado; su repositorio recomienda [Sophgo Arduino](https://github.com/kubuds/sophgo-arduino). También hay [ejemplos Arduino para Duo](https://github.com/milkv-duo/duo-arduino-examples). Comprueba la compatibilidad de la placa y del núcleo antes de usarlo.

## IA, visión artificial y multimedia

- Ejemplos TDL: [SDK V1 para CV180X / Duo original](https://github.com/milkv-duo/cvitek-tdl-sdk-cv180x) · [SDK V1 para SG200X / Duo 256M y Duo S](https://github.com/milkv-duo/cvitek-tdl-sdk-sg200x) · [ejemplos del SDK V2](https://github.com/milkv-duo/duo-tdl-examples).
- TPU y herramientas de modelos: [TPU SDK para CV180X](https://github.com/milkv-duo/tpu-sdk-cv180x) · [conversión de modelos TPU-MLIR](https://github.com/milkv-duo/tpu-mlir) · [TPU SDK para SG200X](https://github.com/milkv-duo/tpu-sdk-sg200x).
- [Ejemplos oficiales de multimedia](https://github.com/milkv-duo/duo-multimedia-examples) · [despliegue de modelos TDL](https://github.com/milkv-duo/duo-yolo-deployment).
- La [guía oficial de descargas](https://milkv.io/docs/duo/getting-started/download) también enumera imágenes de la comunidad por placa. Lee sus advertencias y verifica quién mantiene cada imagen y qué revisión de hardware admite.

## Sistemas operativos comunitarios y recursos de aprendizaje

Son proyectos independientes de la comunidad, no firmware oficial. La compatibilidad y el mantenimiento pueden cambiar; consulta la documentación de cada proyecto antes de instalarlo.

- Distribuciones Linux: [espejo de imágenes Fedora](https://mirror.iscas.ac.cn/fedora-riscv/dl/Milk-V/) · [Debian para Sophgo SG200X](https://github.com/scpcom/sophgo-sg200x-debian) · [generador de imágenes Ubuntu](https://github.com/ambraglow/milkv-duo-ubuntu) · [proyecto OpenWrt/VizOS](https://github.com/Pillar1989/VizOS).
- Sistemas de compilación y RTOS: [capa Yocto/OpenEmbedded](https://github.com/kinsamanka/meta-milkv) · [Zephyr en el núcleo secundario del Duo](https://github.com/kinsamanka/milkv-zephyros) · [NuttX para SG2000 / Duo S](https://github.com/lupyuen/nuttx-sg2000) · [BSP CVitek de RT-Thread](https://github.com/RT-Thread/rt-thread/tree/master/bsp/cvitek) · [port de ThreadX](https://github.com/saicogn/ThreadX-to-RISC-V64).
- [Foro comunitario de Milk-V Duo](https://community.milkv.io/c/duo/5) · [foro de Sophgo](https://forum.sophgo.com/) · [organización Milk-V Duo en GitHub](https://github.com/milkv-duo).

## Contribuciones y mantenimiento de enlaces

Abre una incidencia o una solicitud de cambios si encuentras un enlace roto, falta un recurso o un proyecto cambia las placas compatibles. Da prioridad a la documentación y a las páginas de versiones de los propios mantenedores; no vuelvas a alojar firmware. Antes de grabar una imagen, comprueba el modelo de placa, SoC, memoria, tipo de almacenamiento, modo de arranque e instrucciones; haz una copia de seguridad y utiliza una alimentación y un cableado seguros.

[Volver al índice de idiomas](README.md)
