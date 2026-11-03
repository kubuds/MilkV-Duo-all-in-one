# Milk-V Duo 系列生态现状报告（2026-11）

> 报告日期：2026-11-03 · 覆盖范围：GitHub 组织 `duosdk`、`milkv-duo`、`sophgocommunity`、`kubuds` 全部公开仓库
> 目标读者：准备基于 Milk-V Duo / Duo 256M / Duo S 做开发的开发者与厂商
> 结论速览见 [02-sota-repo-analysis.md](02-sota-repo-analysis.md) 的 “TL;DR”。本文件是**摸底数据**，只陈述现状，不做选型建议。

---

## 1. 调研方法

- 通过 GitHub API 枚举四个组织的全部仓库（`duosdk` 9 个、`milkv-duo` 38 个、`sophgocommunity` 5 个、`kubuds` 49 个，共 101 个仓库），记录：名称、描述、fork 来源、默认分支、最近推送时间、star 数。
- 对 `duosdk` 全部 9 个仓库执行浅克隆并逐个梳理；对其自定义分支（`duosdk` / `duo-next` / `duo-qemu`）用 GitHub compare 接口统计与上游 master 的 ahead/behind 及提交清单。
- 对 `milkv-duo/duo-buildroot-sdk-v2`（当前主力 SDK）完整浅克隆并解剖目录结构、内核版本、板级配置、TPU/多媒体组件。
- 对照官方文档 `milkv.io/docs/duo/overview`（修订停在 2024-06）、`resources/mainline`、`resources/upstream-status`（修订停在 2024-02/2024-07）核实文档口径。
- 抽样核对 `kubuds`、`sophgocommunity` 仓库 README 判定与 Duo 系列的相关性。

---

## 2. `duosdk` 组织（9 个仓库）逐仓梳理

组织定位：**个人/团队的“SDK 归档 + 定制分支”集合**。9 个仓库全部是 fork，0 star，最后活动集中在 2023-07 ~ 2024-05。它包含两类内容：(a) 上游镜像（无定制提交，纯快照）；(b) 少量有价值的定制分支（Duo 的 QEMU 机器模型、mainline u-boot 移植、buildroot 板级支持、CVitek BSP 内核）。

| 仓库 | 基线（默认分支） | 定制分支 | 定制内容 | 与上游差距 | 状态评估 |
| --- | --- | --- | --- | --- | --- |
| `duosdk/linux` | torvalds/linux **v6.7**（2024-01） | `duosdk` | Linux **5.10.4 CVitek BSP** 内核（含 ~781 个厂商/背ported 提交，2020-12 基线） | behind 266 910 | 分支内容是 5.10 时代的 CV18xx BSP，**已过时**；master 只是 6.7 镜像 |
| `duosdk/u-boot` | u-boot **2024.01** | `duosdk`、`duo-next` | `duosdk`：u-boot-2021.10 CVitek BSP 移植（4 commits：cv181x/cv180x、SD 启动、USB dwc2）；`duo-next`：**mainline u-boot 2024.01 + Milk-V Duo 初始支持**（8 commits：boot0 header、cvitek 以太网 PHY、DHCP 启动、DTS、milkv duo defconfig） | behind 15 005 / 11 | `duo-next` 是**未合入上游的宝贵移植成果**（当时 u-boot 尚无 duo 板级支持）；`duosdk` 是旧 BSP |
| `duosdk/buildroot` | buildroot 2023.x | `duosdk` | 12 commits：CV181X/CV182X ext4、musl-riscv64 libc、milkv-duo 板级目录、wiringX、dnsmasq、RNDIS、LED、os-release 等 | behind 13 051 | 早期“用原生 buildroot 做 Duo 根文件系统”的尝试，**已被 SDK V2（buildroot 2025.02）取代** |
| `duosdk/qemu` | QEMU 8.x（2023-08） | `duo-qemu` | 10 commits：移植 T-head Xuantie CPU（来自 T-head-Semi/qemu）、Lichee Pi 机器、**Milk-V Duo 机器模型**（timer、UART、firmware/mrom、C910 CSR 修正） | behind 1 957 | **QEMU 侧唯一的 Duo 仿真模型**，可用于无板开发/CI，但基线老（2023-08） |
| `duosdk/duo-buildroot-sdk` | milkv-duo/duo-buildroot-sdk（SDK V1）`develop` | `develop`、`libcamera` | 无定制：compare 结果 **ahead 0 / behind 180** | — | **纯过时镜像**，可直接忽略 |
| `duosdk/opensbi` | opensbi **1.4**（2023-12） | 无 | 无 | — | 纯镜像 |
| `duosdk/buildroot`（同上之外）/ `meta-riscv` | Yocto RISC-V 层（2023-07） | 无 | 无 | — | 与 Duo 无关的纯镜像 |
| `duosdk/zephyr` | Zephyr 3.4（2023-07） | 无 | 无 | — | 纯镜像；**没有任何 Duo/CV18xx BSP 工作** |
| `duosdk/isp_tuning` | `sg200x-dev`（2024-02） | `sg200x-dev` | ISP 调参数据（cv18xx 系列） | — | 数据快照，随 SDK V2 内 `isp_tuning/` 演进 |

**小结**：`duosdk` 组织 = “2023 下半年 ~ 2024 上半年的生态快照”。真正有延续价值的只有三样：
1. `u-boot` 的 `duo-next` 分支（mainline u-boot + Duo 支持，8 个提交）；
2. `qemu` 的 `duo-qemu` 分支（Duo 仿真模型，10 个提交）；
3. `buildroot` 的 `duosdk` 分支（12 个提交，可作历史参考）。
其余（`linux@duosdk` 的 5.10 BSP、`duo-buildroot-sdk` 镜像、`opensbi`/`zephyr`/`meta-riscv`/`isp_tuning` 镜像）均已被 SDK V2 或 mainline 取代。

---

## 3. `milkv-duo` 组织（38 个仓库）盘点与分类

官方组织。可分六类：

### 3.1 SDK（最重要）
| 仓库 | 内容 | 现状 |
| --- | --- | --- |
| **`duo-buildroot-sdk-v2`** | **当前主力 SDK**：buildroot 2025.02 + Linux **5.10.4 BSP** + u-boot 2021.10 + opensbi 89182b2 + fsbl；支持 7 个目标板（`milkv-duo-musl-riscv64-sd`、`milkv-duo256m-{musl-riscv64,glibc-arm64}-sd`、`milkv-duos-{musl-riscv64,glibc-arm64}-{sd,emmc}`）；内含 TPU（cviruntime/cvikernel/cvimath/cvibuilder/ive）、多媒体（cvi_mpi/cvi_rtsp）、TDL SDK、osdrv 驱动（vi/vpss/vcodec/tpu/ive/wdt/rtc/saradc…）、无线驱动（AIC8800/realtek/mediatek/bouffalolab/icommsemi） | 最近推送 2025-12，活跃；**Duo 256M / Duo S 的唯一正确入口** |
| `duo-buildroot-sdk`（V1） | buildroot 2021.05 + Linux 5.10.4 + u-boot 2021.10 + opensbi；仅 RISC-V；64MB Duo 专用 | 维护模式；仅 Duo 64M 使用 |
| `duo-sdk` | 早期独立 SDK 包（2024-09 后无更新） | 被 V2 取代 |
| `host-tools` | CVitek 交叉工具链（gcc 等） | 仍被 SDK 使用 |
| `milkv-sg200x-toolchain-demo` | 工具链演示 | 参考 |

### 3.2 应用/示例
`duo-examples`（C/C++ 基础示例）、`duo-multimedia-examples`、`duo-media-examples`、`duo-tdl-examples`（SDK V2 TDL 示例）、`duo-yolo-deployment`、`duo-examples-pinpong`、`duo-arduino-examples`、`duo-lvgl-fb-demo`、`lv_port_linux`、`duos-arm-nas`（Duo S ARM NAS，刚起步）。

### 3.3 TPU / AI
`tpu-mlir`（模型编译器，转 cvimodel）、`tpu-files`、`tpu-sdk-cv180x` / `tpu-sdk-sg200x`（TPU SDK 示例/库）、`cvitek-tdl-sdk-cv180x` / `cvitek-tdl-sdk-sg200x`（TDL SDK 示例，V1 时代）、`tdl-models`（模型库）、`eigen`、`sophgo-library`。

### 3.4 板级工具 / 外设
`duo-pinmux`（Duo/Duo256M/DuoS 引脚复用，最新）、`cvi-pinmux`、`milkv-duo-pinmux`、`duo-wiringx`（GPIO 库）、`duo-8051`（8051 小核）、`accessories`、`duo-files`（镜像与资料下载）。

### 3.5 V1 时代的拆分组件（fork，均为 “maintained for the buildroot”）
`milkv-duo-linux`（5.10.4，分支 linux-5.10.4）、`milkv-duo-u-boot`（分支 duo-ion）、`milkv-duo-opensbi`、`milkv-duo-buildroot`、`milkv-duo-buildroot-libraries`、`milkv-duo-smallcore-freertos`、`milkv-duo-pinmux`。
→ 仅当维护 **Duo 64M / SDK V1** 时才需要；Duo 256M / Duo S 开发者**不必看**。

### 3.6 其他
`duo-arduino`（README 明示：**已弃用，请用 `kubuds/sophgo-arduino`**）。

---

## 4. `duosdk` vs `milkv-duo` 对比结论

| 维度 | duosdk | milkv-duo | 结论 |
| --- | --- | --- | --- |
| 定位 | 归档 + 定制分支实验 | 官方 SDK / 工具 / 示例 | 以 milkv-duo 为准 |
| 内核 | 5.10.4 BSP（`linux@duosdk`）+ 6.7 镜像 | 5.10.4 BSP（V1/V2 SDK 内嵌、`milkv-duo-linux`） | 两边 BSP 同源；duosdk 无新增 |
| u-boot | 2021.10 BSP 移植 + **mainline 2024.01 Duo 移植（duo-next）** | 2021.10 BSP（SDK 内嵌、`milkv-duo-u-boot`） | **duosdk 独有 mainline u-boot 工作**，官方当时未做 |
| 根文件系统 | buildroot 2023.x 板级（duosdk 分支） | SDK V1 buildroot 2021.05 / V2 buildroot 2025.02 | V2 胜出 |
| 仿真 | **QEMU Duo 机器模型（duo-qemu）** | 无 | **duosdk 独有** |
| TPU/多媒体 | 无 | 全套（tpu-mlir / TDL / cvi_mpi / tpu-sdk-*） | milkv-duo 独有 |
| 工具 | 无 | duo-pinmux / wiringx / duo-8051 / host-tools | milkv-duo 独有 |
| fork 新鲜度 | `duo-buildroot-sdk` 落后 180 提交，其余镜像停在 2023 | V2 SDK 更新到 2025-12 | milkv-duo 活跃 |

**一句话**：`duosdk` 相对 `milkv-duo` 的增量价值只有 **QEMU Duo 机器模型** 和 **mainline u-boot Duo 移植** 两块，其余都是重复或过时内容。

---

## 5. `sophgocommunity` 组织（5 个仓库）中涉及 Duo 的仓库

| 仓库 | 是否涉及 Duo 系列 | 说明 |
| --- | --- | --- |
| **`CV180-Duo`** | ✅ **是** | Milk-V Duo（CV1800B）产品简介、CV1800B Product Brief PDF、引脚/资料。**仅覆盖 Duo 64M**，不含 Duo 256M / Duo S；最后更新 2023-09，许可 CC BY-NC-SA 4.0（注意非软件许可） |
| `Pioneer_Doc` | ❌ | SG2042 Pioneer 文档 |
| `SG2042-Newsletter` | ❌ | SG2042 周报 |
| `SG2042-Wiki` | ❌ | SG2042 wiki |
| `Airbox` | ❌ | AIGC 智算盒（Stable Diffusion/ChatGLM 部署），非 Duo |

**结论**：`sophgocommunity` 下与 milkv duo / duo 256 / duo S 相关的仓库**只有 `CV180-Duo` 一个**，且只覆盖老 Duo 64M、内容停留在 2023 年，仅可当历史资料/数据手册来源。

---

## 6. `kubuds` 组织（49 个仓库）中涉及 Duo 的仓库

`kubuds` 同时维护 “Sophgo CV18xx SDK 组件镜像（带 sg200x-dev / cv184x-v6.x 定制分支）” 与若干自研工具。按相关性分层：

### 6.1 直接服务于 Milk-V Duo 系列（优先看）
| 仓库 | 分支 | 说明 |
| --- | --- | --- |
| `MilkV-Duo-all-in-one` | master | Duo / Duo 256M / Duo S 资料与资源总索引（本仓库），持续更新 |
| `sophgo-arduino` | sg200x-dev | Arduino 集成，**官方 duo-arduino 的继任者**（milkv-duo/duo-arduino README 明示指向这里） |
| `sophpi` | sg200x-evb | CV18xx 系列开源硬件平台（Duo 同族开发板），含硬件资料 |
| `rproc-burn` | main | **SG200X（Duo / Duo256 / DuoS）C906L 小核固件烧写工具**（burntool/burnd/remoteproc），自研、活跃（2026-10） |
| `host-tools` | master | CVitek 交叉编译工具链 |
| `rt-thread` | cv184x-v6.x | RT-Thread，含 **bsp/cvitek**（Duo 可运行 RT-Thread），另有 qemu-virt64-riscv |
| `linux_5.10` | develop / sg200x-dev / cv184x-v6.x | CV18xx BSP 内核 5.10（SDK V2 内核同源） |
| `u-boot-2021.10` | sg200x-dev | CV18xx BSP u-boot |
| `opensbi` | master / sg200x-dev | OpenSBI |
| `build`、`oss`、`ramdisk`、`fsbl`、`osdrv`、`middleware`、`cvi_mpi`、`isp_tuning`、`SensorSupportList`、`cvi_rtsp`、`tdl_sdk` | sg200x-dev / develop | **duo-buildroot-sdk-v2 的组件仓库镜像**（SDK V2 用 repo 聚合的同一批组件） |
| `buildroot-2021.05`、`buildroot` | master | buildroot 镜像 |

### 6.2 TPU / AI 能力（Duo 的 0.5/1 TOPS 用得到）
| 仓库 | 说明 |
| --- | --- |
| `cviruntime`（sg200x-dev） | TPU 运行时（cviruntime.h / bmruntime 接口、custom_op、python 绑定） |
| `cvikernel` | TPU 指令生成（kernel 层 “汇编器”） |
| `cvimath` | TPU 数学算子库 |
| `cvibuilder` | cvimodel 文件结构定义 |
| `flatbuffers`、`cnpy`（tpu 分支） | TPU SDK 依赖库 |
| `ive` | 智能视觉引擎（IVE 硬件加速） |
| `tdl_sdk`（cv184x-v6.x / master） | TDL 一站式深度学习 SDK（人脸/检测/分类…） |
| `libsophon` | 算能 AI 芯片驱动与运行时（面向 BM168x/SG 系列，可参考） |
| `tilelang-riscv-kubuds` | TileLang RISC-V 移植（与 Sophgo RISC-V AI 生态相关，非 Duo 专属） |

### 6.3 RTOS / 小核
`freertos`（sg200x-dev）、`FreeRTOS-Kernel`、`Lab-Project-FreeRTOS-POSIX`、`cvi_alios_open`（RTOS）、`osal`（OS 抽象层，cv184x-v6.x）。

### 6.4 工具链 / 周边
`llvm-project`（RISC-V 工具链）、`u-boot`（mainline 镜像）、`linux`（mainline 镜像）、`kubuds-qemu`（QEMU 镜像）、`isp-tool-daemon`（ISP 调试守护进程）、`kvmd`（PiKVM 类远程控制，可用于 Duo 实验）、`picoclaw`（Go AI 助手，支持 RISC-V）、`RV-EAI`（RISC-V 具身智能方案）。

### 6.5 与 Duo 无关
`A210-Melon-Pi-all-in-one`（A210 开发板）、`karsier-website`、`kubuds.github.io`、`kuloveinterns`、`flagcx-packaging`（FlagCX 打包）、`eigen` 镜像等。

---

## 7. 跨组织重复与冗余分析

同一份工作在四个组织里出现多份副本：

| 组件 | 副本 | 判定 |
| --- | --- | --- |
| Linux BSP 5.10.4 | `duosdk/linux@duosdk`、`kubuds/linux_5.10`、`milkv-duo/milkv-duo-linux`、V1/V2 SDK 内嵌 | 同源不同步；**以 duo-buildroot-sdk-v2 内嵌版为准**，其余为镜像/旧版 |
| Linux mainline 镜像 | `duosdk/linux`(6.7)、`kubuds/linux` | 无需保留，直接用 torvalds/linux |
| u-boot BSP 2021.10 | `duosdk/u-boot@duosdk`、`kubuds/u-boot-2021.10`、`milkv-duo/milkv-duo-u-boot`、SDK 内嵌 | 以 SDK V2 内嵌为准 |
| u-boot mainline + Duo 移植 | `duosdk/u-boot@duo-next`、`kubuds/u-boot`(main) | **duo-next 是唯一带 Duo 补丁的**（注意：mainline u-boot 后来已收 `board/sophgo/milkv_duo`） |
| buildroot | `duosdk/buildroot@duosdk`、`kubuds/buildroot(-2021.05)`、`milkv-duo/milkv-duo-buildroot`、SDK 内嵌 | 以 SDK V2 内嵌（2025.02）为准 |
| OpenSBI | `duosdk/opensbi`、`kubuds/opensbi`、`milkv-duo/milkv-duo-opensbi`、SDK 内嵌 | 以 SDK V2 内嵌为准 |
| TPU SDK | `kubuds/cvi*`、V2 SDK 内嵌 `cvi*`、`milkv-duo/tpu-sdk-*`、`cvitek-tdl-sdk-*` | **代码同源**；以 V2 SDK 内嵌 + `milkv-duo/tpu-mlir` 为准 |
| ISP 调参 | `duosdk/isp_tuning`、`kubuds/isp_tuning`、SDK 内嵌 | 以 SDK V2 内嵌为准 |
| QEMU | `duosdk/qemu@duo-qemu`、`kubuds/kubuds-qemu` | 仅 `duo-qemu` 含 Duo 机器模型 |
| pinmux | `milkv-duo/duo-pinmux`、`cvi-pinmux`、`milkv-duo-pinmux` | 用 **`duo-pinmux`**（覆盖三块板，最新） |
| Arduino | `milkv-duo/duo-arduino`（弃用）→ `kubuds/sophgo-arduino` | 用后者 |

---

## 8. 时间线与活跃度

- **2023-06 ~ 2024-05**：`duosdk` 各定制分支活跃期；`sophgocommunity/CV180-Duo` 资料定格。
- **2024 全年**：milkv-duo 示例/工具爆发（pinmux、wiringx、TDL 示例、yolo 部署）；文档 mainline/upstream-status 停更于 2024 年。
- **2025**：`duo-buildroot-sdk-v2` 成为主力（buildroot 升 2025.02，2025-12 仍在更新）；`milkv-duo/tdl-models`、`eigen` 等补库。
- **2026**：`kubuds` 侧活跃（`rproc-burn` 2026-10、`sophgo-arduino` 2026-10、`MilkV-Duo-all-in-one` 2026-11、`linux`/`u-boot`/`opensbi` 镜像刷新 2026-09）。

## 9. 数据附录（仓库清单统计）

- `duosdk`：9 仓库（9 fork / 0 原生），定制分支 5 条（linux:duosdk、u-boot:duosdk+duo-next、buildroot:duosdk、qemu:duo-qemu）。
- `milkv-duo`：38 仓库（原生 30 / fork 8），star 最高：`duo-buildroot-sdk` 495、`duo-files` 203、`duo-buildroot-sdk-v2` 154、`duo-examples` 159。
- `sophgocommunity`：5 仓库，Duo 相关 1 个。
- `kubuds`：49 仓库（原生 8 / fork 41），Duo 相关约 30 个（见 §6）。

> 数据采集自 GitHub API（2026-11-03），提交对比使用 GitHub compare 接口；文档口径核对自 milkv.io（overview 修订 2024-06、upstream-status 修订 2024-07）。
