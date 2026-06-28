# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

**Student:** Gaurav Karwa  
**Student ID:** bitsom_ba_2511408  
**Repository:** `gauravkarwa_2511408_part2_kpi_experiment`

---

## 1. Business Context

A subscription-based digital product company launched a **new onboarding and activation campaign** to improve user conversion and early engagement. Users were randomly split into:
- **Control group** (693 users): Existing onboarding experience
- **Treatment group** (715 users): New campaign experience

Leadership needs to decide whether to roll out the Treatment campaign to all users based on experimental evidence.

**Business Problem Statement:**
1. **Decision:** Should the new onboarding campaign be launched to all users?
2. **Who it impacts:** All new users going through the onboarding funnel; Customer Success team; Finance/Revenue team
3. **Metric that should improve:** Paid Conversion Rate (North Star)
4. **Risks to monitor:** Refund rate, support ticket rate, revenue per converted user, segment-level declines
5. **Evidence required:** Statistically significant improvement in paid conversion rate (p < 0.05), with no critical breaches in guardrail metrics

---

## 2. Dataset Description

**File:** `data/campaign_experiment_data.xlsx`  
**Total Records:** 1,408 users  
**Columns:**

| Column | Description |
|--------|-------------|
| user_id | Unique user identifier |
| signup_date | Date user signed up |
| experiment_group | Control or Treatment |
| region | North / South / East / West |
| device_type | Desktop / Mobile / Tablet |
| traffic_source | Email / Organic / Paid Search / Referral / Social |
| plan_type | Free / Basic / Premium |
| visited_landing_page | Binary: 1 = visited |
| started_trial | Binary: 1 = started trial |
| completed_onboarding | Binary: 1 = completed onboarding |
| converted_to_paid | Binary: 1 = converted to paid plan |
| revenue_30d | Revenue generated in 30 days ($) |
| support_tickets_30d | Number of support tickets raised |
| refund_requested | Binary: 1 = refund requested |
| days_to_convert | Days from signup to conversion (blank if not converted) |
| engagement_score | User engagement score (0–100) |

---

## 3. North Star Metric Selected

**Paid Conversion Rate** — proportion of users who converted from free/trial to a paid plan within 30 days.

**Why this metric:**
- Directly measures the campaign's stated objective
- Captures full funnel performance (visit → trial → onboard → pay)
- Direct driver of subscription revenue
- Observable within the 30-day experiment window

**What could go wrong if optimized blindly:**
- Lower-quality conversions (lower ARPU, higher churn)
- Degraded support experience (tickets surge)
- Revenue per converter could drop

---

## 4. KPI Tree Summary

The KPI Tree breaks Paid Conversion Rate into three primary drivers:

**1. Activation Funnel**
- Landing Page Visit Rate
- Trial Start Rate
- Onboarding Completion Rate

**2. Revenue Quality**
- Avg Revenue Per User
- Avg Revenue Per Converted User
- Revenue by Segment

**3. User Engagement**
- Engagement Score
- Days to Convert
- Returning User Rate

**Guardrail Metrics:**
- Refund Rate (threshold: < 2%)
- Support Ticket Rate (threshold: < 15%)
- Revenue Per Converted User quality
- Segment-level conversion decline

See `outputs/kpi_tree.png` for the full visual.

---

## 5. Experiment Analysis Approach

**Data Cleaning Steps (documented in `analysis/experiment_analysis.xlsx` → Data Quality sheet):**
- Verified no duplicate user IDs
- Found and flagged 18 missing `device_type` values and 24 missing `traffic_source` values — retained in analysis with appropriate handling
- 1,336 missing `days_to_convert` records — expected, as only converted users have this value (72 total converters)
- 14 missing `engagement_score` records — excluded from engagement averages
- Validated all binary columns (0/1 only, no invalid values)
- Checked revenue for outliers — retained all values, high-revenue users are legitimate
- Confirmed segment distribution is balanced between Control and Treatment

**Analysis performed:**
- Computed all 11 required metrics by group
- Segment analysis by Region, Device Type, and Traffic Source
- Hypothesis test on primary metric

---

## 6. Hypothesis Test Summary

**Test:** Two-Proportion Z-Test (One-Tailed)  
**H₀:** Paid conversion rate in Treatment ≤ Control  
**H₁:** Paid conversion rate in Treatment > Control  
**Significance level:** α = 0.05

| Result | Value |
|--------|-------|
| Control Conversion Rate | 3.17% (22/693) |
| Treatment Conversion Rate | 6.99% (50/715) |
| Z-Statistic | 3.2519 |
| P-Value (one-tailed) | 0.000573 |
| Decision | **Reject H₀** |

The conversion improvement is **statistically significant at the 99.9% confidence level**. See full details in `analysis/hypothesis_test_notes.md`.

---

## 7. Guardrail Metrics Considered

| Guardrail Metric | Control | Treatment | Risk Level |
|------------------|---------|-----------|------------|
| Refund Rate | 0.00% | 0.42% | LOW — watch |
| Support Ticket Rate | 14.72% | 24.76% | HIGH — exceeds threshold |
| Avg Rev Per Converted User | $1,630 | $770 | MEDIUM — monitor |
| Segment Conversion Decline | None | None | PASS |

The support ticket rate surge is the primary concern and requires immediate investigation post-launch.

---

## 8. Final Recommendation

**LAUNCH — with phased rollout and active monitoring**

The new campaign delivers a statistically significant 120% improvement in paid conversion rate (3.17% → 6.99%, p = 0.0006). All regions, device types, and plan types show positive lift. Users engage more and convert faster.

However, the support ticket rate must be monitored and root-caused within 30 days of launch.

---

## 9. Assumptions and Limitations

- Experiment groups are assumed to be randomly and independently assigned
- Revenue represents 30-day window only; long-term LTV effects are unknown
- Missing data (18 device, 24 traffic source) is assumed to be missing at random
- Social traffic segment shows slight underperformance in Treatment — may need targeted optimization
- No information on experiment duration, which could introduce seasonal bias

---

## 10. Screenshots Included

| File | Contents |
|------|----------|
| `screenshots/summary_metrics.png` | Control vs Treatment metrics comparison table |
| `screenshots/hypothesis_test_output.png` | Z-test inputs, outputs, and decision |
| `screenshots/kpi_tree_preview.png` | KPI tree visual |

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
