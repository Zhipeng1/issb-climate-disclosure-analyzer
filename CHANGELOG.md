# CHANGELOG — v2（以原仓库完整文件为基底的定点增量版）

## ⚠ 首要事项：LICENSE

本包不含 LICENSE 文件。GitHub 仓库（Zhipeng1/issb-climate-disclosure-analyzer）未被搜索引擎收录、无法在本次环境中抓取，为避免拷入错误的许可条款，此处留空。**合并时请将仓库中现有 LICENSE 原样拷入本目录**，即得到完整分发包。

## 一、基底说明

本包以用户提供的原始压缩包（18 个文件）为基底，**全部原文件逐字保留**，仅做下述定点增量。此前一版重建包（v2-full）因基于中转截断的文本重建，请废弃不用；特别地，该版把 §19–21 定量豁免条款的引用"纠正"为 §18–20——经 IFRS S2 原文核实（¶21 "applying the criteria set out in paragraphs 19–20"），**原版引用 §19(a)/(b)、§20、§21(a)/(b)/(c) 是正确的**，重建版反而有误。原版 96 条框架、SKILL 工作流、评分规则、标杆库、红旗机制、自检清单均维持原样。

## 二、本版新增/修改清单

| 文件 | 变更类型 | 内容 |
|---|---|---|
| references/jurisdiction_overlays.md | 新增 | 将 s2_version_notes 预留的辖区叠加落地为可执行规则：HKEX（Part D 节奏、financial effects relief 处理方式、AFRC 鉴证分阶段预期：强制报告第三个财年起 Scope 1/2 有限保证、第五个财年起其余全部，HKSSA 5000）；A 股（双重重要性口径、首个报告期宽限、CCER/履约映射、AA1000 与 ISAE 3000 实践）；2025 GHG 修订的中性处理。使用规则与原版一致：辖区附录按需启用，宽减识别始终生效 |
| references/evidence_schema.md | 定点插入 | 第一节新增 `relief_applied` 证据状态（含使用示例）：区分"准则允许的空白"与"能力/意愿缺口"，评分仍为 ○，缺口分析中单列。其余原文未动 |
| references/s2_version_notes.md | 加一段 | 指向 jurisdiction_overlays.md 的落地说明，预留表原样保留 |
| SKILL.md | 加两行 | 核心引用规则表与文件目录树各加 jurisdiction_overlays.md 一行，其余原文未动 |
| references/sectors/sector_power_utilities.md | 追加 | 第一节加"制度前提"（受规管 vs 市场化须前置判断、分部评估）；第四节追加 6 条经 CLP 2025 报告集验证的误判（显性碳价敞口≠全部转型风险、容量百分比≠资产金额、避免排放≠自身减排、关闭拨备≠政策突变、受规管≠无风险等）；第五节追加 2 条 best practice（气候融资逐笔披露+鉴证、物理风险分灾种量化，来源 CLP）。原有内容未删改 |
| CHANGELOG.md | 新增 | 本文件 |

## 三、后续可选事项

1. 将本版电力模块新增的误判条目回灌 diagnostic_example（如需示例覆盖）。
2. scoring_edge_cases.md 12 条规则与本版新增误判无冲突，如愿收敛可把"容量百分比≠资产金额"上升为通用规则第 13 条（它在电力、矿业两个模块中均出现）。
3. 待 2025 GHG 修订正式生效（2027-01-01）后，按 s2_version_notes 的更新规则调整 ID-059 至 ID-067 评估标准；ID 编号保持稳定。
