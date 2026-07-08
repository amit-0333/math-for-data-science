# Session 2 — Descriptive Statistics (Quantiles, Boxplots, Covariance & Correlation)

## 1. Quantiles

Quantiles divide a numerical dataset into **equal-sized groups**, each containing an equal number of observations. They help understand distribution shape, compare datasets, and identify outliers.

**Important rules:**
- Data must be **sorted** low to high before computing
- Quantiles represent a **location**, not necessarily an actual value in the data
- All quantile types can be derived from **percentiles**

| Type | Divides data into | Notation |
|---|---|---|
| Quartiles | 4 equal parts | Q1 (25th), Q2 (50th/median), Q3 (75th) |
| Quintiles | 5 equal parts | — |
| Deciles | 10 equal parts | D1...D9 |
| Percentiles | 100 equal parts | P1...P99 |

### Percentile
The percentage of observations that fall **below** a particular value.

**Formula for percentile location:**
```
PL = (p / 100) × N
```
where `PL` = desired percentile location, `N` = total number of observations, `p` = percentile rank.

**Formula for percentile rank of a given value:**
```
Percentile Rank = (X + 0.5·Y) / N × 100
```
where `X` = number of values below the given value, `Y` = number of values equal to the given value, `N` = total observations.

**How to use it — step by step:**
Find the **75th percentile** of: 78, 82, 84, 88, 91, 93, 94, 96, 98, 99 (already sorted, N = 10)

1. Plug into the formula: PL = (75/100) × 10 = **7.5**
2. Since 7.5 is not a whole number, it means the answer lies **between the 7th and 8th values**
3. 7th value = 94, 8th value = 96
4. Take the fractional part (0.5) and interpolate: 94 + 0.5 × (96 − 94) = 94 + 1 = **95**
5. So the **75th percentile = 95** → meaning 75% of the scores fall below 95

*Simpler case — when PL is a whole number:*
Find the **50th percentile (median)** of: 10, 20, 30, 40 (N = 4)
1. PL = (50/100) × 4 = **2** (a whole number, no interpolation needed here — take the average of the 2nd value and the next one as a simple median rule)
2. 2nd value = 20, 3rd value = 30 → Median = (20+30)/2 = **25**

---

## 2. Five-Number Summary

A compact summary describing a dataset using 5 values:

1. **Minimum** — smallest value
2. **Q1 (First Quartile)** — 25th percentile
3. **Q2 (Median)** — 50th percentile
4. **Q3 (Third Quartile)** — 75th percentile
5. **Maximum** — largest value

Visually represented by a **box plot**.

### Interquartile Range (IQR)
```
IQR = Q3 − Q1
```
Measures the spread of the **middle 50%** of the data — robust to outliers.

**How to use it — step by step:**
Sorted data: 6, 213, 241, 260, 281, 290, 314, 321, 350, 1500 (N = 10, positions 1–10)

*(Note: this method uses N+1 = 11 in the formula — a common convention that leaves room to interpolate between positions.)*

**Step 1 — Find Q2 (Median):**
1. Position = (50/100) × 11 = 5.5
2. That's halfway between the 5th value (281) and 6th value (290)
3. Q2 = (281 + 290)/2 = **285.5**

**Step 2 — Find Q1:**
1. Position = (25/100) × 11 = 2.75
2. That's between the 2nd value (213) and 3rd value (241), 0.75 of the way across
3. Q1 = 213 + 0.75 × (241 − 213) = 213 + 21 = **234**

**Step 3 — Find Q3:**
1. Position = (75/100) × 11 = 8.25
2. That's between the 8th value (321) and 9th value (350), 0.25 of the way across
3. Q3 = 321 + 0.25 × (350 − 321) = 321 + 7.25 = **328.25**

**Step 4 — Calculate IQR:**
```
IQR = Q3 − Q1 = 328.25 − 234 = 94.25
```

### Outlier Boundaries (used in box plots)
```
Lower bound = Q1 − 1.5 × IQR
Upper bound = Q3 + 1.5 × IQR
```
Any value outside these bounds is considered a potential **outlier**.

**How to use it — step by step:**
Using Q1 = 234, Q3 = 328.25, IQR = 94.25 from above:
1. Lower bound = Q1 − 1.5 × IQR = 234 − 1.5×94.25 = 234 − 141.375 = **≈ 93**
2. Upper bound = Q3 + 1.5 × IQR = 328.25 + 1.5×94.25 = 328.25 + 141.375 = **≈ 469**
3. Check each data point against these bounds: 6 is below 93 → **outlier**. 1500 is above 469 → **outlier**. All other values (213 to 350) fall inside the range → normal.

---

## 3. Boxplots (Box-and-Whisker Plot)

A graphical representation showing:
- Minimum & Maximum (whiskers, unless outliers exist)
- Q1, Median (Q2), Q3 (the "box")
- Outliers (plotted individually as dots beyond the whiskers)

**Benefits of a Boxplot:**
- Easy way to see the distribution of data
- Reveals **skewness** of data
- Helps **identify outliers**
- Enables comparison of **2+ categories side by side** (side-by-side/grouped boxplots, e.g., comparing "Body Weight" across "Male" vs "Female")

---

## 4. Scatterplots

Used for visualizing the relationship between **two numerical variables** (Numerical–Numerical). Each point represents one observation, e.g., Ground Living Area (sq. ft.) vs Sale Price shows how one variable partially explains/predicts the other.

---

## 5. Covariance

**What problem does it solve?** It quantifies whether two variables move together, and in which direction.

**Definition:** Covariance measures the degree to which two variables are **linearly related** — whether one increases as the other increases (or decreases).

- **Positive covariance** → variables move in the **same** direction
- **Negative covariance** → variables move in **opposite** directions
- **Covariance ≈ 0** → variables are not linearly related

**Formulas:**
```
Population:  σxy = Σ[(X − μx)(Y − μy)] / N
Sample:      sxy = Σ[(X − x̄)(Y − ȳ)] / (n − 1)
```

**Worked Example** (Experience vs Salary):
| Exp (x) | Salary (y) |
|---|---|
| 2 | 1 |
| 5 | 2 |
| 8 | 5 |
| 12 | 12 |
| 13 | 10 |

x̄ = 8, ȳ = 6 → Σ(x−x̄)(y−ȳ) = 85 → Sample Covariance = 85/4 = **21.25** (positive → experience & salary move together)

**Worked Example** (Backlogs vs Package — negative relationship):
| Backlogs (x) | Package (y) |
|---|---|
| 2 | 10 |
| 5 | 12 |
| 8 | 5 |
| 12 | 2 |
| 13 | 1 |

x̄ = 8, ȳ = 6 → Σ(x−x̄)(y−ȳ) = −83 → Sample Covariance = −83/4 = **−21.25** (negative → as backlogs increase, package tends to decrease)

**Worked Example** (Covariance ≈ 0 — no linear relationship):
| Backlogs (x) | Package (y) |
|---|---|
| 2 | 10 |
| 5 | 10 |
| 8 | 10 |
| 12 | 10 |
| 13 | 10 |

Here `y` is constant regardless of `x`, so the covariance comes out to **0** — illustrating that a flat/constant variable has no linear relationship with anything.

**Disadvantage of Covariance:** It doesn't indicate the **strength** of a relationship because its magnitude depends on the scale/units of the variables involved — this is the exact problem **correlation** solves.

**Covariance of a variable with itself** = its own variance.

---

## 6. Correlation

**What problem does it solve?** Covariance's magnitude isn't standardized/interpretable across different units — correlation normalizes it into a fixed range.

**Definition:** Correlation measures the degree to which two variables are related, standardized to a range of **−1 to 1**.

```
Correlation (r) = Cov(x, y) / (σx × σy)
```

| Value | Meaning |
|---|---|
| +1 | Perfect positive correlation |
| 0 | No linear correlation |
| −1 | Perfect negative correlation |

**Types of relationships:** strong positive, weak positive, strong negative, weak negative, moderate negative, no correlation.

**How to use it — step by step:**
Using the Experience vs Salary data from the Covariance section: Cov(x,y) = 21.25

1. First, find the standard deviation of x (Experience): 2, 5, 8, 12, 13 → x̄ = 8
   - Deviations²: (2−8)²=36, (5−8)²=9, (8−8)²=0, (12−8)²=16, (13−8)²=25 → sum = 86
   - Sample variance = 86/4 = 21.5 → σx = √21.5 ≈ **4.64**
2. Next, find the standard deviation of y (Salary): 1, 2, 5, 12, 10 → ȳ = 6
   - Deviations²: (1−6)²=25, (2−6)²=16, (5−6)²=1, (12−6)²=36, (10−6)²=16 → sum = 94
   - Sample variance = 94/4 = 23.5 → σy = √23.5 ≈ **4.85**
3. Plug into the formula: r = Cov(x,y) / (σx × σy) = 21.25 / (4.64 × 4.85) = 21.25 / 22.5 ≈ **0.94**
4. Since 0.94 is very close to +1, this indicates a **strong positive correlation** between experience and salary.

### Correlation ≠ Causation
Correlation between two variables does **not** imply that one causes the other.

*Classic example:* Number of firefighters at a fire positively correlates with damage caused — but firefighters don't *cause* damage. A **confounding variable** (severity of the fire) drives both. Establishing true causality requires controlled experiments, randomized controlled trials, or carefully designed observational studies.

---

## 7. Visualizing Multiple Variables

| Technique | Use case |
|---|---|
| **3D Scatter Plot** | Visualize 3 numeric variables at once (e.g., sepal length, width, petal length) |
| **Hue Parameter** | Add a categorical dimension via color to a plot (e.g., bar plot split by "Program") |
| **Facet Grids** | Create a grid of plots split by one or more categorical variables (e.g., tip vs total_bill, faceted by lunch/dinner and colored by smoker) |
| **Jointplot** | Combines a scatter plot with marginal histograms for both variables |
| **Pairplot** | Grid of scatter plots (and histograms on the diagonal) for every pair of numeric variables in a dataset |
| **Bubble Plot** | Scatter plot where a third numeric variable is encoded via bubble/point **size** (and sometimes a 4th via color) |

---

## Additional Notes (Beyond the Session Content)

### Pearson vs Spearman Correlation
- **Pearson correlation** (the formula above) measures **linear** relationships and assumes roughly normal, continuous data.
- **Spearman correlation** measures **monotonic** relationships using ranked data — more robust to outliers and non-linear (but monotonic) trends.

### Other Outlier Detection Methods (complementary to IQR)
- **Z-score method** — flag points where `|z| = |(x − μ)/σ| > 3`
- **Modified Z-score** (uses median & MAD) — more robust for skewed data

### Correlation Matrix / Heatmap
In practice, correlation is computed pairwise across **all numeric columns** of a dataset and visualized as a heatmap — a key step in feature selection for ML (e.g., dropping one of two highly correlated features to reduce multicollinearity).

### Quick Python Reference
```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.DataFrame({'exp': [2,5,8,12,13], 'salary': [1,2,5,12,10]})

df.describe()                     # Five-number summary + mean/std
df['exp'].quantile(0.75)          # 75th percentile
np.percentile(df['exp'], 75)      # Alternative

df.cov()                          # Covariance matrix
df.corr()                         # Pearson correlation matrix
df.corr(method='spearman')        # Spearman correlation

sns.boxplot(data=df)              # Boxplot
sns.scatterplot(x='exp', y='salary', data=df)  # Scatterplot
sns.heatmap(df.corr(), annot=True)             # Correlation heatmap
sns.pairplot(df)                  # Pairplot
```

### Why This Matters for Data Science
- **Boxplots + IQR** → standard outlier-detection technique before model training
- **Covariance/Correlation** → core to **feature selection**, **PCA** (which literally decomposes the covariance matrix), and detecting **multicollinearity** in regression models
- **Pairplots/heatmaps** → almost always the first visual step in **EDA** on any new dataset
