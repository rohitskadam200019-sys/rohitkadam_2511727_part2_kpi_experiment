# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

**Student:** Rohit Kadam
**Student ID:** 2511727
**Repository:** rohitkadam_2511727_part2_kpi_experiment
**Tool Used:** Microsoft Excel

---

## Business Context

A subscription-based digital product company launched a new onboarding and activation campaign. Users were split into two groups — a Control group experiencing the existing onboarding flow, and a Treatment group experiencing the new campaign. The company needs to decide whether to roll out the new campaign to all users based on experiment results.

---

## Business Problem Statement

### 1. What Decision Needs to Be Made
The company must decide whether to launch the new onboarding and activation campaign to all users, continue testing, or restrict the launch to a specific segment. The decision will be based on whether the treatment group shows a statistically meaningful and business-safe improvement over the control group.

### 2. Who the Decision Impacts
- **Users:** All new signups who will go through the onboarding experience
- **Product team:** Responsible for building and maintaining the campaign experience
- **Revenue team:** Impacted by changes in paid conversion rates and revenue per user
- **Support team:** Impacted by changes in support ticket volume
- **Leadership:** Accountable for the business outcome of the launch decision

### 3. What Metric Should Improve
The primary success metric is **Paid Conversion Rate** — the proportion of users who convert from free trial or signup to a paid subscription within 30 days. This directly measures whether the new campaign is achieving its core objective of improving user conversion and early engagement.

Supporting metrics that should also improve or remain stable:
- Landing page visit rate
- Trial start rate
- Onboarding completion rate
- Average revenue per user
- Average engagement score

### 4. What Risks Must Be Monitored
The following guardrail metrics must be monitored to ensure the improvement in conversion does not come at a cost to business health:
- **Refund rate:** An increase in refunds would indicate users are converting but not finding value
- **Support ticket rate:** A rise in support tickets suggests friction or confusion in the new experience
- **Days to convert:** If users take significantly longer to convert, revenue timing is impacted
- **Engagement score:** A decline in engagement despite higher conversion is a quality risk
- **Segment-level performance:** The treatment may help some segments while harming others

### 5. What Evidence Is Required Before Making a Recommendation
- A statistically significant difference in paid conversion rate between Control and Treatment groups (p-value < 0.05)
- No significant deterioration in guardrail metrics (refund rate, support ticket rate)
- Consistent improvement across key segments (region, device type, traffic source, plan type)
- Sufficient sample size in both groups to ensure reliable results
- Business interpretation that the lift is meaningful enough to justify a full rollout

---

## North Star Metric

**Selected Metric: Paid Conversion Rate**
(Users converted to paid / Total users in group)

### Why This Is the Main Success Metric
The campaign's sole objective is to improve user conversion and early engagement. Paid Conversion Rate is the only metric that directly confirms whether a user has committed real money to the product. Every other metric in the funnel — visiting the landing page, starting a trial, completing onboarding — is a step toward this outcome, not the outcome itself. A campaign that moves users all the way to paying is a campaign that works.

### Why Other Metrics Are Supporting Metrics Instead
- **Landing page visit rate** — measures top-of-funnel reach, not business value
- **Trial start rate** — indicates interest, but a trial user has not yet paid
- **Onboarding completion rate** — measures process success, not revenue outcome
- **Average revenue per user** — important, but depends on conversion happening first
- **Engagement score** — a leading indicator of retention, not of initial conversion

These metrics explain *how* users convert, not *whether* they do. They are drivers, not the destination.

### How This Metric Connects to Business Growth
Every paid conversion directly adds to Monthly Recurring Revenue (MRR). A higher conversion rate means more revenue from the same number of signups — improving unit economics without increasing acquisition cost. At scale, even a 1–2 percentage point improvement in conversion rate compounds into significant revenue growth over time.

### What Could Go Wrong If Optimized Blindly
If Paid Conversion Rate is chased without monitoring guardrails:
- Aggressive prompts or pressure tactics could push users to convert but then refund quickly
- Conversion rate could rise while engagement score falls — indicating low-quality users who churn
- Support ticket rate could increase if the new experience is confusing but still converts some users
- Segment-level harm could be hidden — overall conversion improves while specific regions or devices decline
- Revenue per converted user could drop if discounts or incentives are used to inflate conversion numbers

---

## Experiment Data Preparation (Task 4)

> **Important:** The original dataset file `data/campaign_experiment_data.xlsx` has NOT been modified in any way. All cleaning and preparation work was done in a separate file: `analysis/experiment_analysis.xlsx`. The raw file is preserved exactly as downloaded.

### Dataset Overview
- **Total records:** 1,408 users
- **Control group:** 693 users
- **Treatment group:** 715 users
- **Columns:** 16 original fields

### Check 1 — Missing Values

| Column | Missing Count | Action Taken |
|---|---|---|
| device_type | 18 | Filled with 'Unknown' — retained for analysis |
| traffic_source | 24 | Filled with 'Unknown' — retained for analysis |
| days_to_convert | 1,336 | Expected — null for non-converted users. Excluded from average calculation |
| engagement_score | 14 | Excluded from average score calculation only |
| All other columns | 0 | No action needed |

### Check 2 — Group Counts

| Group | Count | % of Total |
|---|---|---|
| Control | 693 | 49.2% |
| Treatment | 715 | 50.8% |
| **Total** | **1,408** | **100%** |

Groups are well balanced — no significant skew.

### Check 3 — Duplicate User IDs
- Total rows: 1,408
- Unique user_ids: 1,400
- Duplicate user_ids found: **8 user_ids appearing twice**
- Action: First occurrence kept, duplicate removed
- Rows retained after deduplication: **1,400**

### Check 4 — Invalid Binary Values
Checked columns: `visited_landing_page`, `started_trial`, `completed_onboarding`, `converted_to_paid`, `refund_requested`

**Result: No invalid values found.** All binary columns contain only 0 or 1.

### Check 5 — Revenue Outliers
- 72 users have revenue > 0 (converted users)
- 7 users have revenue > 2,000 (high-value outliers)
- Maximum revenue: 8,610.72
- **Action: Outliers retained** — high revenue is a valid business outcome for premium subscriptions. Flagged as 'Outlier - Retained' in prepared data.

### Check 6 — Segment Distribution Across Groups

| Segment | Control | Treatment | Balanced? |
|---|---|---|---|
| Region — East | 158 | 172 | ✅ Yes |
| Region — North | 203 | 180 | ✅ Yes |
| Region — South | 184 | 184 | ✅ Yes |
| Region — West | 148 | 179 | ✅ Yes |
| Device — Desktop | 200 | 214 | ✅ Yes |
| Device — Mobile | 428 | 436 | ✅ Yes |
| Device — Tablet | 56 | 56 | ✅ Yes |
| Plan — Basic | 223 | 235 | ✅ Yes |
| Plan — Free | 361 | 368 | ✅ Yes |
| Plan — Premium | 109 | 112 | ✅ Yes |

All segments are well distributed across both groups — randomization appears valid.

---

## KPI Tree Summary

The North Star metric (Paid Conversion Rate) breaks down into three primary drivers:

**Driver 1 — Funnel Progression**
Tracks how users move through each onboarding step toward conversion.
- Sub-drivers: Landing page visit rate, Trial start rate, Onboarding completion rate

**Driver 2 — Revenue Quality**
Tracks the financial value generated per user and per conversion.
- Sub-drivers: Average revenue per user, Average revenue per converted user

**Driver 3 — User Engagement**
Tracks the quality and intent of users during and after onboarding.
- Sub-drivers: Engagement score, Days to convert

**Guardrail Metrics (must not deteriorate):**
- Refund rate — conversion quality check
- Support ticket rate — user friction check
- Engagement score — retention quality check

*(Full KPI tree visual: outputs/kpi_tree.png)*

---

## Experiment Analysis Approach

- Dataset: 1,408 users — Control (693) vs Treatment (715)
- Cleaned and validated data in `analysis/experiment_analysis.xlsx` — original dataset untouched
- Checked for missing values, duplicates, invalid binary values, revenue outliers, and segment balance
- Computed all 11 required metrics for both groups using exact formulas
- Performed segment-level analysis for 3 metrics across Region, Device Type, and Traffic Source
- Conducted a two-proportion z-test (one-tailed) on Paid Conversion Rate as the primary metric
- Evaluated 4 guardrail metrics before forming the final recommendation

*(Full analysis: analysis/experiment_analysis.xlsx, outputs/experiment_summary.xlsx)*

---

## Hypothesis Test Summary

- **Test:** Two-proportion z-test (one-tailed, right-tailed)
- **H0:** p_treatment ≤ p_control
- **H1:** p_treatment > p_control
- **Significance level:** α = 0.05

| Output | Value |
|---|---|
| Control conversion rate | 3.17% (22/693) |
| Treatment conversion rate | 6.99% (50/715) |
| z-statistic | 3.252 |
| p-value (one-tailed) | 0.0006 |
| Decision | **REJECT H0** |

The improvement in paid conversion rate is statistically significant. We are 99.94% confident the result is genuine. The result holds at both the 5% and 1% significance levels.

*(Full test workings: analysis/hypothesis_test_notes.md)*

---

## Guardrail Metrics Considered

| Guardrail Metric | Control | Treatment | Lift | Risk Level |
|---|---|---|---|---|
| Refund Rate | 0.00% | 0.42% | +0.42pp | LOW |
| Support Ticket Rate | 21.93% | 37.20% | +15.27pp | HIGH |
| Days to Convert | 8.86 days | 6.40 days | -2.46 days | POSITIVE |
| Revenue Per Converted User | 1,630.10 | 770.41 | -859.69 | MEDIUM |

- **Refund rate** — low risk, only 3 refunds. Monitor post-launch.
- **Support ticket rate** — highest risk. +15.27pp increase requires investigation before full rollout.
- **Days to convert** — positive signal. Users convert 2.46 days faster in Treatment.
- **Revenue per converted user** — medium risk. Total revenue is still higher in Treatment due to volume.

*(Full guardrail analysis: analysis/experiment_analysis.xlsx — Guardrail Metrics sheet)*

---

## Final Recommendation

### ✅ LAUNCH the campaign to all users.

**Key evidence:**
- Paid Conversion Rate: 3.17% → 6.99% (+3.82pp) — statistically significant (p = 0.0006)
- All 10 segments across Region, Device, and Plan Type show positive lift — no declines
- Total revenue higher in Treatment (38,521 vs 35,862)
- Users convert 2.46 days faster
- Engagement score improved (+5.90)

**Conditions:**
- Investigate support ticket categories before or at launch
- Increase support team capacity for first 60 days
- Monitor revenue per converted user monthly

*(Full recommendation with risks and next steps: outputs/recommendation_memo.md)*

---

## Assumptions and Limitations

### Assumptions
1. Users were randomly assigned to Control and Treatment — no selection bias assumed
2. The 30-day observation window is sufficient to measure conversion intent
3. Missing device_type (18) and traffic_source (24) treated as Unknown — not excluded
4. days_to_convert nulls for non-converted users are expected — excluded from average only
5. Revenue outliers retained — high revenue is a valid outcome for premium subscriptions
6. Engagement score nulls (14 users) excluded from average score calculation only

### Limitations
1. Experiment ran for a limited time window — long-term retention and churn are unknown
2. days_to_convert only captured for converted users — non-converters' intent timeline is missing
3. 18 users missing device_type and 24 missing traffic_source — minor segment gap
4. Revenue outliers (max 8,610) may skew average revenue per user figures
5. Statistical significance does not guarantee the same lift at full production scale

---

## Screenshots Included

| File | Shows |
|---|---|
| `screenshots/summary_metrics.png` | Control vs Treatment full metric summary table |
| `screenshots/hypothesis_test_output.png` | z-test output — z=3.252, p=0.0006, REJECT H0 |
| `screenshots/kpi_tree_preview.png` | KPI tree showing North Star, drivers, and guardrails |

---

## Repository Structure

```
part2_kpi_experiment/
├── data/
│   └── campaign_experiment_data.xlsx
├── analysis/
│   ├── experiment_analysis.xlsx
│   └── hypothesis_test_notes.md
├── outputs/
│   ├── kpi_tree.png
│   ├── experiment_summary.xlsx
│   └── recommendation_memo.md
├── screenshots/
│   ├── summary_metrics.png
│   ├── hypothesis_test_output.png
│   └── kpi_tree_preview.png
└── README.md
```
