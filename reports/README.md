# Milk-V Duo 系列调研与升级报告集

本目录是 `karen-mimo-survey` 分支新增的报告集，回答两个问题：
**“现在生态是什么状态？”** 与 **“新玩家/厂商该从哪里入手、哪些仓库不用看了？”**

| 文件 | 内容 | 适合谁 |
| --- | --- | --- |
| [01-current-status-survey.md](01-current-status-survey.md) | 现状报告：`duosdk` / `milkv-duo` / `sophgocommunity` / `kubuds` 四个组织 101 个仓库逐个摸底，含 fork 关系、定制分支、重复与冗余分析 | 想知道“都有什么”的人 |
| [02-sota-repo-analysis.md](02-sota-repo-analysis.md) | State-of-the-Art 仓库分析：以官方 milkv.io overview（2024-06 版）为底稿核对更新到 2026-11；内核选型（5.10.4 BSP vs 6.18 LTS vs 7.4-rc1）、mainline 支持实测、TPU 全图、CVE 现状、三条入门路径、仓库评级（✅ 主力 / 🟡 参考 / ❌ 不用看） | **刚买板子的开发者与厂商（先读这份）** |
| [03-upgrade-plan.md](03-upgrade-plan.md) | 系统升级计划与执行记录：Arm → RISC-V → TPU → RT-Thread 的升级路线、步骤与产出物索引 | 要跟着做升级的人 |

生成信息：2026-11-03 · Karen KUBUDS AI Coders \<kubuds@kubuds.cn\> · Co-authored-by: Mimo-v2.6-Pro + Pi Agent
数据来源：GitHub API / compare 接口、kernel.org releases.json、milkv.io 官方文档、torvalds/linux v6.18 与 u-boot master 仓库实测核对。
