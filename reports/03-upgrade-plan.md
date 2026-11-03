# Milk-V Duo 系列系统升级计划（2026-11）

> 依据 [01-current-status-survey.md](01-current-status-survey.md)（去重、去陈旧后的现状）与 [02-sota-repo-analysis.md](02-sota-repo-analysis.md)（SOTA 选型）制定。
> 执行顺序：**先 Arm → 再 RISC-V → 再 TPU → 最后 RT-Thread**（任务指定顺序）。
> 执行工作区：`/home/kubuds/duosdk/duosdk-next/`（本计划所有产出物均入库该 repo 并按阶段提交）。

---

## 0. 输入清理结论（先做减法）

**保留（唯一权威源）**：
- SDK V2：`milkv-duo/duo-buildroot-sdk-v2`（buildroot 2025.02 + BSP 5.10.4 + TPU/多媒体栈）——升级对象；
- mainline：`torvalds/linux` v6.18（LTS）与 v7.4-rc1（HEAD）、`u-boot/u-boot` master、`opensbi/opensbi` master——升级目标基线；
- 工具：`milkv-duo/duo-pinmux`、`duo-wiringx`、`host-tools`、`kubuds/sophgo-arduino`、`kubuds/rproc-burn`；
- TPU：`milkv-duo/tpu-mlir`、`tdl-models` + SDK V2 内嵌 `cviruntime/cvikernel/cvimath/cvibuilder/ive/tdl_sdk`；
- RTOS：`kubuds/rt-thread`（bsp/cvitek）、`kubuds/freertos` 系。

**丢弃（重复或过时，不再投入）**：
- `duosdk` 组织：`linux`、`duo-buildroot-sdk`、`opensbi`、`zephyr`、`meta-riscv`、`buildroot`、`isp_tuning`（纯镜像/过时 BSP）；仅摘取 `u-boot@duo-next`（8 提交）与 `qemu@duo-qemu`（10 提交）的补丁集归档到本工作区供参考/移植；
- `milkv-duo`：V1 SDK 及 `milkv-duo-*` 拆分件（Duo 64M 专用）、`duo-sdk`、`duo-arduino`、`milkv-duo-pinmux`、`cvi-pinmux`、`tpu-sdk-cv180x`、`cvitek-tdl-sdk-cv180x`；
- `kubuds`：与 Duo 无关的 `A210-Melon-Pi-all-in-one`、`karsier-website`、`flagcx-packaging` 等。

---

## 1. 目标映射

| 任务目标 | 落点 |
| --- | --- |
| ① RISC-V 与 Arm 内核升到最新 LTS，并提供 HEAD 支持 | Phase 1（Arm）/ Phase 2（RISC-V）：LTS = **6.18.60**，HEAD = **7.4-rc1** |
| ② TPU 能力整合 + 好用的脚本/重写 | Phase 3：`duotpu` 工具套件（模型转换/部署/基准/小核烧写/IVE） |
| ③ Duo S / Duo 256 升级 + 已知 CVE 修复 | Phase 1/2 的内核升级即主要 CVE 修复面；另出 `docs/cve-status.md` + rootfs 加固项 |
| ④ 提交规范 | 作者 `Karen KUBUDS AI Coders <kubuds@kubuds.cn>`，每条提交加 `Co-authored-by: Mimo-v2.6-Pro + Pi Agent` |
| ⑤ 先分析去重、后制定计划、按 Arm→RISC-V→TPU 执行 | 本文件 §0 + 阶段顺序 |
| ⑥ RT-Thread 同步升级最新 | Phase 4：`kubuds/rt-thread`（bsp/cvitek）对齐上游 **v5.3.0** |

---

## 2. 阶段计划

### Phase 1 — Arm 主控内核升级（SG2000 / SG2002，AArch64 Cortex-A53）
1. 工作区骨架：`duosdk-next/`（docs/kernel/tpu/rtthread/tools）。
2. `kernel/fetch-kernel.sh`：拉取并校验 `linux-6.18.60.tar.xz`（LTS）与 `linux-7.4-rc1.tar.xz`（HEAD）。
3. DTS：以 mainline `sg2000.dtsi` + `sg2000-milkv-duo-module-01.dtsi` 为基，补两块板级 DTS：
   - `sg2000-milkv-duos.dts`（Duo S：eMMC/SD、AIC8800 SDIO Wi-Fi、DSI、双 CSI）；
   - `sg2002-milkv-duo256m.dts`（Duo 256M；含 sg2002 arm64 dtsi 补齐）。
4. defconfig：`milkv_duo_arm64_defconfig`（LTS/HEAD 各一份 fragment），从 BSP `cvitek_sg2000_*_defconfig` 提取必要项（AIC8800 可选模块、CMA、TPU 占位等）适配 mainline Kconfig。
5. 构建验证（容器 `ssh -p 2222`，Ubuntu 26.04 + `gcc-aarch64-linux-gnu`）：`make ARCH=arm64 defconfig && make ARCH=arm64 -j8 Image dtbs modules`（LTS 全量；HEAD 至少 defconfig + dtbs）。
6. CVE：6.18.60 相对 5.10.4 覆盖修复清单写入 `docs/cve-status.md`；BSP 增量（若暂留 5.10）列最小 backport 建议。
7. 产出物：configs/、dts/、patches/、构建日志、`docs/phase1-arm.md`。

**验收**：LTS 内核 arm64 Image + dtbs 构建成功；HEAD defconfig/dtbs 构建成功；DTS 无告警。

### Phase 2 — RISC-V 主控内核升级（CV1800B / SG2002 / SG2000，C906）
1. DTS：`sg2002-milkv-duo256m.dts`（riscv）、`sg2000-milkv-duos.dts`（riscv）——mainline 现只有 `cv1800b-milkv-duo.dts` 与 `sg2002-licheerv-nano-b.dts`，板级补齐是主要工作。
2. defconfig：`milkv_duo_riscv64_defconfig`（SMP C906×2，含 C906L 小核预留、remoteproc 选项）。
3. 构建验证：`make ARCH=riscv64 Image dtbs`（LTS 全量；HEAD 抽验）。
4. OpenSBI/u-boot：记录 mainline 版本建议（opensbi master、u-boot master 已支持 cv1800b-milkv-duo；duo-next 的 boot0/ethernet 提交与 upstream 差异比对归档）。
5. 产出物：configs/、dts/、`docs/phase2-riscv.md`。

**验收**：LTS riscv64 Image + dtbs 构建成功；与 Arm 侧配置差异有对照表。

### Phase 3 — TPU 能力整合
1. 盘点算能已释放能力：tpu-mlir（编译）、cvimodel 格式、cviruntime/cvikernel/cvimath/cvibuilder（运行时/自定义算子）、tdl_sdk（算法）、ive（图像硬件加速）、tdl-models（模型库）、rproc-burn（小核）。
2. 重写/新写 `duotpu` 脚本套件（bash/python，单文件可分发）：
   - `duotpu convert`：调 tpu-mlir Docker 一键转 cvimodel；
   - `duotpu deploy`：推送模型 + 依赖到板（scp）、生成运行命令；
   - `duotpu bench`：批量跑 `tdl_sdk`/`cviruntime` 示例并汇总 FPS/延迟；
   - `duotpu ive`：常用 IVE 硬件加速操作封装；
   - `duotpu smallcore`：对接 `kubuds/rproc-burn` 烧写 C906L/8051 固件。
3. 在容器内对 `cviruntime` 做编译冒烟（host x86 编译静态库或至少 CMake 配置通过）。
4. 产出物：`tpu/`、`docs/phase3-tpu.md`。

**验收**：脚本 `--help`/dry-run 全通；cviruntime 编译或配置验证有日志。

### Phase 4 — RT-Thread 同步升级
1. `kubuds/rt-thread`（cv184x-v6.x，含 bsp/cvitek）对齐上游 `RT-Thread/rt-thread` **v5.3.0**（当前最新 tag）。
2. 工具：`rtthread/upgrade-rtt.sh`（取上游 tag、生成 bsp/cvitek 补丁队列、冲突清单）。
3. 产出物：`rtthread/`、`docs/phase4-rtthread.md`。

**验收**：脚本执行产出补丁队列与升级说明；bsp/cvitek 在 v5.3.0 上可 scons 配置（有日志）。

---

## 3. 工作区布局

```
duosdk-next/
├── README.md               # 总览 + 快速上手
├── docs/                   # 计划、阶段报告、CVE 清单
├── kernel/
│   ├── fetch-kernel.sh     # 下载/校验 6.18.60 LTS、7.4-rc1 HEAD
│   ├── build.sh            # build.sh <arm64|riscv64> <lts|head> [targets...]
│   ├── configs/            # defconfig / config fragment（LTS 与 HEAD 分开）
│   ├── dts/                # duo256m / duos 板级 DTS（arm64 + riscv64）
│   └── patches/            # 补丁队列（含 CVE backport）
├── tpu/                    # duotpu 脚本套件
├── rtthread/               # RT-Thread 升级工具与 bsp 补丁
└── tools/                  # 杂项（归档 duosdk@duo-qemu / duo-next 提交清单等）
```

## 4. 风险与已知限制

1. **TPU 驱动不在 mainline**：6.18/7.4 内核暂无 `/dev/cvi-tpu`；TPU 功能短期只能跑在 BSP 5.10 内核上。计划在 `docs/phase3-tpu.md` 记录 `osdrv/interdrv/tpu` 的移植要点（依赖 DMA/fb/clk API 差异），不在本期完成移植。
2. **AIC8800 Wi-Fi 无 mainline 驱动**：Duo S 无线功能在 mainline 内核下暂不可用；DTS 预留 SDIO 节点 + 外部模块构建说明。
3. **ISP/MMF/编解码闭源或半闭源**：`cvi_mpi`/`middleware` 用户态库依赖 BSP 驱动，mainline 下仅能跑纯计算/网络/存储负载。
4. **Duo 64M（CV1800B）EOL**：不在升级范围（mainline 已有 `cv1800b-milkv-duo.dts`，可自便）。
5. **构建资源**：容器 8 核，LTS 全量构建约 20~40 分钟/架构；HEAD 只做配置与 dtbs 抽验。
