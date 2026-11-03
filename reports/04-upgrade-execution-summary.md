# 系统升级执行总结（2026-11-03）

> 对应计划 [03-upgrade-plan.md](03-upgrade-plan.md)。执行工作区：`/home/kubuds/duosdk/duosdk-next/`（含全部脚本、DTS、配置、日志）。
> 执行顺序：分析去重 → 计划 → **Arm → RISC-V → TPU → RT-Thread**。构建环境：Ubuntu 26.04 容器（8 核）+ gcc-aarch64/riscv64-linux-gnu。

## 1. 结果一览

| 阶段 | 目标 | 结果 |
| --- | --- | --- |
| Phase 1 Arm | 5.10.4 → **6.18.60 LTS** + **7.4-rc1 HEAD** | ✅ LTS：Image(41.7MB)+dtbs+1414 模块；HEAD：dtbs 冒烟；两块板 DTB 零告警 |
| Phase 2 RISC-V | 同上 | ✅ LTS：Image(27.4MB)+dtbs+模块；HEAD：dtbs 冒烟 |
| Phase 3 TPU | 整合算能全部已释放能力 | ✅ `duotpu` 七子命令（convert/deploy/bench/ive/smallcore/models/info），dry-run 冒烟全通 |
| Phase 4 RT-Thread | 升级到最新（v5.3.0） | ✅ 上游 v5.3.0 已内建 bsp/cvitek（riscv + aarch64 双核）；fork 差异分析 + scons 冒烟完成 |
| CVE | Duo S / Duo 256M 已知漏洞 | ✅ `docs/cve-status.md`（代表 CVE 清单 + rootfs/启动链加固清单） |

## 2. 内核升级要点（核心交付）

- **LTS = 6.18.60**（推荐产品基线）：Duo S（SG2000）与 Duo 256M（SG2002）的 Arm（A53）与 RISC-V（C906）四条内核线全部构建通过；
  本工程补齐 mainline 6.18 缺失的 4 个板级 DTS + 1 个 arm64 `sg2002.dtsi` shim。
- **HEAD = 7.4-rc1**：实测发现 **上游已收录 Duo S（arm64+riscv）与 Duo 256M（riscv + `-eth` overlay）板级 DTS**；
  唯一剩余板级缺口 = **Duo 256M arm64**，由本工程补齐（可直接提交上游）。
  `build.sh` 实现“上游优先”DTS 注入（同名文件用 mainline 的，只补缺口），LTS/HEAD 行为一致。
- 安全：5.10.4 → 6.18.60 一次性吸收 5 年多 stable 修复（Dirty Pipe / nf_tables / io_uring 等，详见 docs/cve-status.md）。

## 3. 交付物索引（duosdk-next 仓库）

```
kernel/fetch-kernel.sh        6.18.60 / 7.4-rc1 下载 + SHA256 pin
kernel/build.sh               build.sh <arm64|riscv64> <lts|head>（DTS/补丁注入，上游优先）
kernel/dts/{arm64,riscv64}/   Duo S / Duo 256M 板级 DTS + arm64 sg2002.dtsi shim
kernel/configs/               sophgo 平台配置片段（×4）+ 安全基线
tpu/duotpu                    TPU 一站式工具（7 子命令）
rtthread/upgrade-rtt.sh       RT-Thread v5.3.0 对齐工具 + bsp/cvitek 差异报告
docs/phase1..4-*.md           各阶段执行报告
docs/cve-status.md            CVE 与加固清单
docs/logs/                    构建日志（arm64/riscv64 LTS、HEAD、RT-Thread scons）
tools/README.md               duosdk@duo-qemu / duo-next 存档说明
```

## 4. 已知限制与后续

1. TPU/IVE/媒体驱动仍只在 BSP 5.10（mainline 无 `/dev/cvi-*`）；移植要点已写入 docs/phase3-tpu.md（预计 2~3 周驱动工作）。
2. AIC8800 Wi-Fi 驱动/固件未 upstream；DTS 已预留 SDIO 节点。
3. RT-Thread 完整构建需 `milkv-duo/host-tools` 的 `riscv64-unknown-linux-musl-gcc`（容器网络受限未取到）；scons 配置与编译启动已验证。
4. 建议把本工程的 Duo 256M arm64 DTS 提交上游（补 mainline 最后一个板级缺口），把 riscv/duo-s 相关 DTS 同步到 u-boot。
