# Recommendation Memo — Part 2: Campaign Experiment Analysis

**To:** Leadership Team
**From:** Rohit Kadam, Business Analyst
**Date:** June 2025
**Subject:** New Onboarding Campaign — Launch Decision Recommendation

---

## 1. Executive Summary

The company ran an A/B experiment to evaluate a new onboarding and activation campaign across 1,408 users — 693 in Control and 715 in Treatment. The Treatment group experienced the new campaign while the Control group experienced the existing onboarding flow.

The experiment produced a statistically significant improvement in Paid Conversion Rate — the North Star metric — from 3.17% (Control) to 6.99% (Treatment), a lift of +3.82 percentage points (p-value = 0.0006). Every segment showed positive improvement with no declines detected.

One guardrail metric raised a material concern: the Support Ticket Rate increased from 21.93% to 37.20% (+15.27pp), indicating the new experience may be creating friction or confusion for some users. This does not block the launch but requires attention.

**Recommendation: Launch the campaign to all users, with the support team on standby and ticket categories investigated within the first 30 days.**

---

## Business Problem Statement

### What Decision Needs to Be Made
Whether to launch the new onboarding and activation campaign to all users, based on whether the treatment group demonstrates a meaningful and statistically significant improvement over the control group without deteriorating guardrail metrics.

### Who the Decision Impacts
- New users going through onboarding
- Product and revenue teams managing the campaign
- Support teams affected by ticket volume changes
- Leadership accountable for revenue outcomes

### What Metric Should Improve
**Paid Conversion Rate** is the North Star metric. The campaign's primary objective is to convert more users to paid subscriptions within 30 days of signup.

### What Risks Must Be Monitored
- Refund rate increasing (conversion without value)
- Support ticket rate rising (user friction)
- Engagement score declining (quality of acquired users)
- Days to convert increasing (revenue timing delay)
- Segment-level decline (some groups harmed while overall improves)

### What Evidence Is Required Before Making a Recommendation
- p-value < 0.05 on conversion rate difference
- Stable or improved guardrail metrics
- Consistent positive signal across segments
- Sample size sufficient for reliable inference

---

## 2. North Star Metric

**Selected Metric: Paid Conversion Rate**
(Users converted to paid / Total users in group)

### Why This Is the Main Success Metric
Paid Conversion Rate is the only metric that confirms a user has moved from free to paid — the core business outcome this campaign is designed to drive. All funnel steps before it are means to this end. Every other metric in the funnel — visiting the landing page, starting a trial, completing onboarding — is a step toward this outcome, not the outcome itself.

### Why Other Metrics Are Supporting Metrics
- **Landing page visit rate** — reach only, no revenue signal
- **Trial start rate** — intent, not commitment
- **Onboarding completion rate** — process metric, not outcome metric
- **Average revenue per user** — downstream of conversion, not the trigger
- **Engagement score** — predicts retention but does not confirm payment

### How This Metric Connects to Business Growth
Each additional paid conversion adds directly to MRR. Improving conversion rate from 3% to 7% on the same user base doubles revenue without any increase in acquisition spend — a direct and compounding impact on business growth.

### What Could Go Wrong If Optimized Blindly
- High conversion rate paired with high refund rate = revenue that does not stick
- Pressure-driven conversion inflates short-term numbers but damages trust and retention
- Engagement score decline signals users are converting but not finding product value
- Segment-level declines get masked by an overall positive number

| Metric | Control | Treatment | Lift |
|---|---|---|---|
| **Paid Conversion Rate (North Star)** | **3.17%** | **6.99%** | **+3.82pp** |

---

## 3. KPI Tree Explanation

The North Star metric (Paid Conversion Rate) is supported by three primary KPI drivers:

**Driver 1 — Funnel Progression**
Measures how users move through the onboarding steps before converting.
- Landing page visit rate: 63.64% → 72.59% (+8.95pp) ✅
- Trial start rate: 25.11% → 29.09% (+3.98pp) ✅
- Onboarding completion rate: 15.58% → 21.26% (+5.68pp) ✅

All three funnel steps improved in Treatment — confirming the campaign successfully moves users further through the funnel at every stage.

**Driver 2 — Revenue Quality**
Measures the financial value generated per user and per conversion.
- Average revenue per user: 51.75 → 53.88 (+2.13) ✅
- Average revenue per converted user: 1,630.10 → 770.41 (-859.69) ⚠️
- Total group revenue: 35,862 → 38,521 (+2,659) ✅

Revenue per converted user dropped significantly, but total revenue is higher because more users converted. This is a medium-risk signal that warrants monitoring.

**Driver 3 — User Engagement**
Measures the quality and intent of users acquired through the campaign.
- Average engagement score: 57.03 → 62.93 (+5.90) ✅
- Average days to convert: 8.86 → 6.40 (-2.46 days) ✅

Engagement improved and users converted faster — both strong positive signals for long-term retention.

**Guardrail Metrics (must not deteriorate):**
- Refund rate: 0.00% → 0.42% (LOW risk — 3 refunds only)
- Support ticket rate: 21.93% → 37.20% (HIGH risk — requires investigation)
- Engagement score: 57.03 → 62.93 (POSITIVE — improved)

---

## 4. Experiment Result Summary

| Metric | Control | Treatment | Lift | Direction |
|---|---|---|---|---|
| User Count | 693 | 715 | +22 | — |
| Landing Page Visit Rate | 63.64% | 72.59% | +8.95pp | ✅ |
| Trial Start Rate | 25.11% | 29.09% | +3.98pp | ✅ |
| Onboarding Completion Rate | 15.58% | 21.26% | +5.68pp | ✅ |
| Paid Conversion Rate ★ | 3.17% | 6.99% | +3.82pp | ✅ |
| Avg Revenue Per User | 51.75 | 53.88 | +2.13 | ✅ |
| Avg Revenue Per Converted User | 1,630.10 | 770.41 | -859.69 | ⚠️ |
| Refund Rate | 0.00% | 0.42% | +0.42pp | 🟡 |
| Support Ticket Rate | 21.93% | 37.20% | +15.27pp | 🔴 |
| Avg Engagement Score | 57.03 | 62.93 | +5.90 | ✅ |
| Avg Days to Convert | 8.86 | 6.40 | -2.46 days | ✅ |

★ = North Star Metric

8 out of 11 metrics improved in Treatment. 1 metric shows high risk (support ticket rate). 1 shows medium risk (revenue per converted user). 1 is a minor concern (refund rate).

---

## 5. Hypothesis Test Interpretation

**Test:** Two-proportion z-test (one-tailed, right-tailed)
**H0:** p_treatment ≤ p_control
**H1:** p_treatment > p_control
**Significance level:** α = 0.05

| Test Output | Value |
|---|---|
| Control conversion rate | 3.17% (22/693) |
| Treatment conversion rate | 6.99% (50/715) |
| Pooled proportion | 0.0511 |
| Standard error | 0.01174 |
| z-statistic | 3.252 |
| Critical value (α=0.05) | 1.6449 |
| p-value (one-tailed) | 0.0006 |
| Decision | **REJECT H0** |

**Interpretation:** The p-value of 0.0006 is well below the threshold of 0.05. We reject the null hypothesis. The Treatment group's conversion rate of 6.99% is statistically significantly higher than the Control group's 3.17%. We are 99.94% confident this result is genuine and not due to random chance.

The result is significant at both the 5% and 1% significance levels — providing very strong statistical evidence that the new campaign improves paid conversion.

---

## 6. Guardrail Analysis

| Guardrail Metric | Control | Treatment | Lift | Risk Level | Blocks Launch? |
|---|---|---|---|---|---|
| Refund Rate | 0.00% | 0.42% | +0.42pp | LOW | No |
| Support Ticket Rate | 21.93% | 37.20% | +15.27pp | HIGH | Conditional |
| Days to Convert | 8.86 days | 6.40 days | -2.46 days | POSITIVE | No |
| Revenue Per Converted User | 1,630.10 | 770.41 | -859.69 | MEDIUM | No |

**Refund Rate (LOW RISK):** Only 3 refunds out of 50 conversions in Treatment. Small absolute number. Monitor post-launch but not a concern at this scale.

**Support Ticket Rate (HIGH RISK):** The most significant guardrail concern. A +15.27pp increase means Treatment users are raising support tickets at a 69.5% higher rate than Control users. This suggests friction or unmet expectations in the new onboarding experience. This does not block launch but requires the support team to investigate ticket categories and increase capacity for the first 60 days.

**Days to Convert (POSITIVE):** Users in Treatment convert 2.46 days faster. Faster conversion is a positive business outcome — it means stronger user intent and faster revenue recognition.

**Revenue Per Converted User (MEDIUM RISK):** Revenue per converted user dropped by 53% (from 1,630 to 770). However, total revenue is still higher in Treatment (38,521 vs 35,862) because more users converted. The drop is likely driven by the mix of plan types — Free plan conversions increased most strongly (+6.19pp lift), which carry lower revenue. Monitor per-user revenue monthly to ensure it stabilises.

---

## 7. Segment-Level Insight

**By Region:**

| Region | Control | Treatment | Lift |
|---|---|---|---|
| North | 3.45% | 8.89% | +5.44pp ✅ |
| South | 3.26% | 7.61% | +4.35pp ✅ |
| East | 2.53% | 6.40% | +3.86pp ✅ |
| West | 3.38% | 5.03% | +1.65pp ✅ |

North region shows the strongest lift (+5.44pp). West shows the weakest lift (+1.65pp) — worth monitoring post-launch.

**By Device Type:**

| Device | Control | Treatment | Lift |
|---|---|---|---|
| Tablet | 1.79% | 7.14% | +5.36pp ✅ |
| Mobile | 2.57% | 7.34% | +4.77pp ✅ |
| Desktop | 4.50% | 6.54% | +2.04pp ✅ |

Tablet and Mobile users show the strongest lift. The campaign appears especially effective for mobile-first users.

**By Plan Type:**

| Plan | Control | Treatment | Lift |
|---|---|---|---|
| Free | 3.05% | 9.24% | +6.19pp ✅ |
| Premium | 2.75% | 6.25% | +3.50pp ✅ |
| Basic | 3.59% | 3.83% | +0.24pp ✅ |

Free plan users show the strongest lift (+6.19pp). Basic plan users show minimal lift (+0.24pp) — consider a tailored onboarding variant for Basic users in future testing.

**Key insight:** No segment showed a decline. The campaign is universally positive — but the lift is uneven. Free plan and Mobile/Tablet users benefit the most.

---

## 8. Final Recommendation

### ✅ LAUNCH the campaign to all users.

**Supporting evidence:**
- Paid Conversion Rate improved from 3.17% to 6.99% — a statistically significant +3.82pp lift (p = 0.0006)
- All 10 segments (region, device, plan) show positive conversion lift with no declines
- Total revenue increased from 35,862 to 38,521 despite lower per-user revenue
- Users convert 2.46 days faster — stronger intent and faster revenue recognition
- Engagement score improved (+5.90) — higher quality users post-conversion
- Refund rate remains negligible (0.42%)

**Conditions on launch:**
- The support team must investigate the top categories of support tickets raised by Treatment group users before or immediately after launch
- Support capacity must be increased for the first 60 days post-launch
- Revenue per converted user must be tracked monthly to ensure it does not continue declining

---

## 9. Risks and Limitations

**Risks:**
1. **Support ticket volume** — a 37.2% support ticket rate at full scale will significantly increase support team load. If not managed, this can hurt customer satisfaction and retention.
2. **Revenue per converted user** — if the drop from 1,630 to 770 per user is structural rather than segment-mix driven, long-term revenue impact could be negative even with higher conversion volume.
3. **Basic plan users** — minimal lift of +0.24pp suggests the campaign may not resonate with this segment.
4. **Refund rate at scale** — 0.42% refund rate on 50 conversions becomes more significant at scale. Must be monitored as treatment rolls out to thousands of users.

**Limitations:**
1. Experiment ran for a limited time window — long-term retention and churn rates are unknown
2. days_to_convert is only measured for converted users — non-converters' time-to-decision is not captured
3. 18 users missing device_type and 24 missing traffic_source — minor gap in segment completeness
4. Revenue outliers (max 8,610) were retained — they may skew average revenue figures
5. The experiment cannot confirm causality beyond the 30-day observation window

---

## 10. Next Steps

1. **Immediately:** Share support ticket category data with the product team to identify and fix friction points
2. **Before launch:** Brief the support team on the expected ticket volume increase and prepare response templates
3. **At launch:** Roll out campaign to 100% of new users
4. **Week 1–4:** Monitor conversion rate, support ticket rate, and refund rate weekly
5. **Month 2:** Evaluate revenue per converted user — confirm whether the drop is stabilising
6. **Month 3:** Run a follow-up analysis on 90-day retention rates for Treatment converters vs Control converters
7. **Future testing:** Design a variant specifically for Basic plan users to improve their minimal lift (+0.24pp)
8. **Ongoing:** Track West region performance — it showed the weakest lift and may benefit from a region-specific onboarding tweak

---

*Analysis based on experiment data: 1,408 users, Feb–May 2025. Full workings in analysis/experiment_analysis.xlsx, analysis/hypothesis_test_notes.md, and outputs/experiment_summary.xlsx.*
