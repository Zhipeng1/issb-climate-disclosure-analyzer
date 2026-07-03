---
name: issb-climate-disclosure-analyzer
description: "IFRS S2气候披露分析与投资有用性评估工具。触发场景：用户上传ESG报告/可持续发展报告/TCFD报告/气候报告，或提及ISSB/IFRS S2/气候披露/TCFD合规/气候信息投资价值/披露质量评估等话题时触发。即使用户未明确提及'ISSB'，但涉及气候披露分析、ESG报告评估、气候风险识别、情景分析质量等话题时也应触发。"
---

# ISSB 气候披露分析与投资有用性评估

## 核心定位

本 Skill 面向两类用户：
- 企业 IR/可持续发展团队：逐条对照 IFRS S2 找到披露差距，给出改进建议（含最佳实践参考）
- 投资者/分析师：评估气候披露中哪些信息对更新财务模型真正有用

关键原则：
- 合规评估严格不降标。S2 要求"金额和百分比"的（如 §29(b)-(d)），定性描述不算满足
- 投资有用性判定回归三个财务出口（现金流/融资可得性/资本成本），不做 ESG 打分
- §29(f) 内部碳价：严格区分"情景分析引用外部碳价"和"自身决策嵌入碳定价"
- §19-21 定量豁免是系统性封顶——遇到时必须显性标注
- 诊断报告中不提具体比较对象企业名称；改进建议列可引用标杆做法但不点名对比
- 禁止循环标杆：被评估公司在标杆库中时，自动排除同公司案例

## 版本与依据

评估依据：IFRS S2 Climate-related Disclosures (June 2023) + IFRS S1 General Requirements
默认版本代码：`IFRS_S2_2023_base`
版本演进详见 `references/s2_version_notes.md`

## 核心引用规则

运行时必须严格参照以下文件：

| 文件 | 作用 | 何时加载 |
|---|---|---|
| `references/s2_evaluation_framework.md` | 96 条评估清单（ID-001 至 ID-096）。评分判定必须依据此文件 | Step 1 必读 |
| `references/best_practices.md` | 标杆库（12 家企业）。"差距/改进建议"列引用此文件 | Step 1 必读 |
| `references/scoring_edge_cases.md` | 12 条评分误判规则。Step 3 评分时逐条核验 | Step 3 必读 |
| `references/evidence_schema.md` | evidence_status / disclosure_type / standard_version 定义 | Step 2 参考 |
| `references/s2_version_notes.md` | S2 版本说明和辖区叠加预留 | 按需 |
| `references/jurisdiction_overlays.md` | 辖区叠加落地规则（HKEX/A股，含宽减识别） | 用户要求辖区检查时，或报告援引宽减时 |
| `references/sectors/sector_*.md` | 行业模块（6 个行业）| Step 2 按行业加载 |
| `examples/diagnostic_example_full.md` | 完整分析报告样例 | Step 3 对照 |
| `examples/diagnostic_example_short.md` | 简版报告模板（用户要求快速评估时）| 按需 |
| `evals/self-check.md` | 产出质量自检清单 | Step 4 必读 |
| `evals/clause_count_test.md` | 条款计数验证 | Step 4 自动运行 |
| `outputs/scorecard_schema.json` | 结构化输出模板 | 按需（批量测试时）|

## 文件目录

```
issb-climate-disclosure-analyzer/
├── SKILL.md                                    # 核心工作流程
├── README.md                                   # 说明文件
├── references/
│   ├── s2_evaluation_framework.md             # S2 全部 96 子款（ID-001至ID-096）
│   ├── best_practices.md                      # 标杆库（12家企业）
│   ├── scoring_edge_cases.md                  # 评分边界案例（12条规则）
│   ├── evidence_schema.md                     # 证据/披露/版本分类定义
│   ├── s2_version_notes.md                    # S2版本与辖区叠加
│   ├── jurisdiction_overlays.md               # 辖区叠加落地（HKEX/A股）
│   └── sectors/
│       ├── sector_mining_metals.md            # 矿业与金属
│       ├── sector_financial_institutions.md   # 金融机构
│       ├── sector_power_utilities.md          # 电力与公用事业
│       ├── sector_oil_gas_chemicals.md        # 油气与化工
│       ├── sector_cloud_ai_data_centers.md    # 云/AI/数据中心
│       └── sector_consumer_goods_agri_food.md # 消费品/食品/农业
├── examples/
│   ├── diagnostic_example_full.md             # 完整报告样例（96条+ID列）
│   └── diagnostic_example_short.md            # 简版报告模板
├── evals/
│   ├── self-check.md                          # 产出质量自检清单
│   └── clause_count_test.md                   # 条款计数验证
└── outputs/
    └── scorecard_schema.json                  # 结构化输出 JSON 模板
```

## 评分标准

评分分四类，因为 S2 条款性质不同（详见 `evidence_schema.md` §四）：

**定量型条款**（§29(a)-(g) 指标数据、§16(a)-(d) 财务影响金额）：
- ● 给出 S2 要求口径的数值/金额/百分比
- ◐ 有相关描述但未量化，或使用替代量化（标注 proxy_metric）
- ○ 未披露或极弱

**流程/治理型条款**（§6 治理、§25 风管、§22(b) 过程参数、§33-34 过程要求）：
- ● 有具体证据（汇报频率、技能矩阵、委员会议程、流程图、排序方法）
- ◐ 泛泛描述（"已考虑""定期汇报""已整合"但无证据）
- ○ 未提及或仅有样板语言

**战略/韧性型条款**（§10 风险识别、§13 业务影响、§14 转型计划、§22(a) 韧性结论）：
- ● 有结构化识别结果且触及财务传导路径
- ◐ 有识别但未建立财务传导逻辑
- ○ 未识别或仅有样板语言

**目标与进展型条款**（§33 目标参数、§35 进展、§36 技术参数）：
- ● 有目标值 + 基年 + 时间范围 + 逐期追踪
- ◐ 有目标但缺少部分要素
- ○ 未设定目标或仅有模糊表述

## 工作流程

### Step 0：用户引导与材料确认

当 Skill 被触发且用户尚未上传报告或明确公司时，先对齐再动手。已有报告则跳到 Step 1。

0a. 说明能力：按 IFRS S2 逐条评估气候披露完整度 + 从投资者视角评估决策有用性。

0b. 引导材料：
- 最佳方案：上传最新 ESG 报告/可持续发展报告（如有独立 TCFD/气候报告更好）
- 可接受方案：仅上传年报，从中提取气候相关内容
- 无报告方案：提供公司名称，尝试搜索公开报告

0c. 确认公司名称和报告年度。

### Step 1：加载评估框架

读取以下文件：
1. `references/s2_evaluation_framework.md`——96 条评估清单
2. `references/best_practices.md`——标杆库
3. `references/scoring_edge_cases.md`——评分边界规则

根据被评估公司的行业，加载对应行业模块：
- 矿业 → `references/sectors/sector_mining_metals.md`
- 银行/保险/资管 → `references/sectors/sector_financial_institutions.md`
- 电力/公用事业 → `references/sectors/sector_power_utilities.md`
- 油气/化工 → `references/sectors/sector_oil_gas_chemicals.md`
- 互联网/云/AI/数据中心 → `references/sectors/sector_cloud_ai_data_centers.md`
- 消费品/食品/农业 → `references/sectors/sector_consumer_goods_agri_food.md`

如被评估公司在标杆库中（BHP/CLP/台达/施耐德/紫金/环旭/隆基/宁德/阳光/Microsoft/Unilever/DBS），标记"禁止循环标杆"——改进建议列排除同公司案例。

### Step 2：提取报告中的气候内容

首先判断报告类型（disclosure_type）：
- `ISSB_S2`：明确按 IFRS S2 编制，有 S2 索引
- `TCFD`：按 TCFD 四支柱组织，有 TCFD 索引
- `ESG_report`：综合 ESG 报告，气候是其中一章
- `climate_action_plan`：独立气候/转型计划文件
- `annual_report_integrated`：气候信息分散在年报各章节

系统性提取映射到 S2 四大支柱的内容：
- 治理（§6）：董事会/委员会气候监督职责、技能、信息频率、战略考量、薪酬挂钩、管理层角色
- 战略（§10-22）：风险/机遇清单、时间范围、业务模式影响、集中位置、转型计划（含资源配置）、财务影响、情景分析
- 风险管理（§25）：风险识别/评估/排序/监控流程、机遇流程、与整体风管整合
- 指标与目标（§29, §33-37）：GHG Scope 1/2/3、跨行业指标、目标与进展

提取时标注 evidence_status（current_practice / historical_result / future_commitment / proxy_metric / external_scenario_assumption / not_disclosed）。

### Step 3：产出报告

严格按照 `examples/diagnostic_example_full.md` 的结构生成，包含：

**一、报告概要表**
- 含 disclosure_type 和 standard_version

**二、合规评估摘要**（前置于大表之前）
- ●/◐/○/不适用各多少条（总数为 96 条，含百分比）
- 亮点（分条列出）
- 主要缺口（分条列出，标注条款 ID）
- 报告可读性与可检索性加分项（S2 索引/TCFD 索引等，不计入 96 条评分）
- 红旗事项（如有，见下方红旗机制）

**三、S2 逐条合规评估（完整 96 条大表）**
- 列：**ID | 条款 | 要求简述 | 评分 | 企业实际披露 | 证据页码 | 差距/改进建议**
- 按四大支柱分组，每组前有总领段
- 全部子款独立成行，与 s2_evaluation_framework 的 ID-001 至 ID-096 严格对齐
- "企业实际披露"列写详细并标注 evidence_status
- "差距/改进建议"列：每条 ◐ 或 ○ 都必须有具体改进方向；引用 best_practices 和行业模块中的做法（不点名）

评分时逐条核验 scoring_edge_cases 的 12 条规则。

**四、投资有用性评估（含转型计划综合评估子模块）**
- 覆盖 12 个投资模型变量
- 转型计划综合评估（7 个维度，引用合规大表中的条款 ID 和评分）
- 核心发现（气候风险方向、最有用的披露、信息缺口）

**五、关键结论**（一段话）

### 12 个投资模型变量

| # | 变量 | 说明 |
|---|---|---|
| 1 | 收入增速 | 气候机遇对应的产品/区域/客户/订单 |
| 2 | 毛利率/COGS | 碳成本/供应链碳/低碳采购溢价/材料碳足迹 |
| 3 | 市场准入 | 产品碳足迹/CBAM/低碳招标/法规阈值 |
| 4 | 资本开支 | 转型投资/低碳改造/脱碳产能 |
| 5 | 费用率 | 认证/碳管理/合规/供应链审计 |
| 6 | 营运资本 | 海外项目周期/供应商改造/客户验收 |
| 7 | WACC/资本成本 | 绿色融资/greenium |
| 8 | 终值增长 | 情景分析/气候韧性/长期产品适配 |
| 9 | 风险折价 | 物理/转型/供应链/目标偏离 |
| 10 | 管理层质量 | 治理/激励对齐/兑现记录/披露成熟度 |
| 11 | 资产减值/搁浅 | 气候相关减值测试/搁浅风险 |
| 12 | 税率/税收政策 | 碳税对有效税率的影响/绿色税收优惠 |

### 转型计划综合评估（7 个维度）

在投资有用性章节内，对分散在 S2 各条款中的转型计划要素做投资者视角整合（synthesized view），每个维度一句话判断 + 引用对应条款 ID 和评分：

| 维度 | 对应 S2 条款 | 评估问题 |
|---|---|---|
| 目标科学性 | §33-34, SBTi | 目标是否经第三方验证、是否对齐 1.5°C 路径 |
| 行动路径具体性 | §14(a)(i-v) | 从目标到行动的具体路径，还是只有终态描述 |
| 资源配置量化度 | §14(b), §29(e) | 转型计划有没有预算支撑（金额、时间表） |
| 关键依存条件 | §14(a)(iv) | 路径依赖哪些外部条件，依赖度多高 |
| 治理问责 | §6(a)(v), §29(g) | 管理层有没有经济激励执行转型计划 |
| 进展可追踪性 | §35, §14(c) | 是否有逐年 tracking、偏差分析、里程碑对照 |
| 碳信用依赖 | §36(e) | 净零目标多大程度依赖碳信用 vs 自身减排 |

有用性分三级：
- 预测性增量：提供市场/卖方尚未纳入的新信息，能更新因子取值
- 确认性：确认或证伪已有假设，更新把握而非数值
- 样板/无用：不触及财务出口

### 红旗机制

以下情况在报告中单独标注为"红旗事项"：
- Scope 3 未披露但价值链排放重大（如消费品/金融/油气行业）
- 有净零目标但无资本配置（§14(b) ○ 且 §29(e) ○ 且 §33(b) ●）
- 情景分析无财务量化（§22(b) 有过程参数但 §22(a) 全部 ○）
- 声称转型计划但未拨付任何资源
- 碳信用依赖程度不透明且净零目标激进

### Step 4：产出自检

输出前逐项确认 `evals/self-check.md` 中的清单，并运行 `evals/clause_count_test.md` 中的验证。

## 行业模块使用规则

行业模块每个只回答五件事：
1. 本行业最重要的气候风险/机遇
2. 最容易触发的 S2 条款
3. 最关键的投资有用指标
4. 常见误判
5. 推荐 best-practice 做法类型

使用时机：
- Step 1 加载时按行业选择对应模块
- Step 3 评分时检查行业模块中的"常见误判"
- Step 3 改进建议时引用行业模块中的"推荐做法"
- 投资有用性评估时参考"最关键的投资有用指标"

可用行业模块：

| 行业 | 模块文件 |
|---|---|
| 矿业与金属 | `sectors/sector_mining_metals.md` |
| 金融机构（银行/保险/资管）| `sectors/sector_financial_institutions.md` |
| 电力与公用事业 | `sectors/sector_power_utilities.md` |
| 油气与化工 | `sectors/sector_oil_gas_chemicals.md` |
| 互联网/云/AI/数据中心 | `sectors/sector_cloud_ai_data_centers.md` |
| 消费品/食品/农业 | `sectors/sector_consumer_goods_agri_food.md` |

未覆盖行业使用通用框架评估，参考 SKILL.md 底部的"通用行业注意事项"。

## 通用行业注意事项

### 新能源制造商（光伏/储能/电池）
- 气候风险方向通常不是碳税（Scope 1+2 极小），而是需求节奏 + 供应链碳 + 产品碳足迹准入
- §13(b) 的材料级 Scope 3 集中度是投资者最关心的颗粒度
- 产品碳足迹法规（欧盟电池法规/法国 CRE/ESPR）是一阶准入约束

### 高碳行业（钢铁/水泥）
- 碳成本是一阶：Scope 1+2 × 碳价直接进 COGS
- §29(b) 转型风险敞口% 和 §29(e) 气候 Capex 是最直接的估值输入
- 资产减值/搁浅是核心风险 → §16(b) 特别重要

### 交通运输/航运/物流
- 燃料结构（重油/LNG/SAF/甲醇/氢）决定转型路径
- 排放强度（gCO2e/ton-km）是行业标准指标
- 资产寿命长（船舶 25 年+），锁定效应强
- 碳价法规（EU ETS/FuelEU Maritime/CORSIA）直接影响成本

### 房地产/建筑
- 建筑运营排放（能耗/供暖/制冷）和隐含碳（水泥/钢材/玻璃/铝）
- 物理风险（洪水/热浪/海平面上升）直接影响资产估值
- 建筑能效法规和绿色建筑认证是准入约束
