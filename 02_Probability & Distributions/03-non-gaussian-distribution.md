# Session — Kurtosis, QQ Plots & Non-Gaussian Distributions

## 1. Kurtosis

### What is Kurtosis?
Kurtosis is the **4th statistical moment** — it measures the **"tailedness"** of a probability distribution (how heavy or light the tails are compared to a Normal distribution).

**The 4 Statistical Moments (for reference):**
| Moment | Measures |
|---|---|
| 1st | Mean |
| 2nd | Variance (Standard Deviation) |
| 3rd | Skewness |
| 4th | **Kurtosis** |

### Formula (Sample Kurtosis)
```
Sample Kurtosis = { [n(n+1)] / [(n−1)(n−2)(n−3)] } × Σ[((xᵢ−x̄)/s)⁴]  −  [3(n−1)²] / [(n−2)(n−3)]
```

### Excess Kurtosis
**Excess Kurtosis** = Sample Kurtosis − 3. This re-centers the scale so that a **Normal distribution has Excess Kurtosis = 0** (making it easy to compare any distribution against the Normal baseline).

### Types of Kurtosis — Visualized

```
  Leptokurtic (Excess Kurtosis > 0)  —  narrow, tall peak + FAT tails
  ─────────────────────────────────────────────────────────────────
                        ▄██▄
                       █████
                      ███████
                     █████████
              ·  ·  ███████████  ·  ·        ← tails stay "thick"
        ·  ·  ·  · █████████████ ·  ·  ·  ·     far from center
  ·  ·  ·  ·  ·  · ███████████████ ·  ·  ·  ·  ·  ·
  ─────────────────────────────────────────────────
        (sharper peak than Normal, more extreme outliers)


  Mesokurtic (Excess Kurtosis = 0)  —  the Normal distribution baseline
  ─────────────────────────────────────────────────────────────────
                      ▄█████▄
                    ███████████
                  ███████████████
              ·  █████████████████  ·        ← tails taper off
        ·  ·  · ███████████████████ ·  ·  ·     at a "normal" rate
  ─────────────────────────────────────────────────
        (this shape is the reference/baseline — kurtosis = 0)


  Platykurtic (Excess Kurtosis < 0)  —  flat, wide top + THIN tails
  ─────────────────────────────────────────────────────────────────
                ████████████████████
              ████████████████████████
            ████████████████████████████
          ████████████████████████████████
  ─────────────────────────────────────────────────
        (flatter/wider peak, tails drop off quickly — few outliers)
```

| Type | Excess Kurtosis | Tail Weight | Meaning |
|---|---|---|---|
| **Leptokurtic** ("slender") | > 0 | Fatter tails | More extreme values/outliers than Normal |
| **Mesokurtic** | = 0 | Same as Normal | The Normal distribution family itself |
| **Platykurtic** ("broad") | < 0 | Thinner tails | Fewer extreme values/outliers than Normal |

### Practical Use-Case — Finance
**Kurtosis risk** refers to the risk of extreme outcomes ("fat tails") in asset/portfolio returns.
- **High kurtosis (Leptokurtic)** → higher chance of extreme gains or losses → riskier, more volatile asset
- **Low kurtosis (Platykurtic)** → more gradual price movements → less risky
- **Mesokurtic** is often considered the "ideal" balance between risk and return

### Python Example
```python
from scipy.stats import kurtosis
import numpy as np

data = np.random.normal(0, 1, 1000)
print(kurtosis(data))   # Fisher's definition -> returns EXCESS kurtosis (Normal = 0)
```

---

## 2. QQ Plot (Quantile-Quantile Plot)

### How to Check if Data is Normal — 3 Methods
1. **Visual inspection** — plot a histogram/density plot; check if it looks bell-shaped and symmetric
2. **QQ Plot** — plot your data's quantiles against theoretical Normal quantiles; if points fall on a straight line, data is likely Normal
3. **Statistical tests** — Shapiro-Wilk, Anderson-Darling, Kolmogorov-Smirnov tests give a p-value; p < 0.05 usually suggests **not Normal**

### What is a QQ Plot?
A graphical tool comparing the **quantiles of your data** against the **quantiles of a theoretical distribution** (usually Normal).

**How it's built — step by step:**
1. Sort your actual data from smallest to largest
2. Compute its quantiles (e.g., split into 100 equal parts → 100 sample quantiles)
3. Compute the corresponding theoretical quantiles from a **perfect Normal distribution**
4. Plot: X-axis = theoretical quantiles, Y-axis = your data's quantiles
5. **If your data IS Normal** → points fall almost exactly on a straight diagonal line
6. **If your data is NOT Normal** → points curve away from the line

### Visualizing QQ Plot Interpretations

```
Normally Distributed Data                    Skewed Data
                                    
Data                                Data
Quantiles      ⋰                   Quantiles           ⋰⋰
   |         ⋰                        |              ⋰⋰
   |       ⋰                          |          ⋰⋰⋰
   |     ⋰            <- straight     |      ⋰⋰⋰       <- curves away
   |   ⋰                line             |  ⋰⋰                from line
   | ⋰                                   |⋰
   +------------------                   +------------------
     Theoretical Quantiles                 Theoretical Quantiles
```

```
Fat Tails (Leptokurtic)                     Thin Tails (Platykurtic)

Data                                Data
Quantiles       ⋰⋰↗ (points curve    Quantiles          ⋰
   |          ⋰⋰   UP sharply at        |            ⋰
   |        ⋰⋰     the ends -           |          ⋰       <- points curve
   |      ⋰⋰       "fatter tails")      |        ⋰            INWARD at ends
   |   ↙⋰⋰                              |      ⋰               ("thinner tails")
   |⋰⋰                                  |    ⋰
   +------------------                  +------------------
```

### Does a QQ Plot Only Detect Normality?
**No** — a QQ plot can compare your data against **any** theoretical distribution (Normal, Uniform, Pareto, etc.), not just Normal. You simply change which theoretical quantiles you're comparing against.

---

## 3. Uniform Distribution

### What is it?
A distribution where **all outcomes are equally likely** within a given range — no value is more probable than another.

**Types:** Discrete (e.g., a die roll) and Continuous (e.g., a randomly measured height within a range)

**Notation:** `X ~ U(a, b)` where `a` = lower bound, `b` = upper bound

### PDF & CDF

```
PDF (flat rectangle):                    CDF (straight ramp):

f(x)                                     F(x)
 │                                        │                    ________
 │  ┌──────────────┐                      │                 ⋰
 │  │ 1/(b−a)       │                     │              ⋰
 │  │               │                     │           ⋰
 │__│_______________│___                  │________⋰____________
    a               b   x                 0        a        b   x
```

**PDF Formula:**
```
f(x) = 1/(b−a)   for a ≤ x ≤ b
f(x) = 0         otherwise
```

**How to use it — step by step:**
*Example: A machine takes between 5 and 10 minutes (uniformly) to produce a product. What's the probability density at any point in this range?*
1. a = 5, b = 10
2. f(x) = 1/(10−5) = 1/5 = **0.2** for any x between 5 and 10
3. This means every minute value in [5,10] is **equally likely** — the density is flat.

### Real-World Examples
- Height of a randomly selected person from a group ranging 5'6"–6'0"
- Time to produce a product (5–10 minutes)
- Distance a car travels on a full tank (300–400 miles)

### Skewness
Uniform distribution has **Skewness = 0** → perfectly symmetric (though it does NOT look bell-shaped like a Normal distribution — symmetry ≠ Normality!)

### Applications in ML/Data Science
1. **Random initialization** — neural network weights, k-means cluster centers are often initialized using a Uniform distribution
2. **Sampling** — selecting a representative random subset of data
3. **Data augmentation** — generating new synthetic data points within a range
4. **Hyperparameter tuning** — defining a uniform search range/prior for hyperparameters

---

## 4. Log-Normal Distribution

### What is it?
A **heavy-tailed, right-skewed** continuous distribution where the **logarithm** of the variable is Normally distributed.
```
If X ~ LogNormal(μ, σ)  then  ln(X) ~ N(μ, σ)
```

### Shape — Visualized
```
Log-Normal PDF (right-skewed):

 │      ▄█▄
 │    ▄█████▄
 │  ▄████████▄▄
 │▄███████████▄▄▄▄▄▄▄____
 └──────────────────────────  x
   (sharp rise, long tail to the right)
```

### Real-World Examples
- Length of comments/posts in online forums
- Users' dwell time on articles
- Length of chess games
- Income distribution of the **top 97–99%** of a population (economics)

### How to Check if Data is Log-Normal
Take the **log of your data**, then check if THAT transformed data looks Normal (via histogram, QQ plot, or statistical test). If `log(X)` looks Normal, then `X` is Log-Normal.

---

## 5. Pareto Distribution

### What is it?
Models quantities that follow a **power-law** relationship — commonly used for wealth, income, and similar highly unequal distributions.

### What is a Power Law?
A relationship where one variable is proportional to a power of another:
```
y = k · xᵃ
```

### The Pareto Principle ("80-20 Rule")
Vilfredo Pareto observed that **20% of the population controls 80% of the wealth** in a society — this pattern is now called the Pareto Principle or the 80-20 rule.

### Shape — Visualized
```
Pareto PDF (steep drop-off, long thin tail):

 │█
 │█▄
 │██▄▄
 │████▄▄▄▄___
 └──────────────────  x
  xₘ
  (most of the "mass"/probability concentrated
   near the minimum value xₘ, then a long thin tail)
```

**PDF Formula:**
```
f(x) = (α · xₘᵅ) / x^(α+1)      for x ≥ xₘ
```
where `xₘ` = minimum possible value, `α` = shape parameter (controls how fast the tail decays)

### Real-World Examples
- Sizes of human settlements (few large cities, many small villages)
- File size distribution of internet traffic (many small files, few large ones)

### How to Detect a Pareto Distribution
1. **QQ plot** against theoretical Pareto quantiles
2. **Log-log plot** — plot `log(x)` vs `log(y)`; a Pareto distribution shows up as roughly a **straight line** on a log-log scale (this is the classic signature of any power-law distribution)

```
Log-Log Plot of a Pareto Distribution:

log(y)
  │ ⋱
  │   ⋱⋱
  │      ⋱⋱⋱          <- roughly straight line = power-law behavior
  │          ⋱⋱⋱⋱
  └──────────────────  log(x)
```

---

## Additional Notes (Beyond the Session Content)

### Quick Comparison of Non-Gaussian Distributions
| Distribution | Shape | Common Use Case |
|---|---|---|
| **Uniform** | Flat rectangle | Random initialization, unbiased sampling |
| **Log-Normal** | Right-skewed, heavy right tail | Income, dwell time, comment length |
| **Pareto** | Extremely front-loaded, long thin tail | Wealth distribution, file sizes, city populations |

### Transformations — Handling Non-Normal Data
When your data isn't Normal but your model/test needs it to be, common **transformations** include:
- **Log transform** — `log(x)` — good for right-skewed data (e.g., turning Log-Normal data into Normal data)
- **Square root transform** — `√x` — milder than log, useful for count data
- **Box-Cox transform** — a flexible family of power transformations that automatically finds the best exponent to make data as Normal as possible

### Quick Python Reference
```python
import numpy as np
from scipy import stats
import statsmodels.api as sm
import matplotlib.pyplot as plt

# Generate a right-skewed (log-normal) dataset
data = np.random.lognormal(mean=0, sigma=0.5, size=1000)

# QQ plot against Normal distribution
sm.qqplot(data, line='45')
plt.show()

# Check skewness and kurtosis
print("Skewness:", stats.skew(data))
print("Excess Kurtosis:", stats.kurtosis(data))

# Log-transform to make it more Normal
log_data = np.log(data)
print("Skewness after log transform:", stats.skew(log_data))

# Box-Cox transform (data must be strictly positive)
transformed, best_lambda = stats.boxcox(data)
print("Best Box-Cox lambda:", best_lambda)
```

### Why This Matters for Data Science
- Many real-world datasets (income, city sizes, word frequencies, file sizes) are **not Normal** — they follow Log-Normal or Pareto-like patterns instead
- **Kurtosis** matters heavily in finance/risk modeling — ignoring fat tails (Leptokurtic behavior) underestimates the chance of extreme market events
- **QQ plots** are a standard EDA step to decide whether to apply a transformation before using models that assume Normality (linear regression, t-tests, etc.)
- Recognizing power-law (Pareto) behavior is key in network science, recommendation systems, and understanding "long-tail" phenomena in user behavior data
