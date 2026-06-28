# Hypothesis Test Notes
## Experiment: Onboarding & Activation Campaign
**Author:** Gaurav Karwa | bitsom_ba_2511408

---

## 1. Business Context

The company ran an A/B test comparing a **new onboarding and activation campaign** (Treatment) against the **existing onboarding experience** (Control). Leadership needs statistically valid evidence before rolling out the new campaign company-wide.

---

## 2. Metric Being Tested

**Primary Metric:** Paid Conversion Rate  
*(Proportion of users who converted to a paid plan within 30 days)*

**Reason for choosing this metric:**
- Paid conversion rate is the North Star metric because it directly measures the experiment's core objective — turning trial/free users into paying customers.
- It captures the full funnel outcome (visit → trial → onboard → pay).
- It directly impacts revenue and business growth.
- Other metrics (landing page visits, trial starts) are leading indicators but do not confirm business value without actual payment.

---

## 3. Hypotheses

**Null Hypothesis (H₀):**  
The paid conversion rate in the Treatment group is less than or equal to the paid conversion rate in the Control group.  
`H₀: p_treatment ≤ p_control`

**Alternate Hypothesis (H₁):**  
The paid conversion rate in the Treatment group is greater than the paid conversion rate in the Control group.  
`H₁: p_treatment > p_control`

---

## 4. Test Configuration

| Parameter | Value |
|-----------|-------|
| Test Type | Two-Proportion Z-Test |
| Tails | **One-tailed** (we only care if Treatment is *better*) |
| Significance Level (α) | **0.05** (5%) |
| Confidence Level | 95% |
| Metric | Paid Conversion Rate |

**Reason for one-tailed test:**  
The business question is directional — we want to know if the new campaign *improves* conversion. A two-tailed test would waste statistical power on detecting declines, which is not the decision at hand.

---

## 5. Test Inputs

| Input | Control | Treatment |
|-------|---------|-----------|
| Group Size (n) | 693 | 715 |
| Conversions | 22 | 50 |
| Conversion Rate (p) | 3.1746% | 6.9930% |

**Pooled Proportion:**
```
p̂ = (22 + 50) / (693 + 715) = 72 / 1408 = 0.05114
```

**Standard Error:**
```
SE = sqrt(p̂ × (1 - p̂) × (1/n1 + 1/n2))
SE = sqrt(0.05114 × 0.94886 × (1/715 + 1/693))
SE = sqrt(0.05114 × 0.94886 × 0.002837)
SE = 0.011744
```

**Z-Statistic:**
```
Z = (p_treatment - p_control) / SE
Z = (0.06993 - 0.03175) / 0.011744
Z = 0.03818 / 0.011744
Z = 3.2519
```

---

## 6. Test Output

| Output | Value |
|--------|-------|
| Z-Statistic | **3.2519** |
| P-Value (one-tailed) | **0.000573** |
| Critical Z at α=0.05 | 1.645 |

---

## 7. Decision Rule

- If P-value < α (0.05) → **Reject H₀** → Treatment is statistically significantly better
- If P-value ≥ α (0.05) → **Fail to reject H₀** → Insufficient evidence of improvement

**Result:** P-value = 0.000573 < 0.05 → **REJECT H₀**

---

## 8. Business Interpretation

The Treatment group's paid conversion rate of **6.99%** is statistically significantly higher than the Control group's **3.17%** — a **+3.82 percentage point lift (+120% relative improvement)**.

The probability of observing this result by chance (if there were no true difference) is only **0.057%**, far below the 5% threshold.

**This provides strong statistical evidence that the new onboarding campaign causes a meaningful improvement in paid conversions.**

---

## 9. Caveats

- The test assumes **independence** between users — no cross-contamination between Control and Treatment groups.
- The test assumes **stable user unit randomization** throughout the experiment window.
- Revenue per converted user was lower in Treatment ($770 vs $1,630 in Control), which warrants guardrail monitoring even though the overall conversion lift is significant.
- Support ticket rate increased significantly in Treatment (24.76% vs 14.72%), which may indicate onboarding friction that should be resolved before full rollout.
