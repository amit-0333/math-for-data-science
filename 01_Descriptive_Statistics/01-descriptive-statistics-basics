# Session 1 — Descriptive Statistics

## 1. What is Statistics?

Statistics is a branch of mathematics involving the **collection, analysis, interpretation, and presentation of data**. It gives us tools to make sense of large amounts of data and to draw conclusions/decisions from it.

**Applications:**
| Field | Example |
|---|---|
| Business | Customer behavior analysis, demand forecasting |
| Medical | Clinical trials (drug efficacy), epidemiology (risk factors) |
| Government & Politics | Surveys, polling |
| Environmental Science | Climate research |

---

## 2. Types of Statistics

### Descriptive Statistics
Deals with **collecting, organizing, analyzing, interpreting, and presenting** data. It **summarizes and describes** the main features of a dataset — no inference about a larger population is made.

### Inferential Statistics
Deals with making **conclusions and predictions about a population based on a sample**. Uses probability theory to estimate likelihoods, hypothesis testing to validate claims, and regression to study relationships between variables.

**Topics under Inferential Statistics:**
1. **Hypothesis Testing** — testing a claim about a population parameter (e.g., is mean height different from a given value?)
2. **Confidence Intervals** — estimating a range for a population parameter
3. **ANOVA (Analysis of Variance)** — comparing means across multiple groups
4. **Regression Analysis** — modeling relationship between dependent & independent variables
5. **Chi-Square Tests** — testing independence between categorical variables
6. **Sampling Techniques** — ensuring sample representativeness (e.g., random sampling)
7. **Bayesian Statistics** — updating probability of an event given new evidence

> **Why is ML closely tied to statistics?** Most ML algorithms are built on statistical foundations — regression, probability distributions, hypothesis testing (A/B tests), and inference are core to model building, evaluation, and validation.

---

## 3. Population vs Sample

| Term | Definition | Example |
|---|---|---|
| **Population** | The entire group of interest | All students in a school |
| **Sample** | A subset of the population selected for study | 100 randomly selected students |

**Things to be careful about while creating samples:**
- **Sample size** — too small a sample gives unreliable estimates
- **Randomness** — every member should have an equal chance of selection
- **Representativeness** — the sample should reflect the population's diversity

### Parameter vs Statistic
- **Parameter** → characteristic of a **population** (usually unknown, e.g., population mean `μ`)
- **Statistic** → characteristic of a **sample** (computed, e.g., sample mean `x̄`)
- Goal of statistical inference: use the statistic to estimate the parameter.

---

## 4. Types of Data

```
                     Types of Data
                    /              \
     Categorical (Qualitative)   Numerical (Quantitative)
        /            \                /            \
   Nominal        Ordinal        Discrete       Continuous
 (Male/Female)  (Bad/Avg/Good)   (Age, Rank)     (Weight, Height)
```

- **Nominal data** — categories with no inherent order (e.g., gender: male/female)
- **Ordinal data** — categories with a meaningful order but no fixed numeric gap (e.g., bad/average/good, rank)
- **Discrete data** — countable numeric values (e.g., age, number of children)
- **Continuous data** — measurable values on a continuum (e.g., weight, height, temperature)

---

## 5. Measures of Central Tendency

A single value that represents the "typical" or central value of a dataset.

### 5.1 Mean
Sum of all values divided by count.

**Population Mean:**
```
μ = (Σ xᵢ) / N        (i = 1 to N)
```
**Sample Mean:**
```
x̄ = (Σ xᵢ) / n        (i = 1 to n)
```
where `N` = population size, `n` = sample size.

*Example:* Data = 3, 4, 1, 2, 5 → Mean = 15/5 = **3**

### 5.2 Median
The middle value when data is sorted in order.
- Odd count → middle element
- Even count → average of the two middle elements

**How to use it — step by step:**
*Example 1 (odd count):* Data = 7, 2, 9, 4, 5
1. Sort: 2, 4, 5, 7, 9
2. Count = 5 (odd) → middle position = (5+1)/2 = 3rd value
3. Median = **5**

*Example 2 (even count):* Data = 7, 2, 9, 4
1. Sort: 2, 4, 7, 9
2. Count = 4 (even) → average the 2nd and 3rd values
3. Median = (4 + 7) / 2 = **5.5**

### 5.3 Mode
The value that occurs **most frequently** in the dataset.

**How to use it — step by step:**
Data = 2, 3, 3, 5, 3, 7, 5
1. Count occurrences: 2→1, 3→3, 5→2, 7→1
2. The value with the highest count is 3 (appears 3 times)
3. Mode = **3**

*(A dataset can have more than one mode — e.g., if 3 and 5 both appeared 3 times, it would be "bimodal" with modes 3 and 5.)*

### 5.4 Weighted Mean
Used when values have different importance/frequency:
```
Weighted Mean = Σ(wᵢ · xᵢ) / Σ wᵢ
```

**How to use it — step by step:**
*Example:* A student's final grade is based on: Assignments (20% weight, scored 80), Midterm (30% weight, scored 70), Final Exam (50% weight, scored 90)
1. Multiply each score by its weight: (80×0.20) + (70×0.30) + (90×0.50) = 16 + 21 + 45 = 82
2. Since weights already sum to 1 (100%), no further division is needed
3. Weighted Mean (final grade) = **82**

*(If weights don't sum to 1 — e.g., raw frequencies instead of percentages — divide the total by the sum of the weights, as shown in the formula.)*

### 5.5 Trimmed Mean
Remove a fixed percentage of the smallest and largest values, then take the mean of what remains. This reduces the effect of outliers.

*Example:* Salaries: 20k, 22k, 23k, 25k, 28k, 30k, 32k, 35k, 50k, 80k
- Full mean ≈ $36,500 (skewed by 50k, 80k outliers)
- After trimming top/bottom 20% → remaining: 25k, 28k, 30k, 32k, 35k → Trimmed Mean = **$30,000** (more robust to outliers)

### When to use which?
| Situation | Best measure |
|---|---|
| Symmetric data, no outliers | Mean |
| Skewed data / outliers present | Median or Trimmed Mean |
| Categorical data | Mode |
| Values with different weights/importance | Weighted Mean |

---

## 6. Measures of Dispersion

Describes the **spread/variability** of data around the central tendency.

### 6.1 Range
```
Range = Max value − Min value
```
Simple but very sensitive to outliers.

**How to use it — step by step:**
Data = 4, 8, 15, 16, 23, 42
1. Find Max = 42, Min = 4
2. Range = 42 − 4 = **38**

### 6.2 Variance
Average of squared differences between each data point and the mean.

**Population Variance:**
```
σ² = Σ(xᵢ − μ)² / N
```
**Sample Variance:**
```
s² = Σ(xᵢ − x̄)² / (n − 1)
```
> Note: Sample variance divides by `n − 1` (Bessel's correction) instead of `n` to correct the bias that arises from estimating the mean from the same sample — this gives an unbiased estimator of the population variance.

**How to use it — step by step:**
Data = 3, 2, 1, 5, 4 (treat as a sample)
1. Find the mean: (3+2+1+5+4)/5 = 15/5 = **3**
2. Subtract the mean from each value (deviations): 3−3=0, 2−3=−1, 1−3=−2, 5−3=2, 4−3=1
3. Square each deviation: 0², (−1)², (−2)², 2², 1² = 0, 1, 4, 4, 1
4. Sum the squared deviations: 0+1+4+4+1 = **10**
5. Divide by (n−1) since this is a sample: 10 / (5−1) = 10/4 = **2.5**
6. Sample Variance = **2.5**

*(If this were the full population instead of a sample, you'd divide by N=5 instead of n−1=4, giving Population Variance = 10/5 = 2.0)*

### 6.3 Standard Deviation
Square root of variance — brings the unit back to the same scale as the original data.
```
σ = √(Σ(xᵢ − μ)² / N)         (population)
s = √(Σ(xᵢ − x̄)² / (n − 1))   (sample)
```

**How to use it — step by step:**
Continuing the same data (3, 2, 1, 5, 4), we already calculated Sample Variance = 2.5
1. Take the square root of the variance: √2.5 = **≈ 1.58**
2. Sample Standard Deviation = **≈ 1.58**

This tells us: on average, each data point is about 1.58 units away from the mean (3).

### 6.4 Mean Absolute Deviation (MAD)
```
MAD = Σ|xᵢ − x̄| / n
```
Uses absolute differences instead of squared differences — more intuitive but less mathematically convenient (not differentiable at 0).

**How to use it — step by step:**
Same data: 3, 2, 1, 5, 4 → mean = 3
1. Take absolute deviations (ignore sign): |3−3|=0, |2−3|=1, |1−3|=2, |5−3|=2, |4−3|=1
2. Sum them: 0+1+2+2+1 = **6**
3. Divide by n (=5): 6/5 = **1.2**
4. MAD = **1.2**

### 6.5 Coefficient of Variation (CV)
Ratio of standard deviation to mean, expressed as a percentage. Useful to compare variability **across datasets with different units/means**.
```
CV = (σ / μ) × 100%
```
Commonly used in biology, chemistry, and engineering.

**How to use it — step by step:**
*Example:* Two classes take a test.
- Class A: mean = 70, SD = 10
- Class B: mean = 40, SD = 8

Class B has a smaller SD, so it looks "less variable" at first glance — but the means are very different, so we can't compare SDs directly. Use CV instead:
1. CV(A) = (10/70) × 100 = **14.3%**
2. CV(B) = (8/40) × 100 = **20%**
3. Even though Class B's raw SD is smaller, its scores are actually **more variable relative to its own mean** (20% vs 14.3%).

---

## 7. Graphs for Univariate Analysis

### 7.1 Categorical Data — Frequency Distribution & Cumulative Frequency
A **frequency distribution table** summarizes how often each category occurs.

*Example (survey of 200 people on vacation preference):*
| Type | Frequency | Relative Frequency | Cumulative Frequency |
|---|---|---|---|
| Beach | 60 | 0.30 | 60 |
| City | 40 | 0.20 | 100 |
| Adventure | 30 | 0.15 | 130 |
| Nature | 35 | 0.175 | 165 |
| Cruise | 20 | 0.10 | 185 |
| Other | 15 | 0.075 | 200 |

- **Relative frequency** = frequency / total observations
- **Cumulative frequency** = running total of frequencies

### 7.2 Numerical Data — Frequency Distribution & Histogram
Numeric data is grouped into **bins/buckets** (e.g., age ranges 0–10, 11–20, 21–30...) and plotted as a **histogram**.

**Shapes of a Histogram:**
- **Symmetric** — balanced around the center
- **Bimodal** — two peaks
- **Left Skew** — long tail on the left (mean < median)
- **Right Skew** — long tail on the right (mean > median)
- **Uniform** — roughly equal frequency across bins
- **No Pattern** — random, no clear distribution shape

---

## 8. Graphs for Bivariate Analysis

| Variable Combination | Graph Type |
|---|---|
| Categorical – Categorical | **Contingency Table / Crosstab** — summarizes relationship between two categorical variables using rows & columns |
| Numerical – Numerical | **Scatter Plot** — shows relationship/trend between two numeric variables |
| Categorical – Numerical | Side-by-side box plots, bar charts (grouped by category) |

---

## Additional Notes (Beyond the Session Content)

### Other Measures of Central Tendency
- **Geometric Mean** — used for growth rates, ratios: `GM = (x₁·x₂·...·xₙ)^(1/n)`
- **Harmonic Mean** — used for rates (e.g., speed): `HM = n / Σ(1/xᵢ)`

### Skewness & Kurtosis (preview — covered in depth later)
- **Skewness** measures asymmetry of the distribution (0 = symmetric, >0 = right-skewed, <0 = left-skewed)
- **Kurtosis** measures "tailedness" — how much data is in the tails vs the center

### Quick Python Reference
```python
import numpy as np
import pandas as pd
from scipy import stats

data = [3, 4, 1, 2, 5, 78, 82, 84]

np.mean(data)          # Mean
np.median(data)        # Median
stats.mode(data)        # Mode
np.var(data, ddof=1)   # Sample variance (ddof=1 -> divide by n-1)
np.std(data, ddof=1)   # Sample standard deviation
stats.trim_mean(data, 0.1)  # Trimmed mean (10% each side)
stats.variation(data)  # Coefficient of variation
```

### Why Descriptive Statistics Matters for Data Science
- First step of any **EDA (Exploratory Data Analysis)** pipeline
- Helps detect **outliers, skewness, and data quality issues** before modeling
- Central tendency & dispersion measures directly feed into **feature scaling** (standardization uses mean & std dev) and **outlier detection** (IQR, z-scores — covered in Session 2)
