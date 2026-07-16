# Session 1 — Linear Algebra: Vectors

> **Category:** Linear Algebra (place this in a `Linear-Algebra/` folder, not under Descriptive Statistics or Probability & Distributions)

## Introduction

Linear algebra is a branch of mathematics that deals with the study of linear systems — sets of equations involving linear functions of variables. It is foundational to computer science, engineering, physics, economics, and especially machine learning.

---

## What are Vectors

A **vector** is an ordered collection of numbers that represents both a **magnitude** and a **direction**. Geometrically, a vector can be drawn as an arrow from the origin to a point in space.

```
        y
        |
        |      • (3,4)
        |     /
        |    /
        |   /   <- vector (3,4)
        |  /
        | /
        |/________________ x
       (0,0)
```

A vector in n-dimensional space is written as:

```
v = (v1, v2, ..., vn)
```

### How to use it — step by step
1. Identify the components of the vector (its coordinates along each axis).
2. Write it as an ordered tuple, e.g. `v = (3, 4)` in 2D.
3. To draw it, start at the origin `(0,0)` and draw an arrow to the point `(3,4)`.

**Worked example:** A vector `v = (3, 4)` starts at the origin and points to `(3,4)` — this represents a displacement of 3 units in x and 4 units in y.

---

## Vector Example in Machine Learning

In machine learning, a **data point/sample** is commonly represented as a vector, where each component is a **feature**.

### How to use it — step by step
1. List the features you are measuring for one data sample (e.g. height, weight, age).
2. Arrange them in a fixed order as a vector.
3. Each sample in your dataset becomes one vector; the whole dataset becomes a matrix (rows = samples, columns = features).

**Worked example:** A patient record with height = 170 cm, weight = 65 kg, age = 30 years becomes the feature vector:
```
patient = (170, 65, 30)
```

**From the notes — Iris dataset example:** A flower sample is represented as a feature vector of its measurements (sepal length, sepal width, petal length, petal width):
```
feature_vector = [5.2, 2.1, 7.2, 9.1]   # (SL, SW, PL, W)
```
This is a **5-dimensional feature vector** in the notes' example (`[3.1, 4.2, 7, 6.5]`), and the corresponding **target** is the flower species (setosa / versicolor / virginica) — a classic input-features-to-target setup.

**From the notes — Titanic dataset example (categorical encoding):** Non-numeric columns must be encoded as numbers before they can become part of a feature vector:
```
columns:  age | fare | sex | class | embarked
values:    17  |  52  |  M  |   1   |    S
```
Encoding rule used: `M → 0`, `F → 1` (sex), giving the final numeric feature vector:
```
[17, 52, 0, 1, 2]
```
This illustrates why **categorical encoding** is a required preprocessing step before vectors can be used in most ML models.

---

## Row and Column Vectors

- **Row vector**: elements arranged horizontally, shape `1 × n`.
- **Column vector**: elements arranged vertically, shape `n × 1`.

```
Row vector:            Column vector:
[ 1  2  3 ]             [ 1 ]
                        [ 2 ]
                        [ 3 ]
```

### How to use it — step by step
1. Decide whether your convention needs elements listed horizontally (row) or vertically (column).
2. In most ML libraries (numpy), a 1-D array can be reshaped into either form using `.reshape(1, -1)` for row or `.reshape(-1, 1)` for column.

**Worked example:** The vector `(1, 2, 3)` as a row vector is `[1 2 3]`; as a column vector it is a 3×1 array stacked vertically.

---

## Distance From Origin — Vector Norm ‖A‖

The distance of a vector from the origin (its **magnitude** or **L2 norm**) is:

```
‖A‖ = √(a1² + a2² + ... + an²)
```

### How to use it — step by step
1. Square each component of the vector.
2. Sum the squares.
3. Take the square root of the sum.

**Worked example:** For `A = (3, 4)`:
```
‖A‖ = √(3² + 4²) = √(9 + 16) = √25 = 5
```

---

## Euclidean Distance

The **Euclidean distance** between two points (or vectors) `P = (p1, p2, ..., pn)` and `Q = (q1, q2, ..., qn)` is:

```
d(P, Q) = √( (q1-p1)² + (q2-p2)² + ... + (qn-pn)² )
```

### How to use it — step by step
1. Subtract corresponding coordinates of the two points.
2. Square each difference.
3. Sum the squared differences.
4. Take the square root.

**Worked example:** For `P = (1, 2)` and `Q = (4, 6)`:
```
d = √( (4-1)² + (6-2)² ) = √(9 + 16) = √25 = 5
```

---

## Scalar Addition/Subtraction (Shifting) — Mean Centering

Adding or subtracting a constant to every component of a vector **shifts** it. A common use is **mean centering**: subtracting the mean of a dataset from every value so the new dataset has mean 0.

```
x' = x - mean(x)
```

### How to use it — step by step
1. Compute the mean of your data vector.
2. Subtract the mean from every element.
3. The resulting vector is "centered" around zero.

**Worked example:** Data `x = (2, 4, 6)`, mean = `(2+4+6)/3 = 4`.
```
x' = (2-4, 4-4, 6-4) = (-2, 0, 2)
```

Mean centering is used in **PCA** (so the first principal component reflects true variance direction, not offset), **linear regression** (interpretable intercepts), **gradient descent** (better-conditioned optimization), **k-means clustering** (unbiased initial centroids), and **regularization** (consistent penalty across features).

---

## Scalar Multiplication/Division (Scaling)

Multiplying (or dividing) every component of a vector by a scalar `k` stretches or shrinks it.

```
k·v = (k·v1, k·v2, ..., k·vn)
```

### How to use it — step by step
1. Choose the scalar `k`.
2. Multiply every component of the vector by `k`.
3. If `k > 1`, the vector grows; if `0 < k < 1`, it shrinks; if `k < 0`, it also reverses direction.

**Worked example:** `v = (2, 3)`, `k = 3`:
```
3·v = (3·2, 3·3) = (6, 9)
```

---

## Vector Addition/Subtraction

Vectors are added or subtracted **component-wise**.

```
A + B = (a1+b1, a2+b2, ..., an+bn)
A - B = (a1-b1, a2-b2, ..., an-bn)
```

### How to use it — step by step
1. Make sure both vectors have the same number of dimensions.
2. Add (or subtract) corresponding components.

**Worked example:** `A = (1, 2)`, `B = (3, 4)`:
```
A + B = (1+3, 2+4) = (4, 6)
A - B = (1-3, 2-4) = (-2, -2)
```

**From the notes — triangle law of vector addition:** if you place `v2` starting at the tip of `v1`, the vector from the start of `v1` to the tip of `v2` is the **resultant** `v3 = v1 + v2`.

```
        v3 = v2 + v1
       ^
      /
     /  ^ v2
    /  /
   / /
  //________> v1
```

**From the notes — centroid of several vectors:**
```
centroid = (v1 + v2 + v3 + ... + vn) / n
```
This is simply the mean position of a set of points/vectors — the same averaging idea used to find the "center" of a cluster in k-means clustering.

**From the notes — connection to gradient descent:** in ML, the model's parameters are stored as a **weight vector**, and vector addition/subtraction is exactly how weights get updated during training:
```
weight = [w1, w2, w3, ..., wn]
derivative = [∂L/∂w1, ∂L/∂w2, ∂L/∂w3, ..., ∂L/∂wn]
wₙ(new) = wₙ(old) − η · derivative
```
where `η` (eta) is the learning rate and `∂L/∂wᵢ` is the partial derivative of the loss `L` with respect to weight `wᵢ`. This is literally a **vector subtraction**: the new weight vector equals the old weight vector minus a scaled version of the gradient vector.

### How to use it — step by step (gradient descent weight update)
1. Compute the loss `L` for your current weights.
2. Compute the gradient vector (partial derivatives of `L` with respect to each weight).
3. Scale the gradient vector by the learning rate `η`.
4. Subtract this scaled gradient from the current weight vector to get the updated weights.

**Worked example:** `weight = [0.5, 0.2]`, `gradient = [0.4, -0.1]`, `η = 0.1`:
```
new_weight = [0.5, 0.2] - 0.1×[0.4, -0.1]
           = [0.5, 0.2] - [0.04, -0.01]
           = [0.46, 0.21]
```

---

## Dot Product

The **dot product** of two vectors is a scalar defined as:

```
A · B = a1·b1 + a2·b2 + ... + an·bn
      = ‖A‖ ‖B‖ cos(θ)
```

### How to use it — step by step
1. Multiply corresponding components of the two vectors.
2. Sum all the products.

**Worked example:** `A = (1, 2)`, `B = (3, 4)`:
```
A · B = (1×3) + (2×4) = 3 + 8 = 11
```

**Orthogonality check:** two non-zero vectors are **perpendicular (orthogonal)** exactly when their dot product is zero.
```
A · B = 0  ⟺  A ⊥ B
```
**Worked example:** `A = (2, 0)`, `B = (0, 5)`: `A·B = 2×0 + 0×5 = 0` → `A` and `B` are orthogonal (they lie on the x-axis and y-axis respectively).

---

## Angle Between 2 Vectors

Rearranging the dot product formula gives the angle between two vectors:

```
θ = arccos( (A · B) / (‖A‖ ‖B‖) )
```

### How to use it — step by step
1. Compute the dot product `A · B`.
2. Compute the norms `‖A‖` and `‖B‖`.
3. Divide the dot product by the product of the norms.
4. Take the inverse cosine (arccos) of the result.

**Worked example:** `A = (1, 2)`, `B = (3, 4)`, `A·B = 11`, `‖A‖ = √5 ≈ 2.236`, `‖B‖ = 5`:
```
θ = arccos(11 / (2.236 × 5)) = arccos(11/11.18) = arccos(0.984) ≈ 10.3°
```

**Interpreting the angle — cosine similarity:** the value `cos(θ)` itself (before taking arccos) is called **cosine similarity** and always lies between `-1` and `1`. It is one of the most common similarity measures in ML (recommender systems, NLP embeddings):

| cos(θ) | θ | Meaning |
|---|---|---|
| 1 | 0° | Vectors point in exactly the same direction (maximally similar) |
| 0 | 90° | Vectors are orthogonal (unrelated / dissimilar) |
| -1 | 180° | Vectors point in exactly opposite directions |

**Worked example:** two movies represented as rating-pattern vectors `A = (5, 1)` and `B = (4, 1)` (both rated highly by action-fans, low by romance-fans):
```
cos(θ) = (5×4 + 1×1) / (√26 × √17) = 21 / 21.02 ≈ 0.999
```
`θ ≈ 2.5°` — extremely similar, so a recommender system would suggest movie B to fans of movie A.

---

## Unit Vector

A **unit vector** has magnitude 1 and points in the same direction as the original vector.

```
û = v / ‖v‖
```

### How to use it — step by step
1. Compute the norm `‖v‖` of the vector.
2. Divide every component of `v` by `‖v‖`.

**Worked example:** `v = (3, 4)`, `‖v‖ = 5`:
```
û = (3/5, 4/5) = (0.6, 0.8)
```
Check: `‖û‖ = √(0.6² + 0.8²) = √(0.36+0.64) = √1 = 1` ✓

---

## Projection of a Vector

The **projection of vector A onto vector B** gives the component of `A` that lies along the direction of `B`.

```
proj_B(A) = ( (A · B) / ‖B‖² ) · B
```

### How to use it — step by step
1. Compute the dot product `A · B`.
2. Compute `‖B‖²` (the squared norm of `B`).
3. Divide the dot product by `‖B‖²` to get a scalar.
4. Multiply that scalar by vector `B`.

**Worked example:** `A = (2, 3)`, `B = (1, 0)`:
```
A · B = 2×1 + 3×0 = 2
‖B‖² = 1² + 0² = 1
proj_B(A) = (2/1) · (1, 0) = (2, 0)
```
This makes sense: the projection of `A` onto the x-axis just keeps the x-component.

```
      y
      |
      |   A(2,3)
      | .*
      |/  \
      +----*------ x (B direction)
     (0,0) proj=(2,0)
```

---

## Equation of a Line in n-Dimensions

A line through point `P0` in the direction of vector `d` is written parametrically as:

```
P(t) = P0 + t·d,   t ∈ ℝ
```

### How to use it — step by step
1. Pick a known point on the line, `P0`.
2. Pick a direction vector `d` (e.g. from two known points on the line, `d = P1 - P0`).
3. Substitute different values of `t` to generate all points on the line.

**Worked example:** `P0 = (1, 1)`, `d = (2, 3)`:
```
P(t) = (1 + 2t, 1 + 3t)
```
At `t=0`: `(1,1)`. At `t=1`: `(3,4)`. At `t=2`: `(5,7)` — all points on the same line.

---

## Vector Norms

A **norm** is a general way to measure the "length" of a vector. Common norms:

| Norm | Formula | Name |
|---|---|---|
| L1 | `‖v‖₁ = |v1| + |v2| + ... + |vn|` | Manhattan norm |
| L2 | `‖v‖₂ = √(v1² + v2² + ... + vn²)` | Euclidean norm |
| L∞ | `‖v‖∞ = max(|v1|, |v2|, ..., |vn|)` | Max norm |
| Lp | `‖v‖ₚ = (Σ|vi|^p)^(1/p)` | General p-norm |

### How to use it — step by step
1. Choose which norm you need (L1 for sparsity-related tasks, L2 for standard distance, L∞ for worst-case bound).
2. Apply the corresponding formula to the vector's components.

**Worked example:** `v = (3, -4)`:
```
L1 norm  = |3| + |-4| = 3 + 4 = 7
L2 norm  = √(3² + (-4)²) = √25 = 5
L∞ norm  = max(|3|, |-4|) = 4
```

```
Comparing norms of v = (3, -4):

L1  ███████            (7)
L2  █████              (5)
L∞  ████               (4)
```

---

## Additional Notes (Beyond the Session Content)

- **Why vectors matter in ML:** Every feature representation — pixel intensities of an image, word embeddings, sensor readings — is a vector. Almost all ML math (distances, similarities, gradients) reduces to vector operations.
- **Cosine similarity** (related to angle between vectors) is widely used in NLP/recommendation systems to measure how similar two vectors are, regardless of magnitude:
  ```
  cosine_similarity(A, B) = (A · B) / (‖A‖ ‖B‖)
  ```
- **L1 vs L2 regularization:** L1 norm encourages sparsity (many zero coefficients — used in Lasso regression); L2 norm encourages small, spread-out coefficients (used in Ridge regression).
- **Broadcasting:** In numpy, scalar operations and vector operations broadcast automatically over arrays, which is why these formulas translate directly into one-line code.
- **Standardization vs mean centering:** Mean centering only shifts data to zero mean; standardization also divides by the standard deviation, giving unit variance — an extension frequently used together with mean centering in preprocessing pipelines.

### Quick Python Reference

```python
import numpy as np

# Define vectors
A = np.array([1, 2])
B = np.array([3, 4])

# Norm (magnitude / distance from origin)
norm_A = np.linalg.norm(A)                     # 2.236...

# Euclidean distance between two points
euclidean_dist = np.linalg.norm(B - A)         # 2.828...

# Mean centering
data = np.array([2, 4, 6])
centered = data - data.mean()                  # [-2, 0, 2]

# Scalar multiplication
scaled = 3 * A                                 # [3, 6]

# Vector addition/subtraction
add_vec = A + B                                # [4, 6]
sub_vec = A - B                                # [-2, -2]

# Dot product
dot = np.dot(A, B)                             # 11

# Angle between vectors (in degrees)
cos_theta = dot / (np.linalg.norm(A) * np.linalg.norm(B))
theta_deg = np.degrees(np.arccos(cos_theta))

# Unit vector
unit_A = A / np.linalg.norm(A)

# Projection of A onto B
proj_A_on_B = (np.dot(A, B) / np.dot(B, B)) * B

# Different norms
l1_norm = np.linalg.norm(A, ord=1)
l2_norm = np.linalg.norm(A, ord=2)
linf_norm = np.linalg.norm(A, ord=np.inf)

print(norm_A, euclidean_dist, centered, scaled, add_vec, sub_vec,
      dot, theta_deg, unit_A, proj_A_on_B, l1_norm, l2_norm, linf_norm)
```
