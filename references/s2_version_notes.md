# IFRS S2 版本说明（Version Notes）

---

## 当前评估基准

- 标准：IFRS S2 Climate-related Disclosures (June 2023)
- 配套：IFRS S1 General Requirements for Sustainability-related Financial Disclosures (June 2023)
- 代码：`IFRS_S2_2023_base`

---

## 已发布修订（尚未纳入评估框架）

### 温室气体排放披露修订（Amendments to IFRS S2）

- 发布日期：2025 年 12 月
- 生效日期：2027 年 1 月 1 日起（允许提前采用）
- 主要变化：GHG 排放披露要求的技术修订
- 框架影响：预计影响 ID-059 至 ID-067（§29(a) 相关条款）的评估标准
- 代码：`IFRS_S2_2025_GHG_amendments`
- 更新计划：待修订正式生效后更新评估框架

### 转型计划披露指南

- 发布日期：2025 年 6 月
- 性质：指南（非强制要求）
- 主要内容：补充 §14 转型计划披露的最佳实践指引
- 框架影响：可作为 §14 相关条款（ID-015 至 ID-021）的评分参考，但不改变评分标准

---

## 辖区特定要求叠加（预留）

以下辖区要求可在未来版本中作为 overlay 叠加到 S2 基础评估之上：

| 辖区 | 规则 | 与 S2 关系 | 预留代码 |
|---|---|---|---|
| 香港 HKEX | 2025 年 1 月起强制气候披露（基于 ISSB） | 采纳 S2 并有本地化调整 | `HKEX_climate_2025` |
| 中国 A 股 | 三所可持续发展报告指引（2024 年） | 参考 ISSB 但有中国特色要求 | `A_share_ESG_2024` |
| 欧盟 CSRD/ESRS | ESRS E1 Climate Change | 与 S2 有互操作性但范围更广 | `ESRS_E1` |
| 美国 SEC | SEC Climate Disclosure Rule（2024 年发布，诉讼中） | 部分对齐 S2，范围较窄 | `SEC_climate_2024` |
| 澳大利亚 AASB | AASB S2 (2024) | 直接采纳 ISSB S2 | `AASB_S2_2024` |
| 日本 SSBJ | SSBJ 气候披露标准（征求意见中） | 基于 ISSB 框架本地化 | `SSBJ_climate` |

辖区叠加的使用方式：评估基础仍为 S2 2023 base，辖区要求在合规大表之后作为补充附录呈现，标注"辖区额外要求"和"是否满足"。

---

## 更新规则

1. 评估框架以 `IFRS_S2_2023_base` 为默认版本，除非被评估企业明确声称按更新版本编制
2. 如企业声称"提前采用 2025 修订"，在报告概要中标注，但评估标准仍以企业声称采用的版本为准
3. 辖区叠加仅在用户明确要求时启用（如"请额外检查 HKEX 要求"）
4. 版本更新时，96 条 ID 编号保持稳定——新增条款使用 ID-097 起的编号，删除的条款标记为 deprecated 但不重新编号
