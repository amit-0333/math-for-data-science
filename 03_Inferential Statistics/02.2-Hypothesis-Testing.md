# Session 2 — Hypothesis Testing (P-value & T-tests)

> **Suggested folder:** `Inferential Statistics` (or a dedicated `Hypothesis Testing` folder). This content is neither pure "Descriptive Statistics" nor pure "Probability & Distributions" — it's the inferential-statistics bridge between the two.

---

## Table of Contents

1. [P-value](#p-value)
2. [Interpreting P-value](#interpreting-p-value)
3. [P-value in Context of Z-Test](#p-value-in-context-of-z-test)
4. [T-tests — Overview](#t-tests--overview)
5. [Single Sample T-test](#single-sample-t-test)
6. [Independent Two-Sample T-test](#independent-two-sample-t-test)
7. [Paired Two-Sample T-test](#paired-two-sample-t-test)
8. [Additional Notes (Beyond the Session Content)](#additional-notes-beyond-the-session-content)

---

## P-value

**Definition:** The p-value is the probability of getting a sample **as extreme or more extreme** (i.e., having as much or more evidence against H0) than our own observed sample, **given that the null hypothesis (H0) is true**.

**In simple words:** The p-value is a **measure of the strength of evidence against H0** provided by the sample data. The smaller the p-value, the stronger the evidence against H0.

```
Binomial Distribution of Coin Tosses (100 tosses, testing a fair coin)
P(H) = P(T) under H0.  Observed: 53 heads.  P-value = P(getting ≥53 heads | fair coin)

Probability
0.08 |                    ▓▓
0.07 |                  ▓▓▓▓▓▓
0.06 |                ▓▓▓▓▓▓▓▓▓▓
0.05 |              ▓▓▓▓▓▓▓▓▓▓▓▓▓▓
0.04 |            ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░
0.03 |          ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░
0.02 |        ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░
0.01 |      ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░░░
0.00 |____▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░░░░░░░░░░░░
       0        20        40  50  53(→)  65  80
       ▓ = bulk of distribution (not extreme)
       ░ = "as extreme or more extreme" region → shaded area = p-value
```

### How to use it — step by step

**Worked example:** You flip a coin 100 times, testing H0: the coin is fair (P(Heads) = P(Tails) = 0.5). You observe 53 heads.

1. Build the sampling distribution of "number of heads out of 100 flips" **assuming H0 is true** (a Binomial(n=100, p=0.5) distribution).
2. Find P(X ≥ 53), the probability of getting 53 or more heads just by chance, if the coin really is fair.
3. Using the normal approximation to the binomial: mean = np = 50, std = √(np(1−p)) = √(100×0.5×0.5) = 5.
   ```
   Z = (53 − 50) / 5 = 0.6
   P(X ≥ 53) ≈ P(Z ≥ 0.6) ≈ 0.274 (one-tailed)
   ```
4. This computed value (~0.27, in the same ballpark as the "P-value: 0.072" and "7.2%" annotations sketched for related scenarios in the original notes) is your **p-value**.
5. Since this p-value is fairly large, it represents **weak evidence** against fairness — we'd fail to reject H0.

> Note: the original handwritten notes sketch several related scenarios (65 heads out of 100 flips, 53 heads assuming P=0.3, 80 heads out of 100, etc.) to build intuition that **the further the observed count is from the expected mean under H0, the smaller (more extreme) the p-value becomes**, and the stronger the evidence against H0.

---

## Interpreting P-value

| P-value range              | Strength of evidence against H0                                              |
|-----------------------------|-------------------------------------------------------------------------------|
| p < 0.01 (very small)        | **Strong** evidence against H0 — unlikely due to chance alone                |
| 0.01 ≤ p < 0.05 (small)       | **Moderate** evidence against H0 — less likely due to chance alone           |
| 0.05 ≤ p < 0.1 (large)        | **Weak** evidence against H0 — might be due to chance, some uncertainty      |
| p ≥ 0.1 (very large)          | **Weak or no** evidence against H0 — likely due to chance alone              |

```
Evidence strength as p-value shrinks →

|--------|--------|--------|--------|--------|
0      0.01     0.05      0.1              1.0
Strong  |Moderate|  Large (weak) | Very large (none)
evidence|evidence|   evidence    |    evidence
against |against |   against    |    against
  H0    |  H0    |     H0        |      H0
```

### How to use it — step by step
1. Compute your p-value (from a Z-test, t-test, etc.).
2. Compare it to your pre-chosen significance level α (commonly 0.05).
3. **If p-value < α** → reject H0 (statistically significant result).
4. **If p-value ≥ α** → fail to reject H0 (not statistically significant).

**Numeric example:** If a test gives p = 0.03 and you set α = 0.05, then p < α, so you **reject H0** — this falls in the "small p-value, moderate evidence" band above.

---

## P-value in Context of Z-Test

Two illustrative examples were used to compute p-values directly instead of just comparing to a critical value.

### How to use it — step by step (Example A — Training Program, σ = 4)

**Scenario:** Average productivity was 50 units/day. After training, a sample of n = 30 has mean = 53 units/day, population std σ = 4.

1. **Hypotheses:** H0: μ = 50, Ha: μ > 50 (one-sided)
2. **Test statistic:**
   ```
   Z = (53 − 50) / (4 / √30) = 3 / 0.730 = 4.11
   ```
3. **P-value (one-tailed):** P(Z ≥ 4.11) ≈ **0.00002** (extremely small)
4. **Decision:** Since p ≈ 0.00002 ≪ 0.05, **reject H0** — very strong evidence the training program increased productivity.

```
Standard Normal Curve — shaded p-value region, one-tailed test

Probability
   |                    ___
   |                 __/   \__
   |               _/         \_
   |             _/             \_
   |           _/                 \_
   |_________/_____________________\________________ Z
        -3     0        1.645              4.11 ↑
                                              (observed Z,
                                          p-value ≈ tiny sliver
                                          of area beyond this point)
```

### How to use it — step by step (Example B — Lays Wafer Weight, σ = 5)

**Scenario:** Claimed average weight = 50g. A sample of n = 40 has mean = 49g, population std σ = 5.

1. **Hypotheses:** H0: μ = 50, Ha: μ ≠ 50 (two-sided)
2. **Test statistic:**
   ```
   Z = (49 − 50) / (5 / √40) = −1 / 0.7906 = −1.265
   ```
3. **P-value (two-tailed):** 2 × P(Z ≤ −1.265) ≈ 2 × 0.103 = **0.206**
4. **Decision:** Since p ≈ 0.206 > 0.05, **fail to reject H0** — the weight difference could plausibly be due to chance ("large p-value / weak evidence" band from the table above).

> Note: this uses the same style of scenario as the classic Z-test rejection-region example, but with a different assumed σ (5g here) — a good reminder that **σ (or s) is a critical input** that changes your conclusion, so always double-check which standard deviation value you're given.

---

## T-tests — Overview

A **t-test** is used in hypothesis testing to compare the means of two samples, or a sample mean to a known population mean — **when the population standard deviation is unknown and the sample size is small**. It's based on the **t-distribution** (which has heavier tails than the normal distribution, to account for the extra uncertainty of estimating σ from the sample itself).

There are three main types:
1. **One-sample t-test** — compares one sample's mean to a known/hypothesized population mean.
2. **Independent two-sample t-test** — compares the means of two independent (unrelated) samples.
3. **Paired t-test (dependent two-sample t-test)** — compares means of two related/paired samples (e.g., before-and-after on the same subjects).

```
Normal distribution vs t-distribution (heavier tails)

Normal (Z):                       t-distribution (small df):
        ___                              __
     __/   \__                        __/  \__
   _/         \_                    _/        \_
 _/             \_                _/            \_
/                 \              /                \
(thin tails,                    (fatter tails — more probability
narrower spread)                 in the extremes, to allow for
                                  extra uncertainty in small samples)
```

---

## Single Sample T-test

Checks whether a sample mean differs from a known/claimed population mean, when **σ is unknown**.

**Formula:**

```
        x̄ − μ
t  =  ──────────      with degrees of freedom (df) = n − 1
        s / √n
```

Where `s` = **sample** standard deviation (estimated, not the true population σ).

**Assumptions:**
1. **Normality** — the population the sample is drawn from is normally distributed.
2. **Independence** — one observation doesn't influence another.
3. **Random Sampling** — the sample is a random, representative subset of the population.
4. **Unknown population std** — this is what distinguishes it from a Z-test.

### How to use it — step by step

**Scenario:** A manufacturer claims chocolate bars average 50 grams. A sample of n = 25 bars has sample mean = 49.7g and sample std dev s = 1.2g. Significance level α = 0.05.

1. **Hypotheses:** H0: μ = 50, Ha: μ ≠ 50 (two-sided — we simply doubt the claim, no specific direction stated)
2. **α = 0.05**
3. **Check assumptions:** σ unknown, small sample (n = 25) → t-test is appropriate.
4. **Degrees of freedom:** df = n − 1 = 24
5. **Test statistic:**
   ```
   t = (49.7 − 50) / (1.2 / √25)
     = −0.3 / (1.2 / 5)
     = −0.3 / 0.24
     = −1.25
   ```
6. **Critical value:** For df = 24, two-tailed α = 0.05 → critical t ≈ **±2.064**
7. **Decision:** |−1.25| = 1.25 < 2.064 → **fail to reject H0**.
8. **Interpret:** There isn't enough evidence to say the chocolate bars differ from the claimed 50g average.

```
t-distribution, df = 24, two-tailed test at α = 0.05

           Fail to Reject H0
        ___________________________
       /                           \
      /                             \
_____/                               \_____
REJECT|         ↑                    |REJECT
(2.5%)|      t = -1.25                |(2.5%)
     -2.064   (observed,             +2.064
              inside "fail to reject" zone)
```

---

## Independent Two-Sample T-test

Also called an **unpaired t-test** — compares the means of **two independent groups** to see if there's a significant difference.

**Formula (equal variances / pooled version):**

```
                    x̄₁ − x̄₂
t  =  ──────────────────────────────────
        Sp × √(1/n₁ + 1/n₂)

where pooled variance:
        (n₁−1)s₁² + (n₂−1)s₂²
Sp² =  ─────────────────────────
              n₁ + n₂ − 2

df = n₁ + n₂ − 2
```

If variances are **not** assumed equal, use **Welch's t-test** instead (adjusted standard error and degrees-of-freedom formula — see Additional Notes below).

**Assumptions:**
1. **Independence of observations** — the two groups are unrelated, randomly and independently sampled.
2. **Normality** — each group's data is approximately normal (robust to mild violations if n ≥ 30 per group).
3. **Equal variances (Homoscedasticity)** — check via an F-test; if violated, use Welch's t-test instead.
4. **Random sampling** from each population.

### How to use it — step by step

**Scenario:** Testing whether average time spent on a website differs between two user groups.
- Group 1: n₁ = 30, mean₁ = 18.5 minutes, s₁ = 3.5 minutes
- Group 2: n₂ = 30, mean₂ = 14.3 minutes, s₂ = 2.7 minutes
- α = 0.05

1. **Hypotheses:** H0: μ₁ = μ₂ (no difference), Ha: μ₁ ≠ μ₂ (two-sided)
2. **Check assumptions:** Independent random samples, n ≥ 30 each (robust to normality), assume variances roughly equal for this pooled-variance walkthrough.
3. **Pooled variance:**
   ```
   Sp² = [(30−1)(3.5²) + (30−1)(2.7²)] / (30+30−2)
       = [29 × 12.25 + 29 × 7.29] / 58
       = [355.25 + 211.41] / 58
       = 566.66 / 58
       = 9.77
   Sp = √9.77 = 3.13
   ```
4. **Test statistic:**
   ```
   t = (18.5 − 14.3) / (3.13 × √(1/30 + 1/30))
     = 4.2 / (3.13 × 0.258)
     = 4.2 / 0.807
     = 5.20
   ```
5. **df = 30 + 30 − 2 = 58.** Critical t at α = 0.05 (two-tailed) ≈ **±2.002**
6. **Decision:** |5.20| > 2.002 → **reject H0**.
7. **Interpret:** There's a statistically significant difference in average time spent between the two groups.

```
t-distribution, df = 58, two-tailed test at α = 0.05

           Fail to Reject H0
        ___________________________
       /                           \
      /                             \
_____/                               \_____
REJECT|                             |REJECT///// t=5.20
(2.5%)|                             |(2.5%) ────────►  (way out
     -2.002        0             +2.002       in the reject zone)
```

---

## Paired Two-Sample T-test

Also called a **dependent t-test** — compares the means of **two related/paired groups** (e.g., the same subjects measured before and after an intervention).

**Formula:**

```
        d̄
t  =  ──────────      where d̄ = mean of the paired differences
        sd / √n         sd = std dev of the paired differences
                         n  = number of pairs
                         df = n − 1
```

**Common scenarios:** before-and-after studies, or matched/correlated pairs (e.g., siblings, twin studies).

**Assumptions:**
1. **Paired observations** — each pair is genuinely related (same subject, matched subjects, etc.).
2. **Normality of the differences** — the *differences* between pairs should be roughly normal (check with Q-Q plots or Shapiro-Wilk test); robust to moderate violations at large n.
3. **Independence of pairs** — one pair's outcome shouldn't affect another pair's outcome.

### How to use it — step by step

**Scenario:** A fitness center tests an 8-week weight-loss program on 15 participants, measuring weight before and after. α = 0.05.

- Before: `[80, 92, 75, 68, 85, 78, 73, 90, 70, 88, 76, 84, 82, 77, 91]`
- After: `[78, 93, 81, 67, 88, 76, 74, 91, 69, 88, 77, 81, 80, 79, 88]`

1. **Hypotheses:** H0: μ_d = 0 (no change), Ha: μ_d ≠ 0 (two-sided — testing for any change)
2. **Compute differences (Before − After)** for each of the 15 participants:
   ```
   2, -1, -6, 1, -3, 2, -1, -1, 1, 0, -1, 3, 2, -2, 3
   ```
3. **Mean of differences:**
   ```
   d̄ = (sum of differences) / 15 = −1 / 15 ≈ −0.067
   ```
4. **Std dev of differences:**
   ```
   sd ≈ 2.46  (computed from the squared deviations of each difference from d̄)
   ```
5. **Test statistic:**
   ```
   t = d̄ / (sd / √n)
     = −0.067 / (2.46 / √15)
     = −0.067 / (2.46 / 3.873)
     = −0.067 / 0.636
     = −0.105
   ```
6. **df = 15 − 1 = 14.** Critical t at α = 0.05 (two-tailed) ≈ **±2.145**
7. **Decision:** |−0.105| ≪ 2.145 → **fail to reject H0**.
8. **Interpret:** There isn't enough evidence that the weight-loss program produced a significant average change in weight (in this particular sample, the average change was tiny and inconsistent in direction across participants).

```
t-distribution, df = 14, two-tailed test at α = 0.05

           Fail to Reject H0
        ___________________________
       /                           \
      /                             \
_____/                               \_____
REJECT|      ↑                       |REJECT
(2.5%)|   t = -0.105                  |(2.5%)
     -2.145 (observed, right in                +2.145
             the middle — nowhere
             near either tail)
```

---

## Additional Notes (Beyond the Session Content)

These extra notes weren't in the original material but are useful context for practical data-science work.

### Related concepts worth knowing

- **Z-test vs t-test:** The core session covers t-tests, which are used when σ is unknown. When σ *is* known (or n is very large), you'd use a Z-test instead — same core logic, different reference distribution.
- **Welch's t-test:** The safer default choice for an independent two-sample t-test when you can't assume equal variances between groups (uses an adjusted standard error and a fractional/approximate degrees-of-freedom formula — this is what `scipy.stats.ttest_ind(..., equal_var=False)` implements).
- **Non-parametric alternatives:** When normality is badly violated, use rank-based tests instead — **Mann-Whitney U test** (alternative to independent t-test), **Wilcoxon signed-rank test** (alternative to paired t-test), **Kruskal-Wallis test** (alternative to one-way ANOVA).
- **ANOVA (Analysis of Variance):** Extends the two-sample t-test idea to **3+ groups** at once, testing whether at least one group mean differs from the others, without inflating Type I error the way running many pairwise t-tests would.
- **Multiple testing / p-hacking:** Running many hypothesis tests increases the chance of a false positive purely by chance. Corrections like **Bonferroni** or **Benjamini-Hochberg (FDR)** adjust the p-value threshold accordingly.
- **Effect size (e.g., Cohen's d):** A p-value tells you *whether* an effect is statistically significant, but not *how big* it is practically. Effect size measures the magnitude of the difference, independent of sample size.

### Common ML / data-science use cases

- **Comparing model performance across folds** — a paired t-test on cross-validation accuracy scores between two models (since the same folds are used for both models, the "paired" version is statistically more appropriate than an independent test).
- **Feature significance in regression** — the p-values reported next to each coefficient in `statsmodels` OLS output are literally one-sample t-tests of H0: coefficient = 0.
- **A/B testing with small samples** — when you can't assume σ is known or the sample is small, a t-test (rather than a Z-test) is the statistically correct choice.
- **Before/after experiment analysis** — measuring the same users/subjects before and after a product change is a textbook paired t-test scenario.

### Quick Python Reference

```python
import numpy as np
import pandas as pd
from scipy import stats
import matplotlib.pyplot as plt

# ---------------------------------------------------------
# One-sample t-test (population std unknown)
# ---------------------------------------------------------
sample_data = np.array([49.1, 50.2, 49.5, 48.9, 49.7])  # example values
t_stat, p_val = stats.ttest_1samp(sample_data, popmean=50)
print(f"t = {t_stat:.3f}, p-value = {p_val:.5f}")

# ---------------------------------------------------------
# Independent two-sample t-test
# ---------------------------------------------------------
group_a = np.array([12, 15, 18, 16, 20])   # example values
group_b = np.array([10, 12, 14, 13, 16])
t_stat, p_val = stats.ttest_ind(group_a, group_b, equal_var=True)         # pooled (equal variance)
t_stat_w, p_val_w = stats.ttest_ind(group_a, group_b, equal_var=False)    # Welch's (unequal variance)

# ---------------------------------------------------------
# Paired t-test
# ---------------------------------------------------------
before = np.array([80, 92, 75, 68, 85, 78, 73, 90, 70, 88, 76, 84, 82, 77, 91])
after  = np.array([78, 93, 81, 67, 88, 76, 74, 91, 69, 88, 77, 81, 80, 79, 88])
t_stat, p_val = stats.ttest_rel(before, after)
print(f"t = {t_stat:.3f}, p-value = {p_val:.5f}")

# ---------------------------------------------------------
# Visualizing a p-value region under H0
# ---------------------------------------------------------
x = np.linspace(-4, 4, 500)
y = stats.norm.pdf(x)
observed_z = 4.11
plt.plot(x, y)
plt.fill_between(x, y, where=(x >= observed_z), color="red", alpha=0.5, label="p-value region")
plt.axvline(observed_z, color="blue", linestyle="--", label=f"Observed Z = {observed_z}")
plt.legend()
plt.title("P-value as the shaded 'as extreme or more extreme' area")
plt.show()
```
