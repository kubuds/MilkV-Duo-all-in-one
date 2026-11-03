# Milk-V Duo 系列 State-of-the-Art 仓库分析报告（2026-11）

> 本文以官方 `milkv.io/docs/duo/overview`（修订停在 2024-06，下称“官方 overview”）为底稿，**逐项核对并更新到 2026-11 的实际状态**。
> 配套数据见 [01-current-status-survey.md](01-current-status-survey.md)；升级工程见 [03-upgrade-plan.md](03-upgrade-plan.md)。
> 面向读者：刚买到 Milk-V Duo / Duo 256M / Duo S（或 Duo Module 01）的开发者与厂商。

---

## 0. TL;DR —— 先看这 10 行

1. **只做应用开发 / 快速出活**：烧录 **SDK V2 官方镜像**（`milkv-duo/duo-buildroot-sdk-v2`，buildroot 2025.02），跑 `duo-examples` / `duo-tdl-examples`，工具用 `duo-pinmux`、`duo-wiringx`、`kubuds/sophgo-arduino`。
2. **做产品 / 要长期维护**：走 **mainline 内核 6.18 LTS**（Arm 与 RISC-V 双线），vendor BSP 只借它的 TPU / ISP / 多媒体用户态；不要再基于 5.10.4 BSP 开新项目。
3. **内核版本现状**：BSP = 5.10.4（2021 年代码，**缺 5 年安全修复**）；最新 LTS = **6.18.60**；最新开发分支 = **7.4-rc1**（linux-next 20261102）。
4. **mainline 对 Duo 系列的支持已经“能启动、能干活”**：v6.18 内含 CV1800B（Duo）RISC-V DTS、SG2002（Duo 256M 同芯片）RISC-V DTS、SG2000（Duo S 同芯片）**arm64** DTS（Duo Module 01），以及 pinctrl/clk/gpio/reset/mmc/usb 等一批 sophgo 驱动；**7.4-rc1（HEAD）更进一步：Duo S（双架构）与 Duo 256M（RISC-V + 以太网 overlay）的板级 DTS 已进 mainline**。
5. **mainline 还缺的**：Duo 256M 的 **arm64** 板级 DTS（唯一板级缺口）、AIC8800 Wi-Fi 6/BT 驱动、TPU 驱动、ISP/视频编解码（MMF 闭源/半闭源）、音频。这些只能走 vendor 栈；6.18 LTS 用户可直接用升级工程的回植 DTS（duosdk-next）。
6. **TPU 能力**：`tpu-mlir`（模型→cvimodel）+ `cviruntime/cvikernel/cvimath/cvibuilder`（运行时）+ `tdl_sdk`（一站式算法）+ `ive` + `tdl-models`（模型库）。全都随 SDK V2 或 milkv-duo 独立仓库发布。
7. **Duo 64M（CV1800B）已 EOL**，官方停产；新设计选 **Duo 256M（SG2002）/ Duo S（SG2000）/ Duo Module 01**。
8. **不用看的仓库**：`duosdk` 组织除 `u-boot@duo-next`、`qemu@duo-qemu` 外全是 2023 快照；`milkv-duo/milkv-duo-*` 拆分组件、`duo-buildroot-sdk`(V1)、`duo-sdk`、`duo-arduino`、`cvitek-tdl-sdk-*`、`tpu-sdk-cv180x` 均已被取代（详见 §7）。
9. **仿真先行**：`duosdk/qemu@duo-qemu` 有 Duo 机器模型（T-head C906），无板也能做内核/启动链开发与 CI。
10. **安全**：任何仍在跑 5.10.4 BSP 的存量设备应视为高风险，升级 6.18 LTS 是唯一根治手段（见 §6）。

---

## 1. 硬件矩阵（据官方 overview，2024-06 版）与勘误

| | Duo（**EOL**） | Duo 256M | Duo S | Duo Module 01 |
| --- | --- | --- | --- | --- |
| SoC | CV1800B | SG2002 | SG2000 | SG2000 |
| RISC-V | C906@1GHz + C906@700MHz | 同左 | 同左 | 同左 |
| Arm | — | 1× Cortex-A53@1GHz（**arm64**） | 1× Cortex-A53@1GHz（**arm64**） | 1× Cortex-A53@1GHz |
| MCU | 8051（8KB SRAM） | 8051（6KB） | 8051（6KB） | 8051（6KB） |
| TPU | 0.5 TOPS@INT8 | **1.0 TOPS@INT8** | 0.5 TOPS@INT8 | 0.5 TOPS@INT8 |
| 内存 | 64MB SIP | 256MB SIP | 512MB SIP | 512MB SIP |
| 存储 | microSD / SD NAND | microSD / SD NAND | microSD + eMMC 焊盘 | microSD + 8GB eMMC |
| 摄像头 | 1× MIPI CSI 2-lane | 1× MIPI CSI 2-lane | 2× MIPI CSI 2-lane | 2× MIPI CSI 2-lane |
| 显示 | — | — | MIPI DSI 4-lane（排针） | MIPI DSI 4-lane（39P FPC） |
| 网络 | 100M（扩展板） | 100M PHY | 100M RJ45 | 2× 100M RJ45 |
| 无线 | — | — | 可选 **Wi-Fi 6 / BT 5.4** | Wi-Fi 6 / BT 5.4 |
| USB | Type-C | Type-C | Type-C 或 4× USB2.0 HOST | 1× Type-C / 4× A HOST |
| 启动切换 | — | RISC-V/Arm 二选一（可双系统） | **BOOT 开关**（RISC-V/Arm） | 同左 |

**勘误与补充（相对官方 overview）**：
- Arm 核是 **AArch64（Cortex-A53）**，不是 armhf：SDK V2 的 Arm 目标是 `glibc-arm64`，板级配置写明 `CA53 + SD + DDR 512MB`；编译请用 `aarch64-linux-gnu-` 工具链。
- “RISC-V/ARM 切换”是**启动核二选一**（大核镜像不同），不是同时双核双系统；小核（C906L/8051）由 FreeRTOS/裸机镜像另行烧写（工具见 `kubuds/rproc-burn`）。
- Duo S 的 Wi-Fi 模组驱动是 **AIC8800**（BSP 内 `CONFIG_AIC8800`，固件放 `/mnt/system/firmware/aic8800`），**未进入 mainline**。
- TPU 算力：Duo 256M（SG2002）为 1.0 TOPS，其余 0.5 TOPS；这是 NPU（CVITEK TPU），与算能 BM168x 系列（`libsophon`）不是一套软件栈。

---

## 2. 官方文档哪些已经过时

| 文档 | 停更时间 | 过时点 |
| --- | --- | --- |
| `docs/duo/overview` | 2024-06 | 硬件矩阵仍准确；“OS Support: Buildroot, RTOS” 未提 mainline/RT-Thread 现状 |
| `docs/duo/resources/mainline` | 2024-02 | 表里 “In mainline since 6.7 / Under Review” 一大批：截至 v6.18，GPIO(6.8)、Clock(6.10)、SPI&I2C(6.10)、MMC(6.9/6.10)、USB(6.10) 等**早已合入**；pinctrl、clk 驱动现已覆盖 cv1800b/cv1812h/sg2000/sg2002/sg2042/sg2044 |
| `docs/duo/resources/upstream-status` | 2024-07 | 同上；且未反映 arm64 侧（SG2000）2024 年后新增的 mainline 支持 |
| `docs/duo/getting-started/buildroot-sdk` | — | 仍有效：SDK V1/V2 划分、7 个目标板、编译步骤与现实一致 |
| `docs/duo/application-development/tpu/*` | — | 基本有效，但示例只覆盖 “简单测试”；正式开发应走 TDL SDK |

**结论**：官方文档在“硬件参数 / SDK 编译 / 应用示例”上可用，在“mainline 状态 / 内核版本 / 安全”上已过时两年多，本报告补上。

---

## 3. 软件栈现状（2026-11）

### 3.1 三层栈，按需求选

```
┌────────────────────────────────────────────────────────────┐
│ A. Vendor 栈（SDK V2，官方镜像）                              │
│    buildroot 2025.02 · Linux 5.10.4 BSP · u-boot 2021.10     │
│    + ISP/MMF(vi/vpss/vcodec) + TPU 驱动 + AIC8800 Wi-Fi      │
│    → 全功能（摄像头/编解码/TPU/Wi-Fi），但内核 2021 年水平     │
├────────────────────────────────────────────────────────────┤
│ B. Mainline 栈（推荐新项目）                                  │
│    Linux 6.18 LTS（或 7.4-rc1 HEAD）· u-boot master · OpenSBI │
│    → 启动/外设/网络/USB/SD 全通；缺 TPU、ISP、Wi-Fi、音视频    │
│    → TPU/多媒体可等：驱动在 vendor 侧，用户态库可复用          │
├────────────────────────────────────────────────────────────┤
│ C. RTOS 栈                                                  │
│    FreeRTOS（8051 小核 / C906L 小核）· RT-Thread bsp/cvitek   │
│    · cvi_alios_open · Zephyr（尚无 Duo BSP）                  │
└────────────────────────────────────────────────────────────┘
```

### 3.2 各层关键版本

| 组件 | SDK V1 | SDK V2（现行） | Mainline（现行） |
| --- | --- | --- | --- |
| Linux | 5.10.4 | **5.10.4**（`linux_5.10`，CONFIG_ARCH_CVITEK） | **6.18.60 LTS** / 7.4-rc1 |
| U-Boot | 2021.10 | 2021.10 | master（含 `board/sophgo/milkv_duo`） |
| OpenSBI | 89182b2 | 89182b2 | master（generic + sophgo） |
| Buildroot | 2021.05 | **2025.02** | —（可换 Buildroot 2025.11+/Yocto） |
| 支持板 | 仅 Duo 64M | Duo / Duo256M / DuoS（7 目标） | Duo（RISC-V）、SG2002 通用板（RISC-V）、SG2000 arm64（Module 01） |
| libc | musl-riscv64 | musl-riscv64 / **glibc-arm64** | 自选 |

### 3.3 mainline 支持实测（对 v6.18 / u-boot master 逐项核对）

**Linux v6.18 已包含**：
- `arch/riscv/boot/dts/sophgo/`：`cv1800b.dtsi`、**`cv1800b-milkv-duo.dts`**（Duo 64M）、`sg2002.dtsi` + `sg2002-licheerv-nano-b.dts`（SG2002 芯片级支持）、cv181x、sg2042、sg2044。
- `arch/arm64/boot/dts/sophgo/`：`sg2000.dtsi` + **`sg2000-milkv-duo-module-01.dtsi/.dts`**（SG2000 的 arm64 核支持）。
- 驱动：`drivers/pinctrl/sophgo/`（pinctrl-cv1800b/cv1812h/**sg2000**/**sg2002**/sg2042/sg2044）、`drivers/clk/sophgo/`（clk-cv1800 家族）、reset/gpio/mmc/usb/ethernet 等（2024 年 upstream-status 表中 “Accepted” 的均已合入）。

**Linux v6.18 尚缺（相对三块板的完整体验）**：
1. `sg2002-milkv-duo256m` 板级 DTS（RISC-V 与 arm64 两个核）；**注意：7.4-rc1 已补 riscv 侧**（含 `-eth` 以太网 overlay）；
2. `sg2000-milkv-duos` 板级 DTS（RISC-V 与 arm64）；**注意：7.4-rc1 已补双侧**（上游命名 `sg2000-milkv-duo-s`）；arm64 侧连 `sg2002.dtsi` 都还没有（7.4 仍缺，Duo 256M arm64 是最后一个板级缺口）；
3. AIC8800 Wi-Fi 6 / BT 驱动（vendor extdrv 里，未 upstream）；
4. TPU（`osdrv/interdrv/tpu`）、IVE、ISP（vi/vpss）、视频编解码（cvi_vc_drv/jpeg）、音频等多媒体驱动；
5. 小核 remoteproc 管理（可用 `kubuds/rproc-burn` 用户态方案绕过）。

**U-Boot master 已包含**：`board/sophgo/milkv_duo`、`board/sophgo/licheerv_nano`、`arch/riscv/dts/cv1800b-milkv-duo.dts`、`sg2002-licheerv-nano-b.dts`。尚无 Duo 256M / Duo S 板级目录。
> 注：`duosdk/u-boot@duo-next`（2023-12）是当年同一批工作的先行版本，已被 mainline 取代。

**OpenSBI**：mainline generic 平台可直接服务 CV18xx（SDK 内 89182b2 建议一并升级到 1.4+）。

### 3.4 TPU（算能已释放能力全图）

| 能力 | 仓库 | 说明 |
| --- | --- | --- |
| 模型编译 | `milkv-duo/tpu-mlir` | ONNX/Caffe/PyTorch/TFLite → **cvimodel**；提供 Docker 化转换环境 |
| 模型库 | `milkv-duo/tdl-models` | 预转换 cvimodel（检测/分类/人脸…） |
| 运行时 | SDK V2 内 `cviruntime`（或 `kubuds/cviruntime`） | `cviruntime.h`/`bmruntime.h` API、custom_op、python 绑定 |
| 指令层 | `cvikernel` | TPU 指令生成（“汇编器”），写自定义算子用 |
| 数学库 | `cvimath` | 常用算子封装 |
| 模型格式 | `cvibuilder` + `flatbuffers` | cvimodel 结构定义 |
| 一站式算法 | SDK V2 内 `tdl_sdk`（`kubuds/tdl_sdk` 镜像） | 人脸检测/识别、YOLOv5/v8/v11/v12、行人/宠物检测、分类、音频（BLIP）等 |
| 图像硬件加速 | `ive` | IVE 硬件算子（缩放/形态学/差分…） |
| 示例 | `milkv-duo/duo-tdl-examples`、`duo-multimedia-examples`、`duo-yolo-deployment` | 摄像头+TPU 全链路示例 |
| 面向 BM168x 的另一套 | `kubuds/libsophon` | **不是 Duo 的 TPU 栈**，仅同厂参考 |

TPU 调用链：`你的模型 → (tpu-mlir) → cvimodel → (tdl_sdk 或 cviruntime) → /dev/cvi-tpu 驱动(BSP) → TPU`。
注意：**TPU 驱动只在 5.10.4 BSP 中**（`osdrv/interdrv/tpu`），mainline 6.18 无 TPU 驱动 → 要用 TPU 就必须在 vendor BSP 内核上跑，或等待驱动 upstream（见 03 号报告的计划）。

---

## 4. 内核版本选型（这是本报告的核心建议）

| 内核 | 版本现状（kernel.org, 2026-11-03） | Duo 适用性 | 建议 |
| --- | --- | --- | --- |
| Vendor BSP | 5.10.4（2021-01 基线） | 全功能（TPU/ISP/Wi-Fi/编解码） | **仅存量维护**；新项目禁用 |
| 5.10.273 LTS | 官方 LTS 仍在维护 | 可作 BSP 底座做最小升级 | 过渡方案 |
| 6.6.161 / 6.1.191 LTS | 维护中 | 可用但无必要 | 跳过 |
| **6.18.60 LTS（推荐）** | 最新 LTS（2026-10-30 发布） | mainline sophgo 支持最完整；arm64+riscv64 双线 | **新项目默认** |
| **7.4-rc1（HEAD）** | mainline 开发分支 | 跟进最新修复/特性 | 做前瞻/上游化开发 |
| linux-next (20261102) | 日更 | 冒烟测试用 | 厂商 CI 可选 |

安全视角：5.10.4 → 6.18 LTS 一次性吸收 **5 年多**的安全修复（详见 §6）。

---

## 5. 从哪里入手（三类人三条路径）

### 5.1 刚买板子的开发者（想点灯、跑摄像头、跑 AI）
1. 确认板型：Duo 64M（RISC-V）/ Duo 256M（RISC-V 或 Arm）/ Duo S（BOOT 开关选核）。
2. 从 `milkv-duo/duo-files`（或官方镜像页）下载 **SDK V2 v2.0.1** 镜像烧录（Duo 64M 用 V1 v1.1.4）。
3. 装 `milkv-duo/duo-pinmux`（引脚复用）、`milkv-duo/duo-wiringx`（GPIO）；Arduino 用户用 `kubuds/sophgo-arduino`。
4. 跑 `milkv-duo/duo-examples`（GPIO/UART/I2C/SPI）→ `duo-multimedia-examples`（摄像头）→ `duo-tdl-examples` + `tdl-models`（AI）。
5. 想换 RISC-V/Arm 核：SDK V2 同时出 `musl-riscv64` 与 `glibc-arm64` 镜像，Duo S 用 BOOT 开关选择。
6. 想跑 RTOS：`milkv-duo/duo-8051`（8051）、`kubuds/rproc-burn`（烧 C906L 小核固件）、`kubuds/rt-thread` 的 `bsp/cvitek`。

### 5.2 厂商 / ODM（做产品，要 3~5 年维护）
1. 选 **Duo Module 01（SG2000）** 或 Duo 256M / Duo S；停产的 Duo 64M 不要新设计。
2. 内核直接上 **6.18 LTS**（arm64 与 riscv64 双线并行开发，见 03 号报告的升级工程）；U-Boot 用 master + board/sophgo；根文件系统用 Buildroot 2025.x 或 Yocto（`duosdk/meta-riscv` 是 2023 快照，需自更新）。
3. 需要 TPU/摄像头的产线功能：短期用 **双内核策略**（功能镜像 5.10.4 BSP + 通用镜像 6.18 LTS），中期把 `osdrv` 的 TPU/IVE 驱动移植到 6.18（6.18 的驱动模型更干净，DMA/fb/clk 接口已变）。
4. 安全基线：关掉不用的调试口、rootfs 只读、逐月跟进 6.18.x stable、把 §6 的 CVE 清单当回归测试表。
5. 供应链注意：Wi-Fi（AIC8800）固件/驱动无 mainline 支持，需长期自维护或选有线型号。

### 5.3 内核/启动链/工具链开发者（或无板 CI）
1. `duosdk/qemu@duo-qemu`：Duo 机器模型（C906、timer、UART、mrom/firmware），可跑内核冒烟测试；注意基线是 2023 的 QEMU，可将 10 个提交移植到新 QEMU。
2. `duosdk/u-boot@duo-next`：当年的 mainline u-boot Duo 移植（8 提交），已被 upstream 取代，作历史参考。
3. 交叉工具链：`milkv-duo/host-tools`（厂商工具链）或发行版 `gcc-riscv64-linux-gnu` / `gcc-aarch64-linux-gnu`（mainline 内核够用）；进阶用 `kubuds/llvm-project`。
4. 上游化入口：给 v6.18 补 `sg2002-milkv-duo256m.dts`、`sg2000-milkv-duos.dts`（缺什么补什么，见 §3.3）是最好的贡献点。

---

## 6. 安全与 CVE 现状

**核心事实**：SDK V1/V2 的内核是 **Linux 5.10.4（2021-01 发布）**，此后 5.10.x stable 的 270+ 次更新、约 **数万**个修复（含大量 CVE）**一个都没有**。这不是“版本旧一点”的问题，是可被已知工具链直接利用的问题。

升级到 6.18 LTS（或至少 5.10.273）一次性修复的代表性 CVE 类别（举例，非全表）：

| CVE | 类别 | 5.10.4 是否受影响 |
| --- | --- | --- |
| CVE-2022-0847（Dirty Pipe） | 任意文件写 | ✅ 受影响（5.8–5.16） |
| CVE-2022-2588 / CVE-2022-2586（nftables/netfilter） | 本地提权 | ✅ |
| CVE-2022-0185（fsconfig 堆溢出） | 本地提权 | ✅（5.1–5.16） |
| CVE-2023-0179（nftables 栈溢出） | 本地提权 | ✅ |
| CVE-2023-32233（netfilter use-after-free） | 本地提权 | ✅ |
| CVE-2023-3269（StackRot） | 本地提权 | ✅（5.10–6.4） |
| CVE-2023-3390 / CVE-2023-35001（netfilter） | 本地提权 | ✅ |
| CVE-2024-1086（nf_tables UAF） | 公开利用 | ✅ |
| CVE-2024-36971 / CVE-2024-41009 系列 | 内核 UAF/越界 | ✅ |
| ksmbd / io_uring / n_gsm / vt 等 2023–2025 系列 | 多类 | ✅ |
| TLS/net/bluetooth/Wi-Fi 栈修复 | 多类 | ✅（含 AIC8800 类驱动周边） |

**BSP 之外的存量风险**（升级内核也解决不了的）：
1. AIC8800 Wi-Fi 驱动 + 闭源固件：无 mainline 审计，需厂商自查；
2. rootfs：SDK 镜像默认可写、root 无密码/弱口令的早期镜像、dropbear/openssh 老版本 —— 用 Buildroot 2025.02 重建并显式配置；
3. TPU/MMF 用户态库（闭源 .so）无法审计，暴露面在 `/dev/cvi-*` 设备节点，建议收紧权限；
4. 无安全启动链：fsbl/u-boot 均未验签（两代 SDK 皆然），对量产设备是硬伤；
5. 8051/C906L 小核固件烧写通道（串口/HTTP CGI）务必在量产固件里关闭（参考 `kubuds/rproc-burn` 的参数化设计）。

**结论**：新项目直接上 6.18 LTS；存量 5.10.4 设备至少把 rootfs 与暴露端口收紧，按 03 号报告的内核升级路径安排迁移。

---

## 7. 仓库评级：用哪个、看哪个、不用看

### 7.1 ✅ 主力（直接用）
| 仓库 | 用途 |
| --- | --- |
| `milkv-duo/duo-buildroot-sdk-v2` | SDK V2 全功能镜像/开发（Duo 256M、Duo S、Module 01） |
| `milkv-duo/duo-files` | 官方镜像与资料下载 |
| `milkv-duo/duo-examples`、`duo-multimedia-examples`、`duo-tdl-examples` | 应用示例 |
| `milkv-duo/tpu-mlir` + `tdl-models` | AI 模型转换与模型库 |
| `milkv-duo/duo-pinmux`、`duo-wiringx`、`milkv-duo/host-tools` | 引脚/GPIO/工具链 |
| `kubuds/sophgo-arduino`、`kubuds/rproc-burn`、`kubuds/rt-thread` | Arduino / 小核烧写 / RT-Thread |
| `kubuds/MilkV-Duo-all-in-one` | 资料总索引（本仓库） |
| upstream：`torvalds/linux` ≥6.18、`u-boot/u-boot` master、`opensbi/opensbi` | mainline 内核/启动链 |

### 7.2 🟡 参考（特定需求才看）
| 仓库 | 何时看 |
| --- | --- |
| `milkv-duo/duo-buildroot-sdk`（V1）+ `milkv-duo/milkv-duo-*` 7 个拆分件 | 只维护 Duo 64M 时 |
| `duosdk/qemu@duo-qemu` | 无板仿真/CI |
| `duosdk/u-boot@duo-next` | 历史参考（已被 upstream 取代） |
| `duosdk/buildroot@duosdk` | 参考 2023 年 buildroot 板级做法 |
| `kubuds/cviruntime/cvikernel/cvimath/cvibuilder/ive/tdl_sdk` | 需要与 SDK 内嵌版不同的分支（cv184x-v6.x 等）时 |
| `kubuds/freertos`、`FreeRTOS-Kernel`、`cvi_alios_open` | 小核 RTOS 开发 |
| `milkv-duo/cvitek-tdl-sdk-sg200x`、`tpu-sdk-sg200x` | TDL/TPU 老示例对照 |
| `sophgocommunity/CV180-Duo` | Duo 64M 数据手册/历史资料 |
| `kubuds/sophpi`、`milkv-duo/accessories` | 硬件设计参考 |
| `kubuds/kvmd`、`picoclaw`、`RV-EAI` | 周边玩法（远程控制/AI 助手/具身智能） |

### 7.3 ❌ 不用看（已被取代或无 Duo 内容）
| 仓库 | 原因 |
| --- | --- |
| `duosdk/duo-buildroot-sdk` | 纯镜像，落后上游 180 提交 |
| `duosdk/linux`（两个分支）、`duosdk/opensbi`、`duosdk/zephyr`、`duosdk/meta-riscv` | 2023 快照/无定制；Zephyr 无 Duo BSP |
| `milkv-duo/duo-sdk` | 被 SDK V2 取代 |
| `milkv-duo/duo-arduino` | 官方明示弃用 → `kubuds/sophgo-arduino` |
| `milkv-duo/milkv-duo-pinmux`、`cvi-pinmux` | 被 `duo-pinmux` 取代 |
| `milkv-duo/tpu-sdk-cv180x`、`cvitek-tdl-sdk-cv180x` | CV180x（Duo 64M）老栈 |
| `milkv-duo/duo-examples-pinpong`、`duo-arduino-examples`、`duo-lvgl-fb-demo`、`lv_port_linux` | 示例/演示，按需检索即可 |
| `sophgocommunity` 其余 4 仓（Pioneer_Doc、SG2042-*、Airbox） | 与 Duo 无关 |
| `kubuds/A210-Melon-Pi-all-in-one`、`karsier-website`、`flagcx-packaging`、`kuloveinterns` | 与 Duo 无关 |

---

## 8. Day-1 检查清单（买板子第一周）

- [ ] 板型与启动核确认（Duo S：BOOT 开关位置决定 RISC-V/Arm 镜像）
- [ ] 烧 SDK V2 镜像，跑通串口登录 + USB RNDIS / 以太网 SSH
- [ ] `duo-pinmux` 确认要用的引脚复用，`duo-wiringx` 点灯
- [ ] 摄像头：`duo-multimedia-examples` 出流；显示（Duo S/Module 01）走 MIPI DSI 示例
- [ ] AI：`tpu-mlir` 转一个自己的模型 → `duo-tdl-examples` 跑通推理
- [ ] 小核：`kubuds/rproc-burn` 烧一个 FreeRTOS/裸机 blink
- [ ] 安全：改 root 密码、关不需要的端口、记录当前内核版本（`uname -r` 应为 5.10.4）
- [ ] 立项决策：产线项目 → 直接开始 6.18 LTS 移植（见 03 号报告），不要在 5.10.4 上加功能

---

*本报告由 Karen KUBUDS AI Coders 基于 2026-11-03 的公开仓库数据与官方文档核对生成；mainline 仓库内容为实测核对（torvalds/linux v6.18、u-boot master），内核版本数据取自 kernel.org releases.json。*
