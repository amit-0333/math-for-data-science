# Session 3 — Random Variables & Probability Distributions

## 1. Random Variables

### Algebraic Variable vs Random Variable
| Type | Definition | Example |
|---|---|---|
| **Algebraic Variable** | An unknown, fixed value (from Algebra) | `x` in `2x + 3 = 7` |
| **Random Variable** | A set of possible values from a **random experiment**, each with an associated probability | Outcome of a dice roll, height of a randomly selected person |

**How to think about it — step by step:**
1. Imagine rolling a single die. The outcome isn't fixed — it could be 1, 2, 3, 4, 5, or 6.
2. Each of these possible outcomes is a **value** the random variable `X` could take.
3. Each value also has a **probability** attached — here, each face has probability 1/6.
4. So a Random Variable = "the outcome" + "how likely each outcome is."

### Types of Random Variables
1. **Discrete Random Variable** — takes a **countable** number of distinct values (e.g., number of heads in 10 coin flips: 0, 1, 2, ... 10)
2. **Continuous Random Variable** — takes **any value within a range** (e.g., height, weight, time) — technically infinite possible values

---

## 2. Probability Distributions

### What is a Probability Distribution?
A list of **all possible outcomes** of a random variable, along with their **corresponding probabilities**.

### The Problem with Tables
For simple cases (like a die roll), a table works fine:
| Outcome | Probability |
|---|---|
| 1 | 1/6 |
| 2 | 1/6 |
| ... | ... |
| 6 | 1/6 |

But this breaks down when:
- The number of outcomes is very large (e.g., rolling 10 dice together — thousands of combinations)
- The number of outcomes is **infinite** (e.g., height of people — any decimal value is possible)

### The Solution — Use a Function
Instead of a table, we use a **mathematical function** `f(x)` that models the relationship between an outcome `x` and its probability. This function is called a **Probability Distribution Function**.

> **Note:** "Probability Distribution" and "Probability Distribution Function" are often used interchangeably in practice.

### Why are Probability Distributions Important?
1. They give us an idea of the **shape/spread** of the data.
2. If our data matches a **known/famous distribution**, we instantly know a lot about it (its mean, spread, common behaviors) — without having to analyze it from scratch.

### A Note on Parameters
**Parameters** are numerical values that determine the **shape, location, and scale** of a distribution. Different distributions have different parameters:

| Distribution | Parameters | What they control |
|---|---|---|
| Normal | μ (mean), σ (standard deviation) | Center and spread |
| Binomial | n (trials), p (probability of success) | Number of trials and success rate |
| Poisson | λ (lambda — average rate) | Average number of events in an interval |
| Exponential | λ (lambda — rate) | How quickly probability decays |
| Uniform | a, b (lower/upper bounds) | The range of possible values |

**How to use this — step by step example:**
Say you're told data follows a **Normal distribution with μ=50, σ=10**.
1. You immediately know the data is centered around 50 (the mean).
2. You know most values will fall within 10 units of 50 (one standard deviation) — roughly 68% of the data lies between 40 and 60.
3. You didn't need to look at a single raw data point to know this — just knowing "it's Normal with these parameters" tells you the whole shape.

### Types of Distributions (Discrete vs Continuous)
- **Discrete distributions** — plotted as separate dots/bars (e.g., Bernoulli, Binomial, Poisson, Geometric, Negative Binomial)
- **Continuous distributions** — plotted as a smooth curve (e.g., Normal, Exponential, Uniform, Beta, Gamma, Log-normal, Weibull, Cauchy)

**Famous Distributions (from the reference chart):**
| Discrete | Continuous |
|---|---|
| Bernoulli | Normal |
| Binomial | Uniform |
| Poisson | Exponential |
| Negative Binomial | Beta |
| Geometric | Gamma |
| Categorical | Log-normal, Weibull, Cauchy, Pareto |

---

## 3. Probability Mass Function (PMF)

**Definition:** A mathematical function describing the probability distribution of a **discrete** random variable. It assigns a probability to **each possible value**.

**Two conditions a valid PMF must satisfy:**
1. Every probability must be **non-negative** (≥ 0)
2. All probabilities together must **sum to 1**

**How to use it — step by step:**
*Example: A fair coin flipped once (X = 0 for Tails, X = 1 for Heads)*
1. List possible outcomes: X = 0, X = 1
2. Assign probabilities: P(X=0) = 0.5, P(X=1) = 0.5
3. Check condition 1: both are ≥ 0 ✅
4. Check condition 2: 0.5 + 0.5 = 1 ✅
5. This is a valid PMF — it's actually the **Bernoulli distribution** with p=0.5

*Example: Rolling a fair die (X = 1 to 6)*
1. P(X=k) = 1/6 for each k in {1,2,3,4,5,6}
2. Sum = 6 × (1/6) = 1 ✅ valid PMF

*(Further reading: [Bernoulli distribution](https://en.wikipedia.org/wiki/Bernoulli_distribution), [Binomial distribution](https://en.wikipedia.org/wiki/Binomial_distribution))*

---

## 4. Cumulative Distribution Function (CDF) — of a PMF

**Definition:** Describes the probability that a random variable `X` will be found at a value **less than or equal to** `x`.
```
F(x) = P(X ≤ x)
```

**How to use it — step by step:**
*Example: Fair die (X = 1 to 6), each with P(X=k) = 1/6*
1. F(1) = P(X≤1) = P(X=1) = 1/6 ≈ 0.167
2. F(2) = P(X≤2) = P(X=1) + P(X=2) = 2/6 ≈ 0.333
3. F(3) = P(X≤3) = 3/6 = 0.5
4. F(4) = 4/6 ≈ 0.667
5. F(5) = 5/6 ≈ 0.833
6. F(6) = 6/6 = 1.0

Notice the CDF always **increases** (or stays flat) as x increases, and eventually reaches 1 — this "staircase" shape is typical of a discrete CDF.

---

## 5. Probability Density Function (PDF)

**Definition:** A mathematical function describing the probability distribution of a **continuous** random variable.

### Why "Density" and not "Probability" directly?
For continuous variables, the probability of hitting **exactly one precise value** is technically **zero** (there are infinitely many possible decimal values). For example, `P(height = 165.00000... cm exactly) = 0`. Instead, the PDF gives a **density** — probability is only meaningful over a **range** (an interval), not a single point.

### What does the Area Under the Curve Represent?
The **area under the PDF curve between two points** gives the probability that the variable falls in that range.
```
P(a ≤ X ≤ b) = ∫ₐᵇ f(x) dx     (the integral/area from a to b)
```
And the **total area under the entire curve = 1** (100% probability across all possible values).

**How to use it — step by step (conceptual):**
*Example: Exam marks follow a PDF, and you want P(8 ≤ X ≤ 9) — the chance a mark falls between 8 and 9 (out of 10)*
1. You cannot ask "what's the probability of scoring exactly 8.00000...?" — that's 0 for a continuous variable.
2. Instead, shrink the question to a range: 8 to 9.
3. The PDF's **shaded area** between x=8 and x=9 on the graph *is* that probability.
4. If you wanted an even narrower range (8.0 to 8.1, or 8.00 to 8.01), the area shrinks accordingly — but a **range** is always needed to get a real probability number.

*(Further reading: [Normal distribution](https://en.wikipedia.org/wiki/Normal_distribution), [Log-normal distribution](https://en.wikipedia.org/wiki/Log-normal_distribution), [Poisson distribution](https://en.wikipedia.org/wiki/Poisson_distribution))*

---

## 6. Cumulative Distribution Function (CDF) — of a PDF

Same core idea as the discrete case, but now it's a **smooth curve** instead of a staircase, since the underlying variable is continuous.
```
F(x) = P(X ≤ x)
```

**How to read the paired PDF/CDF graphs:**
- The **PDF** (probability density curve) shows where the data is "bunched up" (peaks = more likely values).
- The **CDF** (cumulative curve) always **rises from 0 to 1**, and is essentially the **running total (integral)** of the PDF up to that point.
- Example: For heights centered around 165cm — the PDF peaks near 165, while the CDF crosses 0.5 (50%) right at 165, since half the population is below that height and half above.

**How to use it — step by step:**
*Example: Using the CDF to find P(X ≤ 165) for a height distribution*
1. Locate x = 165 on the CDF graph's x-axis
2. Read the corresponding y-value on the CDF curve → say it reads **0.5**
3. This means P(X ≤ 165) = **0.5**, i.e., there's a 50% chance a randomly selected person is 165cm or shorter.

**How to use PDF and CDF together in data analysis:**
- Use the **PDF** to understand the shape of your data (is it skewed? symmetric? multi-peaked?)
- Use the **CDF** to directly answer "what % of the data falls below/above a certain value?" — useful for percentiles, risk analysis, and setting thresholds

---

## 7. Density Estimation

**Definition:** A statistical technique to **estimate the PDF** of a random variable based on observed data — i.e., figuring out the underlying distribution shape when we only have raw data points, not the formula.

**Used for:** hypothesis testing, data analysis, data visualization, and (in ML) estimating the probability distribution of input data or modeling the likelihood of outcomes.

### 7.1 Parametric Density Estimation
**Assumes** the data follows a **specific known distribution family** (e.g., Normal, Exponential, Poisson) and then estimates that distribution's parameters (like μ and σ) from the data.

**How to use it — step by step:**
1. Look at your data's histogram — does it look bell-shaped?
2. If yes, assume it's Normally distributed.
3. Estimate the parameters directly from the data: μ ≈ sample mean (x̄), σ ≈ sample standard deviation (s)
4. Now you have a complete mathematical model (a specific Normal curve) describing your data.

### 7.2 Non-Parametric Density Estimation
Used when the data **doesn't clearly match** any famous distribution. It makes **no assumption** about the underlying shape and instead builds an estimate directly from the data itself.

| | Parametric | Non-Parametric |
|---|---|---|
| Assumption | Assumes a known distribution family | No assumption about shape |
| Flexibility | Less flexible, but simpler & needs less data | More flexible, handles complex/unknown shapes |
| Cost | Computationally cheap | Computationally intensive, needs more data |

### Kernel Density Estimation (KDE) — a Non-Parametric Method
**How it works:** Places a small "kernel" (typically a mini bell-curve) over **each data point**, then sums/smooths them all together to create one continuous estimated density curve.

**How to use it — step by step (conceptual):**
1. Say you have 6 data points scattered on a number line.
2. Place a small bell-shaped bump (kernel) centered on each of the 6 points.
3. Add up all 6 bumps together, point by point along the x-axis.
4. The result is one smooth curve — this is your **KDE estimate** of the underlying density.
5. **Bandwidth** (the width of each little bump) controls smoothness:
   - Too small → the curve looks spiky/jagged (overfits to individual points)
   - Too large → the curve becomes too flat/smooth (loses real detail/structure)

---

## 8. 2D Probability Density Plots

Extending the idea of a 1D PDF (single variable) to **two variables at once** — visualizing how the probability density is distributed across a 2D plane (e.g., a contour plot or heatmap showing where two variables are jointly most likely to occur together).

---

## Additional Notes (Beyond the Session Content)

### Expected Value & Variance of a Random Variable
- **Expected Value (Mean of a Random Variable):** `E(X) = Σ x · P(X=x)` (discrete) — the long-run average outcome if the experiment were repeated infinitely
- **Variance of a Random Variable:** `Var(X) = E[(X − E(X))²]` — measures the spread of the random variable's outcomes

**Step-by-step example:** Fair die (X = 1 to 6, each P = 1/6)
```
E(X) = (1+2+3+4+5+6) × (1/6) = 21/6 = 3.5
```

### Common Distributions & Where They Show Up in Data Science / ML
| Distribution | Real-world use |
|---|---|
| **Bernoulli** | Single yes/no event (e.g., one coin flip, one click/no-click) |
| **Binomial** | Number of successes in n repeated trials (e.g., 10 coin flips) |
| **Poisson** | Number of events in a fixed time/space (e.g., customer arrivals per hour) |
| **Normal (Gaussian)** | Heights, test scores, measurement errors — the most common distribution, central to the Central Limit Theorem |
| **Exponential** | Time between events (e.g., time until next customer arrives) |
| **Uniform** | Every outcome equally likely (e.g., random number generators) |

### Quick Python Reference
```python
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt
import seaborn as sns

# Discrete: Binomial PMF & CDF
n, p = 10, 0.5
x = np.arange(0, n+1)
pmf = stats.binom.pmf(x, n, p)
cdf = stats.binom.cdf(x, n, p)

# Continuous: Normal PDF & CDF
mu, sigma = 165, 10
x = np.linspace(130, 200, 200)
pdf = stats.norm.pdf(x, mu, sigma)
cdf = stats.norm.cdf(x, mu, sigma)

# P(a <= X <= b) for a continuous Normal variable
prob = stats.norm.cdf(170, mu, sigma) - stats.norm.cdf(160, mu, sigma)

# Non-parametric density estimation (KDE)
data = np.random.normal(50, 5, 200)
sns.kdeplot(data)   # plots a smooth estimated density curve

# 2D density plot
x = np.random.normal(0, 1, 500)
y = np.random.normal(0, 1, 500)
sns.kdeplot(x=x, y=y, fill=True)   # 2D density/contour plot
```

### Why This Matters for Data Science
- Recognizing which distribution your data follows lets you **choose the right statistical tests** and **model assumptions** (e.g., linear regression assumes normally distributed residuals)
- **PMF/PDF/CDF** underpin core ML concepts: loss functions (e.g., cross-entropy uses probability), Naive Bayes classifiers, and probabilistic models
- **KDE** is widely used in EDA to visualize the shape of a feature's distribution without assuming it fits a known formula
- Understanding **parameters of distributions** is essential for simulating data, generative models, and Bayesian statistics
