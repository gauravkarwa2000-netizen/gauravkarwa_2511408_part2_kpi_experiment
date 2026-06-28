# Recommendation Memo
## Campaign: New Onboarding & Activation Experience
**To:** Leadership Team  
**From:** Gaurav Karwa | Business Analyst | bitsom_ba_2511408  
**Date:** June 2025  
**Subject:** A/B Test Results & Launch Recommendation

---

## 1. Executive Summary

The new onboarding and activation campaign (Treatment) produced a **statistically significant 120% improvement in paid conversion rate** compared to the existing experience (Control) — 6.99% vs 3.17% (Z = 3.25, p = 0.0006). This result is highly significant and warrants a launch recommendation.

However, guardrail metrics reveal two concerns:
- **Support ticket rate** nearly doubled in the Treatment group (14.72% → 24.76%)
- **Revenue per converted user** dropped significantly ($1,630 → $770)

**Recommendation: Phased launch — roll out to all users with parallel monitoring of guardrail metrics, and initiate a fast-follow investigation into support ticket drivers and revenue quality.**

---

## 2. North Star Metric

**Paid Conversion Rate** — the proportion of users who converted from free/trial to a paid plan within 30 days.

This metric was selected because:
- It directly measures the campaign's stated objective (conversion improvement)
- It captures the full funnel outcome, not just early-stage engagement
- It is the most direct driver of subscription revenue growth
- It is actionable and observable within the 30-day experiment window

**Risk of blind optimization:** Optimizing only for conversion rate could lead to lower-quality conversions (lower revenue per user, higher churn) or create a degraded support experience. This is why guardrail metrics must be monitored alongside the North Star.

---

## 3. KPI Tree Explanation

The KPI tree breaks Paid Conversion Rate into three primary driver pillars:

**Pillar 1 — Activation Funnel**
- Landing Page Visit Rate → Trial Start Rate → Onboarding Completion Rate → Conversion
- Treatment improved all three funnel steps vs Control

**Pillar 2 — Revenue Quality**
- Avg Revenue Per User, Avg Revenue Per Converted User, Revenue by Segment
- Mixed results: total revenue per user slightly up (+$2.13), but per-converter revenue fell sharply

**Pillar 3 — User Engagement**
- Engagement Score, Days to Convert, Returning User Rate
- Treatment users are more engaged (score: 62.93 vs 57.03) and convert faster (6.4 vs 8.9 days)

**Guardrail Metrics (must not breach thresholds):**
- Refund Rate < 2%
- Support Ticket Rate < 15%
- Revenue Per Converted User (monitor for decline)
- Segment-level conversion decline

---

## 4. Experiment Result Summary

| Metric | Control | Treatment | Change |
|--------|---------|-----------|--------|
| Users | 693 | 715 | +22 |
| Landing Page Visit Rate | 63.64% | 72.59% | +8.95pp |
| Trial Start Rate | 25.11% | 29.09% | +3.98pp |
| Onboarding Completion Rate | 15.58% | 21.26% | +5.68pp |
| **Paid Conversion Rate** | **3.17%** | **6.99%** | **+3.82pp (+120%)** |
| Avg Revenue Per User | $51.75 | $53.88 | +$2.13 |
| Avg Revenue Per Converted User | $1,630.10 | $770.41 | -$859.69 |
| Refund Rate | 0.00% | 0.42% | +0.42pp |
| Support Ticket Rate | 14.72% | 24.76% | +10.04pp |
| Avg Engagement Score | 57.03 | 62.93 | +5.90 |
| Avg Days to Convert | 8.86 | 6.40 | -2.46 days |

---

## 5. Hypothesis Test Interpretation

**Test:** Two-proportion Z-test (one-tailed)  
**H₀:** p_treatment ≤ p_control  
**H₁:** p_treatment > p_control  
**Significance level:** α = 0.05

| Result | Value |
|--------|-------|
| Z-Statistic | 3.2519 |
| P-Value | 0.000573 |
| Decision | Reject H₀ |

The probability that this improvement occurred by chance is only 0.057%. The conversion improvement in the Treatment group is **statistically significant at the 99.9% confidence level**. The experiment has provided strong, valid evidence that the new campaign works.

---

## 6. Guardrail Analysis

| Guardrail Metric | Control | Treatment | Status |
|------------------|---------|-----------|--------|
| Refund Rate | 0.00% | 0.42% | WATCH — new refunds appeared |
| Support Ticket Rate | 14.72% | 24.76% | ALERT — exceeds 15% threshold |
| Avg Rev / Converted User | $1,630 | $770 | ALERT — 52% drop in revenue quality |
| Segment-level decline | No segments below Control | No net declines | PASS |

**Key concern:** The support ticket rate at 24.76% significantly exceeds the 15% guardrail threshold. This suggests the new onboarding may be confusing for some users even as it drives more conversions. This does not warrant blocking launch, but it requires immediate investigation into the ticket topics.

The drop in revenue per converted user may reflect the different mix of users converting — Treatment attracts a broader set of lower-tier plan subscribers (especially Free plan users converting at 9.24% vs Control's 3.05%). This is not necessarily negative — it could represent successful democratization of the product.

---

## 7. Segment-Level Insights

**By Region:**
- Treatment outperformed Control in all four regions
- Strongest lift: North (3.45% → 8.89%) and South (3.26% → 7.61%)
- West shows the smallest lift (3.38% → 5.03%) — could warrant targeted optimization

**By Device Type:**
- All device types improved with Treatment
- Mobile and Tablet showed strong conversion lifts
- Treatment is particularly effective for Mobile users (2.57% → 7.34%)

**By Traffic Source:**
- Biggest uplift from Referral traffic (2.47% → 10.99%) — a 4.5x improvement
- Social traffic showed a small decline in Treatment (7.69% → 6.02%) — only potential concern
- Paid Search and Organic both improved significantly

**By Plan Type:**
- Free plan users showed the largest relative uplift (3.05% → 9.24%)
- Basic and Premium plans also improved meaningfully
- No segment showed a decline below the corresponding Control rate (except Social source, minor)

---

## 8. Final Recommendation

### Launch with Monitoring

**Decision: Launch — with a phased rollout and guardrail monitoring protocol**

**Rationale:**
1. The conversion improvement (+120%) is statistically significant with p < 0.001
2. All four regions, all device types, and all plan types show positive lift
3. Revenue per user improved slightly (+$2.13)
4. Users convert faster (6.4 vs 8.9 days) and engage more (score 62.93 vs 57.03)

**Conditions for full launch:**
- Begin 30-day monitoring post-launch focusing on support ticket volume and refund rate
- Investigate support tickets from Treatment group to identify friction points
- Address the Social traffic segment's minor conversion dip in follow-up optimization

---

## 9. Risks and Limitations

1. **Support ticket surge** (24.76%): If this persists at scale, it will increase Customer Support costs and may erode user satisfaction (NPS/CSAT impact)
2. **Revenue per converter drop**: If Treatment users churn faster or stay on lower-tier plans, LTV may not justify acquisition cost — recommend 90-day cohort revenue tracking
3. **Experiment duration**: The exact experiment window is not disclosed — if < 4 weeks, some seasonal effects may be present
4. **Missing data**: 18 missing device_type, 24 missing traffic_source records — small but could introduce minor bias in segment analysis
5. **Social source decline**: Treatment appears less effective for Social traffic — may need a variant specifically designed for this channel
6. **Sample size**: While statistically sufficient, 1,408 users may not fully represent all user personas at scale

---

## 10. Next Steps

| Priority | Action | Owner | Timeline |
|----------|--------|-------|----------|
| HIGH | Full rollout to all new users | Product & Engineering | Within 1 week |
| HIGH | Monitor support tickets daily for 30 days | Customer Success | Ongoing |
| HIGH | Analyze what drives support tickets in Treatment | Product | 2 weeks |
| MEDIUM | Track 90-day revenue and churn cohort for Treatment converters | Analytics | 90 days |
| MEDIUM | Run targeted Social-source optimization experiment | Growth | Next sprint |
| LOW | Explore West region underperformance with qualitative research | UX Research | Next quarter |
