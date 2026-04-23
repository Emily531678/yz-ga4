# Phase 2：GA4 Measurement Plan（1 页）

## Web/App Property

- 网站名称：扬州六大著名景点（投票互动网页）
- Public Live URL：https://emily531678.github.io/yz-ga4/
- 平台：Web（静态站点）

## Business Objective（业务目标）

提升用户参与度，并提高“完成投票”的人数（让更多访问者从浏览 → 选择 → 成功提交投票）。

## KPIs（2–3 个，可衡量）

1. 投票完成数（Primary KPI）
   - 指标：`vote_submit` 事件数量
   - 目标示例：较基期提升 10%（由你在 Phase 3 的报告里写具体数字）

2. 投票漏斗转化率（行为转化 KPI）
   - 指标：从 `vote_option_select` → `vote_submit` 的转化率
   - 计算：`vote_submit` / `vote_option_select`

3. 结果查看度（参与度 KPI）
   - 指标：`vote_results_view` 事件数量，或 `vote_results_view` / `vote_page_view`

## Measurement Strategy（如何用 GA4 衡量）

- 事件追踪（已在网站实现）
  - `vote_page_view`：页面访问（用于漏斗第一步）
  - `vote_option_select`：选择景点（用于漏斗中间步）
  - `vote_submit`：提交投票（用于目标达成）
  - `vote_results_view`：查看结果（用于参与度）
- 用户属性（已在网站实现）
  - `voter_status`：`not_voted` / `voted`（用于分群与对比）

## Notes（给老师看的要点）

- Custom Event（Events Interface 创建）建议：在 GA4 后台把 `vote_submit` 派生为 `vote_submit_custom`（满足 Phase 1“用界面创建 1 个 Custom Event”要求）。
