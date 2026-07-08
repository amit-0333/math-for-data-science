# Session 4 — Normal Distribution

## 1. Recap — Using PDF in Data Science

Before diving into the Normal Distribution itself, this session recaps how a **PDF (Probability Density Function)** is used practically with real data.

**Example — Iris flower petal length, split by species:**
Imagine plotting the PDF of `petal_length` separately for 3 species: setosa, versicolor, virginica. Each species produces its own bell-shaped (or near bell-shaped) curve.

**How to read/use overlapping PDFs — step by step:**
1. Look at where each species' curve is concentrated on the x-axis.
2. *Setosa* is tightly packed around ~1.5 (petal_length) — a tall, narrow peak.
3. *Versicolor* and *Virginica* overlap more, centered further right (~4.5 to 5.5).
4. **To classify a new flower:** if its petal_length is, say, 2.3–5 → likely *versicolor* (since that's where its curve dominates). If petal_length > 5 → likely *virginica*.
5. This is literally how some simple classifiers work — comparing which class's density is **highest** at a given value of `x`.

**Extending to a second feature — petal_width:**
Using two thresholds:
- If petal_width is between 0.7 and 1.7 → **~95% likely** versicolor
- If petal_width > 1.7 → **~90% likely** virginica

This shows how **PDF-based reasoning** directly powers real classification decisions — you don't need a complex model to get a first estimate; the distribution's shape already tells you a lot.

---

## 2. 2D Probability Density Plots (Recap)

Progression of density plots by dimension:
```
1D (single variable) → PMF (discrete) / PDF (continuous)
2D (two variables together) → 2D density plot (contour/heatmap)
```

**How to read a 2D density plot — step by step:**
1. Axes represent two continuous variables (e.g., `sepal_length` on y-axis, `petal_length` on x-axis).
2. Darker/more intense shaded regions = combinations of both variables that occur **more frequently together**.
3. The color bar (e.g., 0.0146 to 0.2193) tells you the actual density value at each shaded region.
4. Marginal curves along the top and right edges show the **1D PDF** of each variable individually (as if you "squashed" the 2D plot down to one axis).
5. This lets you spot **clusters** — e.g., seeing two separate "blobs" in the 2D plot suggests the data naturally splits into two groups.

---

## 3. Normal Distribution

### What is the Normal Distribution?
Also called the **Gaussian Distribution**. It is a **continuous probability distribution** that is:
- **Symmetrical** around its mean
- **Bell-shaped**
- **Asymptotic** — the tails approach (but never touch) zero, stretching infinitely in both directions
- Has **most points concentrated near the mean**, with progressively fewer as you move away

### Parameters
Characterized by exactly **two parameters**:
- **μ (mu)** — the mean, representing the **center** of the distribution
- **σ (sigma)** — the standard deviation, representing the **spread**

**Notation:** `X ~ N(μ, σ)` — read as "X follows a Normal distribution with mean μ and standard deviation σ"

### Why is it Important?
**Commonality in Nature** — many real-world phenomena naturally follow a Normal distribution:
- Heights of people
- Weights of objects
- IQ scores of a population

This makes it one of the most useful distributions to assume/model data with.

### PDF Equation of the Normal Distribution
```
f(x) = (1 / (σ√(2π))) · e^(−½ · ((x−μ)/σ)²)
```

**Breaking the formula down — step by step (what each part does):**
1. `(x − μ) / σ` → measures **how many standard deviations away** x is from the mean (this is actually the Z-score, covered next!)
2. Squaring that and multiplying by `−½` → makes the curve peak at x=μ and fall off symmetrically as x moves away
3. `e^(...)` → the exponential function turns that into a smooth bell-curve shape
4. `1 / (σ√(2π))` → a constant that **normalizes** the curve so the total area underneath equals exactly 1

*(Reference tool: [Interactive Normal Distribution visualizer](https://samp-suman-normal-dist-visualize-app-lkntug.streamlit.app/))*

---

## 4. Standard Normal Variate (Z)

### What is it?
A **standardized form** of the Normal distribution with **mean = 0** and **standard deviation = 1**.
```
Z ~ N(0, 1)
```

### Why Standardize?
Standardizing lets us:
1. **Compare different distributions** with each other (even if their original scales/units are totally different)
2. **Calculate probabilities easily** using a pre-built **Z-table** instead of solving the integral by hand each time

### Z-score Formula
```
Z = (X − μ) / σ
```

### How to Transform Any Normal Distribution → Standard Normal Variate — step by step

**Worked Example:** Heights of adult males follow `X ~ N(68, 3)` (mean = 68 inches, SD = 3 inches). What's the probability a randomly selected male is **taller than 72 inches**?

1. **Convert 72 inches to a Z-score:**
   ```
   Z = (72 − 68) / 3 = 4/3 ≈ 1.33
   ```
2. **Look up Z = 1.33 in a Z-table** ([ztable.net](https://www.ztable.net/)) → this gives the area (probability) **to the left** of Z = 1.33 → approximately **0.9082** (i.e., 90.82%)
3. **We want the area to the RIGHT** (taller than 72"), so subtract from 1:
   ```
   P(X > 72) = 1 − 0.9082 = 0.0918 ≈ 9.18%
   ```
4. **Conclusion:** There's roughly a **9.18% chance** a randomly selected adult male is taller than 72 inches.

### What is a Z-table?
A **Z-table** tells you the area under the standard normal curve **to the left of a given Z-score**. It's a pre-computed lookup table so you don't need to solve the integral manually every time.

---

## 5. Properties of the Normal Distribution

### 5.1 Symmetricity
The distribution is **symmetric about its mean** — the probability of a value falling above the mean equals the probability of it falling below.
- Area to the left of the mean = 50%
- Area to the right of the mean = 50%

### 5.2 Measures of Central Tendency are Equal
For a perfectly Normal distribution:
```
Mean = Median = Mode
```

### 5.3 The Empirical Rule (68-95-99.7 Rule)
| Range | % of Data Contained |
|---|---|
| μ ± 1σ | ~68% (68.27%) |
| μ ± 2σ | ~95% (95.45%) |
| μ ± 3σ | ~99.7% (99.73%) |

**How to use it — step by step:**
*Example:* Test scores follow `X ~ N(70, 10)` (mean=70, SD=10)
1. 68% of students scored between 70−10 and 70+10 → **between 60 and 80**
2. 95% of students scored between 70−20 and 70+20 → **between 50 and 90**
3. 99.7% of students scored between 70−30 and 70+30 → **between 40 and 100**
4. So a score of 95 would be quite rare — it's more than 2 standard deviations above the mean!

### 5.4 Area Under the Curve
The **total area under the entire PDF curve = 1** (100% probability), and any sub-region's area gives the probability of falling in that range (same principle as a general PDF from Session 3).

---

## 6. Skewness

### What is Skewness?
A measure of the **asymmetry** of a distribution — how much it deviates from being perfectly symmetrical (Normal).

- In a **symmetrical** distribution → Mean = Median = Mode
- In a **skewed** distribution → Mean, Median, Mode are **not equal**, and one tail is longer than the other

### Types of Skew
| Skew Type | Tail Direction | Relationship |
|---|---|---|
| **Positive Skew (Right Skew)** | Longer tail on the **right** | Mode < Median < Mean |
| **Negative Skew (Left Skew)** | Longer tail on the **left** | Mean < Median < Mode |
| **Zero Skew** | Perfectly symmetric | Mean = Median = Mode |

*(Rule of thumb: the greater the skew, the greater the distance/gap between mode, median, and mean.)*

### Skewness Formula (Sample Skewness)
```
Skewness = [n / ((n−1)(n−2))] × Σ[((x − x̄)/s)³]
```
This is based on the **3rd moment** of the distribution (for reference: 2nd moment → variance, 3rd moment → skewness, 4th moment → kurtosis).

### Interpreting the Skewness Value — step by step
| Skewness value | Interpretation |
|---|---|
| 0 | Perfectly symmetric |
| ~0.5 | Moderately skewed |
| ~1 | Highly skewed |
| ~1.5 | Very highly skewed |

**Worked interpretation example:** If your computed skewness = **0.38**
1. Compare it to the general guide: values roughly between −0.5 and 0.5 are considered **"approximately/almost symmetric"**
2. 0.38 falls in that near-symmetric zone → conclude the data is **almost symmetric**, only mildly right-skewed.

### Python Example
```python
from scipy.stats import skew
import numpy as np

data = np.array([2, 3, 4, 4, 5, 6, 8, 20])
skew(data)   # returns the skewness value
```

---

## 7. CDF of the Normal Distribution

Same core idea as before (probability that X ≤ some value), but now expressed using the Normal PDF formula inside an integral:
```
F(x) = P(X ≤ x) = ∫₋∞ˣ f(t) dt = (1/(σ√(2π))) ∫₋∞ˣ e^(−(t−μ)²/2σ²) dt
```

**How to read the CDF graph — step by step:**
1. The CDF is an **S-shaped curve** (also called a "sigmoid" shape) that rises from 0 to 1.
2. Different μ and σ values shift/stretch this S-curve — e.g., a smaller σ makes the curve rise more steeply (data is tightly packed), while a larger σ makes it rise more gradually (data is spread out).
3. At `x = μ` (the mean), the CDF always equals exactly **0.5** — since half the data lies below the mean.
4. In practice, you rarely compute this integral by hand — you use a **Z-table** or software (`scipy.stats.norm.cdf`) instead.

---

## 8. Use of Normal Distribution in Data Science

1. **Outlier Detection** — values far in the tails (e.g., beyond 3 standard deviations) are flagged as potential outliers (the Z-score method from Session 2's "Additional Notes" directly uses this idea)
2. **Assumptions in ML Algorithms** — several algorithms assume normally distributed data/errors:
   - **Linear Regression** — assumes residuals (errors) are normally distributed
   - **Gaussian Mixture Models (GMM)** — literally models data as a mixture of several Normal distributions
3. **Hypothesis Testing** — many statistical tests (t-tests, z-tests) assume the underlying data (or the sampling distribution of the mean) is approximately Normal
4. **Central Limit Theorem (CLT)** — a cornerstone of statistics: no matter what distribution the original data follows, the distribution of **sample means** (for large enough sample sizes) approaches a Normal distribution. This is *why* the Normal distribution is so central to inferential statistics.

---

## Additional Notes (Beyond the Session Content)

### Kurtosis (the 4th Moment — a companion to Skewness)
While skewness measures asymmetry, **kurtosis** measures how heavy or light the **tails** of a distribution are compared to a Normal distribution:
- **Mesokurtic** — kurtosis ≈ Normal distribution (baseline)
- **Leptokurtic** — heavier tails, more extreme outliers than Normal
- **Platykurtic** — lighter tails, fewer extreme outliers than Normal

### Quick Python Reference
```python
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt

# Generate normal data and check its properties
data = np.random.normal(loc=68, scale=3, size=1000)   # mean=68, sd=3

# Z-score of a specific value
z = (72 - 68) / 3
print(z)   # 1.33

# Probability of X > 72 using the CDF directly (no need for a Z-table!)
prob_taller = 1 - stats.norm.cdf(72, loc=68, scale=3)
print(prob_taller)   # ≈ 0.0912

# Skewness and Kurtosis
print(stats.skew(data))
print(stats.kurtosis(data))

# Visualize
plt.hist(data, bins=30, density=True)
plt.show()
```

### Why This Matters for Data Science
- The Normal distribution and Z-scores are the backbone of **standardization** (feature scaling) used before training many ML models
- The **Empirical Rule** gives a fast, rule-of-thumb way to flag unusual/extreme data points without complex calculations
- The **Central Limit Theorem** is *the* reason why sample-based inference (confidence intervals, hypothesis tests, A/B testing) works even when we don't know the true population distribution
- **Skewness** checks are a standard EDA step — many models perform better after transforming (e.g., log-transform) heavily skewed features to make them closer to Normal
