# IT114116 / ITP4827 Web Analytics（GA4 项目总报告）

## 0. 项目概览

- 学校/课程：Hong Kong Institute of Information Technology — IT114116 / ITP4827 Web Analytics
- 项目主题：Digital Growth: Using GA4 to Improve 扬州六大著名景点（投票互动网页） Performance
- 网站名称：扬州六大著名景点（投票互动网页）
- Public Live URL：https://emily531678.github.io/yz-ga4/
- 技术形态：纯静态网页（HTML/CSS/原生 JS）+ GA4（gtag.js）
- GA4 Measurement ID：G-T39YW06F1C

## 1. Phase 1：GA4 Implementation & Tracking（实现与追踪）

### 1.1 安装与配置（Technical Accuracy）

- 已在网站 `<head>` 中安装 GA4 tracking code（gtag.js）
- 网站可在 GA4 Realtime 中捕获访问与事件
- 支持调试参数：在 URL 末尾加 `?debug=1`（用于在浏览器控制台输出事件触发信息，便于验证）

### 1.2 事件追踪（网站端已实现）

网站已实现投票流程相关事件（用于后续 KPI 与 Exploration）：

- `vote_page_view`：页面加载完成后触发（用于漏斗第一步）
  - 参数：`voter_status`（`voted` / `not_voted`）
- `vote_option_select`：用户点击并选择景点时触发
  - 参数：`place`
- `vote_submit`：用户点击“投我一票”并提交成功时触发（核心目标事件）
  - 参数：`place`、`total_votes`
- `vote_results_view`：投票结果展示/刷新时触发（参与度事件）
  - 参数：`total_votes`、`selected_place`、`voter_status`
- `image_load_error`：图片加载失败时触发（质量监控事件）
  - 参数：`alt`、`src`

### 1.3 自定义事件（GA4 Events Interface 创建）

为满足课程要求“Use the GA4 Events Interface to create one GA4 Custom Event”，在 GA4 后台通过 **Create events** 创建 1 个自定义事件规则：

- Custom event name：`vote_submit_custom`
- Matching condition：
  - `event_name` equals `vote_submit`
- Copy parameters from source event：开启（复制 `place`、`total_votes` 等参数）

该自定义事件用于在报告中作为“额外设置的自定义事件”展示，并可作为 Phase 3 的量化目标（例如提升 10%）。

### 1.4 Phase 1 交付物（Deliverables）

- Public Live URL：https://emily531678.github.io/yz-ga4/
- Realtime 截图（需在你本机操作后保存截图）：
  1. 打开网站：`https://emily531678.github.io/yz-ga4/?debug=1`
  2. 完成一次投票动作：选择景点 → 点击“投我一票”
  3. 打开 GA4：Reports → Realtime，截图能看到自己的访问/事件（建议能看到 `vote_submit` 或 `vote_submit_custom`）

## 2. Phase 2：Business Objective & KPIs Definition（Measurement Plan）

### 2.1 Business Objective（业务目标）

提升用户参与度，并提高“完成投票”的人数，让更多访问者从浏览 → 选择 → 成功提交投票。

### 2.2 KPIs（2–3 个可衡量指标）

1. Primary KPI：投票完成数
   - 定义：`vote_submit` 事件数量（或 `vote_submit_custom` 事件数量）
2. 漏斗转化率（行为 KPI）
   - 定义：从 `vote_option_select` → `vote_submit` 的转化率
   - 计算：`vote_submit` / `vote_option_select`
3. 结果查看度（参与度 KPI）
   - 定义：`vote_results_view` 数量，或 `vote_results_view` / `vote_page_view`

### 2.3 Phase 2 交付物（Deliverable）

- 1 页 Measurement Plan：见项目文件 `Phase2_MeasurementPlan_1页.md`

## 3. Phase 3：Insights, Analysis and Exploration（洞察与优化）

### 3.1 使用的 Exploration 工具

- 工具：GA4 Funnel exploration（漏斗探索）
- 目标：找出投票流程中流失最大的步骤，并提出可执行的优化方案，推动核心目标（投票完成数）提升

### 3.2 漏斗定义（与业务目标对齐）

漏斗 Steps（Events）：

1. `vote_page_view`（进入/加载投票页）
2. `vote_option_select`（选择景点）
3. `vote_submit`（提交投票）

Breakdown（分群对比）：

- `Device category`（desktop vs mobile），用于识别不同设备上的流失差异

### 3.3 分析结果（示例写法，按你的截图数字填写）

以下为你当前探索截图中呈现的结构化结论写法（将数字替换为你 GA4 当下数据即可）：

- Step 1 `vote_page_view`：6
- Step 2 `vote_option_select`：4（Step1→Step2 转化率：66.67%，流失：33.33%）
- Step 3 `vote_submit`：4（Step2→Step3 转化率：100%）

**问题定位：**

- 主要流失发生在 Step1→Step2（用户进入页面后没有选择景点）
- Step2→Step3 转化率较高，说明“已选择的用户通常会完成投票”，页面提交步骤阻力较小

### 3.4 优化方案（Fix a problem）

针对 Step1→Step2 流失（进入但不选择），提出以下可落地优化：

1. 强化投票区的“价值与引导”
   - 在投票区补充一句更明确的价值点：投票后可立即查看实时统计结果
   - 提升提示文案视觉权重（字号/颜色/位置），让用户更快理解下一步动作是“点选一个景点”

2. 降低“开始选择”的心理成本
   - 增加“推荐/热门”提示（例如默认高亮一个选项或提示“点击任意景点即可投票”）
   - 优化移动端首屏：确保投票区在首屏可见，减少用户需要滚动才看到投票区的概率

3. 提交后的反馈闭环（提升参与感）
   - 提交后自动滚动到结果区域（让用户立刻看到反馈）
   - 结果区域强调“你选择的景点”高亮展示（已实现高亮逻辑，可作为亮点说明）

### 3.5 量化目标（10% 增长目标）

- 目标：将自定义事件 `vote_submit_custom`（或 `vote_submit`）提升 10%
- 衡量方式：对比优化前后同等时间窗口内 `vote_submit_custom` 的事件数量与漏斗转化率变化

### 3.6 Phase 3 交付物（Deliverables）

- Exploration 截图（至少 2 张）：
  - 漏斗步骤设置截图（包含 Steps 与 Breakdown）
  - 漏斗结果/分设备对比截图（包含转化率与流失）
- 视频（录屏讲解）：
  - 展示：漏斗设置 → 关键数字 → 流失点 → 优化方案 → 10%目标
- 报告：
  - 可参考项目文件 `Phase3_Exploration_分析报告模板.md`，把你的截图数字填入即可

## 4. 结论（总结）

本项目完成 GA4 安装、关键交互事件埋点，并在 GA4 后台通过 Events Interface 创建额外自定义事件 `vote_submit_custom`。在 Phase 3 使用 Funnel exploration 对投票流程进行分析，定位主要流失点并提出可执行的优化方案与量化目标（提升 10%）。整体满足课程三项评估维度：技术准确性、战略匹配度与分析洞察。

