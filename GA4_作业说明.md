# GA4 作业：扬州六大景点网站（埋点与截图指引）

## 你的网站信息（填写）

- 网站名称：______________
- Public Live URL：https://emily531678.github.io/yz-ga4/
- GA4 Property / 数据流：Web（Measurement ID：`G-T39YW06F1C`）

## 已加入的 GA4 功能（本网站已完成）

页面已安装 GA4 `gtag.js`，并在投票相关交互里加入事件埋点与用户属性。

### 事件（Events）

- `vote_page_view`
  - 触发：页面加载完成（DOMContentLoaded）
  - 参数：`voter_status`（`voted` / `not_voted`）
- `vote_option_select`
  - 触发：选择投票选项时
  - 参数：`place`（景点名称）
- `vote_submit`
  - 触发：点击“投我一票”且成功提交时
  - 参数：`place`（景点名称）、`total_votes`（提交后总票数）
- `vote_results_view`
  - 触发：结果区域显示/刷新时
  - 参数：`total_votes`、`selected_place`、`voter_status`
- `image_load_error`
  - 触发：图片加载失败时
  - 参数：`alt`、`src`

### 用户属性（User Properties）

- `voter_status`
  - `not_voted`：未投票
  - `voted`：已投票

## Phase 1：Realtime 截图（老师要求）

1. 确认你的网站是「公开可访问」的 URL（例如 GitHub Pages / Wix / Google Sites）。
2. 打开 GA4：`Reports` → `Realtime`。
3. 在你自己的网站上做以下动作：
   - 点击任意一个景点选项（触发 `vote_option_select`）
   - 点击“投我一票”（触发 `vote_submit`）
4. 回到 GA4 的 `Realtime`，截图能看到你自己的实时活跃（以及事件列表/事件计数更佳）。

提示：如果你需要更容易定位自己的测试流量，可以用带参数的方式打开页面：

- 在网址后加 `?debug=1`（例如 `https://xxx.github.io/yz/?debug=1`）
- 浏览器控制台会输出 `[ga4] ...` 日志，便于确认事件已触发。

## Phase 1：用「Events Interface」创建 1 个 GA4 Custom Event（老师要求）

下面给你一个最简单、最容易成功的例子（建议照做）：

### 例子 A（推荐）：把“成功提交投票”定义成自定义事件

1. GA4：`Admin` → `Events` → `Create event`。
2. `Custom event name` 填：`vote_submit_custom`。
3. `Matching conditions`：
   - `event_name` `equals` `vote_submit`
4. 保存。

这样当页面触发 `vote_submit` 时，GA4 会在后台额外生成一个 `vote_submit_custom` 事件，满足“用界面创建自定义事件”的要求。

### 例子 B（可选）：只统计某一个景点的投票

1. `Custom event name`：`vote_submit_shouxihu`
2. `Matching conditions`：
   - `event_name` `equals` `vote_submit`
   - `place` `equals` `瘦西湖`

## Phase 2：Measurement Plan（1 页）写法示例

- Web/App property：扬州六大景点投票网页
- Business Objective：提高用户参与度并促使更多用户完成投票
- KPIs（选 2–3 个即可）：
  - `vote_submit` 事件数量（投票完成数）
  - `vote_option_select` 到 `vote_submit` 的转化率（投票漏斗）
  - `vote_results_view` 事件数量（查看结果次数）

## Phase 3：Exploration 示例（建议用 Funnel Exploration）

目标：找出用户在投票流程的哪一步流失最多，并提出优化。

可用漏斗步骤（Events）：

1. `vote_page_view`
2. `vote_option_select`
3. `vote_submit`

你可以针对设备（mobile/desktop）、新老用户（用 `voter_status`）做分段对比，输出截图 + 结论 + 优化建议（例如按钮文案、引导提示、把投票按钮移到更显眼位置等）。
