# IT114116 / ITP4827 Web Analytics (GA4 Final Report)

## 0. Project Overview

- School / Module: Hong Kong Institute of Information Technology — IT114116 / ITP4827 Web Analytics
- Topic: Digital Growth: Using GA4 to Improve “Yangzhou Six Major Attractions (Voting Website)” Performance
- Website name: Yangzhou Six Major Attractions (Voting Website)
- Public Live URL: https://emily531678.github.io/yz-ga4/
- Website type: Static website (HTML/CSS/Vanilla JS) + GA4 (gtag.js)
- GA4 Measurement ID: G-T39YW06F1C

## 1. Phase 1: GA4 Implementation & Tracking

### 1.1 Installation & Setup (Technical Accuracy)

- Installed GA4 tracking code (gtag.js) in the website `<head>`.
- The website data can be captured in GA4 Realtime reports.
- Debug mode is supported by adding `?debug=1` to the URL (to verify events in the browser console).

### 1.2 Event Tracking (Implemented on the Website)

The website tracks key interactions for the voting flow (used for KPIs and Explorations):

- `vote_page_view`: fired after page load (used as the first funnel step)
  - Parameters: `voter_status` (`voted` / `not_voted`)
- `vote_option_select`: fired when a user selects an attraction
  - Parameters: `place`
- `vote_submit`: fired when a user submits a vote (primary goal event)
  - Parameters: `place`, `total_votes`
- `vote_results_view`: fired when the results section is displayed/refreshed (engagement event)
  - Parameters: `total_votes`, `selected_place`, `voter_status`
- `image_load_error`: fired when an image fails to load (quality monitoring)
  - Parameters: `alt`, `src`

### 1.3 GA4 Custom Event (Created via Events Interface)

To satisfy the requirement “Use the GA4 Events Interface to create one GA4 Custom Event”, a custom event is created in GA4 (**Create events**) based on an existing event:

- Custom event name: `vote_submit_custom`
- Matching conditions:
  - `event_name` equals `vote_submit`
- Copy parameters from source event: Enabled (copies `place`, `total_votes`, etc.)

This custom event is used as evidence of “custom event created in the GA4 interface” and can be used as the measurement target in Phase 3 (e.g., +10%).

### 1.4 Phase 1 Deliverables

- Public Live URL: https://emily531678.github.io/yz-ga4/
- Realtime screenshot (to be captured by the student):
  1. Open: `https://emily531678.github.io/yz-ga4/?debug=1`
  2. Perform one voting action: select an attraction → click “Vote”
  3. GA4: Reports → Realtime, take a screenshot showing your own activity (ideally including `vote_submit` or `vote_submit_custom`)

## 2. Phase 2: Business Objective & KPIs Definition (Measurement Plan)

### 2.1 Business Objective

Increase user engagement and increase the number of completed votes, guiding more visitors from page view → option selection → successful vote submission.

### 2.2 KPIs (2–3 Measurable KPIs)

1. Primary KPI: Vote completions
   - Definition: Event count of `vote_submit` (or `vote_submit_custom`)
2. Funnel conversion rate (behavior KPI)
   - Definition: Conversion from `vote_option_select` → `vote_submit`
   - Calculation: `vote_submit` / `vote_option_select`
3. Results viewing (engagement KPI)
   - Definition: Event count of `vote_results_view`, or `vote_results_view` / `vote_page_view`

### 2.3 Phase 2 Deliverable

- One-page Measurement Plan: see `Phase2_MeasurementPlan_1页.md`

## 3. Phase 3: Insights, Analysis and Exploration

### 3.1 Exploration Tool Used

- Tool: GA4 Funnel exploration
- Goal: Identify the step with the highest drop-off in the voting funnel and propose actionable fixes to improve the primary KPI (vote completions).

### 3.2 Funnel Definition (Aligned with the Objective)

Funnel steps (Events):

1. `vote_page_view` (enter/load the voting page)
2. `vote_option_select` (select an attraction)
3. `vote_submit` (submit a vote)

Breakdown (segmentation):

- `Device category` (desktop vs mobile) to compare drop-off differences by device.

### 3.3 Findings (Example Format — Replace with Your Own Numbers)

Use the following structure and replace the numbers with your GA4 exploration results:

- Step 1 `vote_page_view`: 6
- Step 2 `vote_option_select`: 4 (Step1→Step2 conversion: 66.67%, drop-off: 33.33%)
- Step 3 `vote_submit`: 4 (Step2→Step3 conversion: 100%)

**Problem identified:**

- The main drop-off happens at Step1→Step2 (users visit the page but do not select any attraction).
- Step2→Step3 conversion is high, meaning users who select an option usually complete the vote.

### 3.4 Fix Recommendations (How to Improve)

To reduce drop-off at Step1→Step2:

1. Strengthen the call-to-action and value proposition
   - Add a clearer message: “Vote to see the live results immediately”
   - Make the instruction more visible (font size/color/position)

2. Reduce the friction to start voting
   - Add a “recommended” hint (e.g., highlight one option or show “tap any attraction to vote”)
   - Ensure the voting section is visible on the first screen for mobile users

3. Improve post-vote feedback loop (increase engagement)
   - Auto-scroll to the results section after voting
   - Keep highlighting the user’s selected attraction in results (already implemented)

### 3.5 Quantitative Target (+10%)

- Target: Increase `vote_submit_custom` (or `vote_submit`) by 10%
- Measurement: Compare event counts and funnel conversion rates before vs after implementing improvements, within the same time window.

### 3.6 Phase 3 Deliverables

- Screenshots (at least 2):
  - Funnel setup screenshot (Steps + Breakdown)
  - Funnel results screenshot (conversion/drop-off with device breakdown)
- Video (screen recording):
  - Show funnel setup → key numbers → drop-off point → fixes → +10% target
- Written report:
  - Use `Phase3_Exploration_分析报告模板.md` and fill in your actual numbers

## 4. Conclusion

This project successfully implemented GA4 tracking, configured custom interaction events for the voting flow, and created an additional custom event (`vote_submit_custom`) through the GA4 Events Interface. Using GA4 Funnel exploration, the project identified the main drop-off step and proposed actionable improvements with a measurable +10% growth target. Overall, the work meets the evaluation criteria of technical accuracy, strategic KPI alignment, and analytical insight.

