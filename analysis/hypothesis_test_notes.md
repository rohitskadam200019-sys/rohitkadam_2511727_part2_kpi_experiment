# Hypothesis Test Notes — Campaign Experiment Analysis

**Student:** Rohit Kadam
**Student ID:** 2511727
**Part:** Part 2 — KPI Framework & Experiment Analysis

---

## 1. Metric Being Tested

**Paid Conversion Rate**
(Users converted to paid / Total users in group × 100)

- Control group: 22 conversions / 693 users = **3.17%**
- Treatment group: 50 conversions / 715 users = **6.99%**

---

## 2. Reason for Choosing This Metric

Paid Conversion Rate is the North Star metric for this experiment. The entire purpose of the new onboarding and activation campaign is to increase the proportion of users who become paying customers within 30 days. This metric directly measures whether the campaign achieves its primary business objective.

All other metrics (landing page visit rate, trial start rate, onboarding completion rate) are funnel steps leading toward conversion. Testing conversion rate gives the clearest, most direct answer to the business question: **does the new campaign make more users pay?**

---

## 3. Null Hypothesis (H0)

> The paid conversion rate of the Treatment group is equal to or less than the paid conversion rate of the Control group.

**H0: p_treatment ≤ p_control**

In other words: the new campaign has no positive effect on conversion. Any observed difference is due to random chance.

---

## 4. Alternate Hypothesis (H1)

> The paid conversion rate of the Treatment group is greater than the paid conversion rate of the Control group.

**H1: p_treatment > p_control**

In other words: the new campaign genuinely improves conversion rate above and beyond what chance alone would produce.

---

## 5. One-Tailed or Two-Tailed Test

**One-tailed test (right-tailed)**

The business question is directional — leadership wants to know whether the Treatment is **better** than Control, not merely **different**. There is no business value in detecting whether the campaign makes conversion worse (that would simply mean do not launch). A one-tailed test is therefore appropriate as it tests specifically for improvement in the direction the campaign intends.

---

## 6. Significance Level

**α = 0.05 (5%)**

This is the standard significance level used in business A/B testing. It means we accept a 5% probability of concluding the campaign works when it actually does not (Type I error). Given the business stakes — a full product rollout decision — a 5% false positive risk is acceptable.

---

## 7. Interpretation Logic

### Decision Rule
- If **p-value < 0.05** → Reject H0 → The improvement in conversion rate is statistically significant → Evidence supports launching the campaign
- If **p-value ≥ 0.05** → Fail to reject H0 → The difference may be due to chance → Do not launch based on this evidence alone

### Test Type
Two-proportion z-test (one-tailed, right-tailed)

This test is appropriate because:
- We are comparing two independent proportions (conversion rates)
- Both sample sizes are large (693 and 715) — satisfying the normal approximation condition
- The groups are independent — users were randomly assigned

### Formula Used
```
z = (p_treatment - p_control) / sqrt(p_pooled × (1 - p_pooled) × (1/n_treatment + 1/n_control))

where:
  p_control   = 22 / 693  = 0.0317
  p_treatment = 50 / 715  = 0.0699
  p_pooled    = (22 + 50) / (693 + 715) = 72 / 1408 = 0.0511
  n_control   = 693
  n_treatment = 715
```

### Test Output
```
p_pooled    = 0.0511
SE          = sqrt(0.0511 × 0.9489 × (1/693 + 1/715)) = 0.01317
z-statistic = (0.0699 - 0.0317) / 0.01317 = 2.901
p-value     = P(Z > 2.901) ≈ 0.0019
```

### Result
**p-value = 0.0019 < 0.05 → Reject H0**

The result is statistically significant at the 5% level. The probability of observing a conversion rate difference this large by chance alone is less than 0.2%.

### Business Interpretation
The Treatment group's conversion rate of 6.99% is statistically significantly higher than the Control group's 3.17%. The new onboarding and activation campaign has a genuine positive effect on paid conversion. This result, combined with guardrail metric evaluation, forms the basis for the launch recommendation.

However, statistical significance alone does not mean the campaign is safe to launch. The following guardrail metrics must also be evaluated before a final decision:
- **Refund rate** — Treatment shows 0.42% vs Control 0.00% (small but present increase)
- **Support ticket rate** — Treatment shows 37.2% vs Control 21.93% (significant increase — requires attention)
- **Engagement score** — Treatment shows 62.93 vs Control 57.03 (positive signal)
- **Days to convert** — Treatment shows 6.4 days vs Control 8.86 days (users convert faster — positive)

The hypothesis test confirms the campaign works. The guardrail evaluation determines whether it is safe to launch.

---

## 8. Connection to Business Decision

| Test Outcome | Business Action |
|---|---|
| Reject H0 (p < 0.05) + guardrails stable | **Launch campaign to all users** |
| Reject H0 (p < 0.05) + guardrails show risk | **Launch to selected segments only / continue monitoring** |
| Fail to reject H0 (p ≥ 0.05) | **Do not launch — insufficient evidence** |

**This experiment result: Reject H0 — p-value = 0.0019**
Proceed to guardrail evaluation before final recommendation.

---

*Test performed using two-proportion z-test. Calculations documented in outputs/experiment_summary.xlsx and Task 7 analysis.*

---

## Task 7 — A/B Test Results

### Summary of Test Inputs

| Input | Control | Treatment |
|---|---|---|
| Total users (n) | 693 | 715 |
| Converted users (x) | 22 | 50 |
| Conversion rate (p) | 3.17% | 6.99% |
| Significance level (α) | 0.05 | 0.05 |
| Test type | One-tailed (right) | One-tailed (right) |

### Step-by-Step Test Calculations

```
p_control   = 22 / 693                          = 0.0317
p_treatment = 50 / 715                          = 0.0699
p_pooled    = (22 + 50) / (693 + 715)           = 0.0511
SE          = √(0.0511 × 0.9489 × (1/693 + 1/715)) = 0.01174
z-statistic = (0.0699 - 0.0317) / 0.01174      = 3.252
p-value     = P(Z > 3.252)                      = 0.0006
Critical value (α = 0.05, one-tailed)           = 1.6449
```

### Test Output

| Output | Value |
|---|---|
| z-statistic | **3.252** |
| p-value (one-tailed) | **0.0006** |
| Critical value (α = 0.05) | 1.6449 |
| z > Critical value? | YES — 3.252 > 1.6449 |
| p-value < α? | YES — 0.0006 < 0.05 |
| Decision | **REJECT H0** |

### Decision Rule

- z > 1.6449 AND p-value < 0.05 → **Reject H0** → Campaign improves conversion → Evidence to LAUNCH
- z ≤ 1.6449 OR p-value ≥ 0.05 → **Fail to reject H0** → Insufficient evidence → Do not launch

**This experiment: z = 3.252 > 1.6449 | p-value = 0.0006 < 0.05 → REJECT H0**

### Business Interpretation

The Treatment group's paid conversion rate of 6.99% is statistically significantly higher than the Control group's 3.17% — a lift of +3.82 percentage points. With a p-value of 0.0006, we are 99.94% confident this improvement is genuine and not due to random chance. The result is significant at both the 5% and 1% significance levels.

The conversion rate more than doubled, representing strong practical significance in addition to statistical significance. This is compelling evidence that the new onboarding campaign genuinely improves user conversion.

However, statistical significance alone is not sufficient for a launch decision. The support ticket rate increased significantly (21.93% → 37.2%), which must be evaluated as a guardrail risk before proceeding with a full rollout.

*(Full test calculations available in analysis/ab_test_analysis.xlsx — see screenshot: screenshots/hypothesis_test_output.png)*

---

## Task 8 — Guardrail Metric Evaluation

> Statistical significance in the North Star metric (Paid Conversion Rate) is necessary but not sufficient for a launch decision. The following 4 guardrail metrics were evaluated to assess whether the campaign is safe to launch.

---

### Guardrail 1 — Refund Rate

| | Control | Treatment | Lift |
|---|---|---|---|
| Refund Rate | 0.00% (0 refunds) | 0.42% (3 refunds) | +0.42pp |

**Risk Level: LOW**

3 refunds out of 50 conversions in the Treatment group. The absolute number is small. This is not a blocker for launch but must be monitored weekly post-launch to ensure it does not grow as the campaign scales to all users.

**Creates risk? No — minor and manageable.**

---

### Guardrail 2 — Support Ticket Rate

| | Control | Treatment | Lift |
|---|---|---|---|
| Support Ticket Rate | 21.93% (152 tickets) | 37.20% (266 tickets) | +15.27pp |

**Risk Level: HIGH**

Support ticket rate increased by +15.27 percentage points — a 69.5% relative increase. Treatment users raised 114 more support tickets than Control despite having only 22 more users. This is the most significant guardrail risk in this experiment.

A spike in support tickets suggests the new onboarding experience may be creating confusion, unmet expectations, or friction for users — even as it successfully drives more conversions.

**Creates risk? YES — this is a material concern.**
Recommended action: Investigate the top categories of support tickets in the Treatment group before full rollout. Launch with the support team on standby with increased capacity.

---

### Guardrail 3 — Days to Convert

| | Control | Treatment | Lift |
|---|---|---|---|
| Avg Days to Convert | 8.86 days | 6.40 days | -2.46 days |

**Risk Level: POSITIVE (no risk)**

Treatment users convert 2.46 days faster than Control users. This is a positive signal — faster conversion means faster revenue recognition and stronger early intent. The new campaign appears to accelerate the user decision-making process.

**Creates risk? No — this is a positive guardrail outcome.**

---

### Guardrail 4 — Revenue Per Converted User

| | Control | Treatment | Lift |
|---|---|---|---|
| Avg Revenue Per Converted User | 1,630.10 | 770.41 | -859.69 |
| Total Group Revenue | 35,862.20 | 38,520.50 | +2,658.30 |

**Risk Level: MEDIUM**

Revenue per converted user dropped by 53% in Treatment. However, because the Treatment group converted more than twice as many users (50 vs 22), total group revenue is still higher in Treatment (38,520 vs 35,862). The campaign converts more users at lower individual value — which is net positive in aggregate but raises a concern about conversion quality and long-term retention.

**Creates risk? Conditionally — monitor per-user revenue trend monthly.**

---

### Guardrail 5 — Segment Level Decline

| Segment | Value | Control | Treatment | Lift | Decline? |
|---|---|---|---|---|---|
| Region | East | 2.53% | 6.40% | +3.86pp | No |
| Region | North | 3.45% | 8.89% | +5.44pp | No |
| Region | South | 3.26% | 7.61% | +4.35pp | No |
| Region | West | 3.38% | 5.03% | +1.65pp | No |
| Device | Desktop | 4.50% | 6.54% | +2.04pp | No |
| Device | Mobile | 2.57% | 7.34% | +4.77pp | No |
| Device | Tablet | 1.79% | 7.14% | +5.36pp | No |
| Plan | Basic | 3.59% | 3.83% | +0.24pp | No |
| Plan | Free | 3.05% | 9.24% | +6.19pp | No |
| Plan | Premium | 2.75% | 6.25% | +3.50pp | No |

**Risk Level: NONE**

No segment shows a decline in conversion rate. Every region, device type, and plan type shows a positive lift for Treatment over Control. The campaign improves conversion consistently across all user groups.

**Creates risk? No — safe across all segments.**

---

### Overall Guardrail Summary

| Guardrail Metric | Risk Level | Blocks Launch? |
|---|---|---|
| Refund Rate | LOW | No |
| Support Ticket Rate | HIGH | Conditional |
| Days to Convert | POSITIVE | No |
| Revenue Per Converted User | MEDIUM | No |
| Segment Level Decline | NONE | No |

**Guardrail conclusion:** The campaign is statistically proven to improve conversion and shows no segment-level decline. The primary risk is the significant rise in support ticket rate (+15.27pp). This does not block launch but requires the support team to be prepared and the ticket categories to be investigated. Proceed to recommendation with this risk noted.

