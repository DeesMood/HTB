# **Algebraic Notations**

### Subscript Notation (`x_t`)

The subscript notation represents a variable indexed by `t,` often indicating a specific time step or state in a sequence. For example:

Code: python

```python
x_t = q(x_t | x_{t-2})

```

This notation is commonly used in sequences and time series data, where each `x_t` represents the value of `x` at time `t`.

**Norm (‖v‖):** size/length of vectors (Euclidean, L1, L∞).

![image.png](attachment:1434f5fc-1f33-42fc-95c0-842f55e6c4e3:image.png)

**Σ (Summation):** add up a sequence of terms.

## 📈 Logs & Exponentials

- **log₂(x):** base-2 log, used in information theory.
- **ln(x):** natural log, base _e_.
- **eˣ:** exponential growth/decay. (euler)
- **2ˣ:** exponential with base 2, common in binary systems.

## 🔲 Linear Algebra (Core for AI)

- **Matrix–Vector Multiplication (A·v):** applies transformation.
- **Matrix–Matrix Multiplication (A·B):** combine transformations.
- **Transpose (Aᵀ):** flip rows ↔ columns.
- **Inverse (A⁻¹):** undoes a transformation (if invertible).
- **Determinant (det A):** scalar telling invertibility/volume change.
- **Trace (tr A):** sum of diagonal elements.

## 🔗 Set Theory

- **Cardinality (|S|):** number of elements.
- **Union (A ∪ B):** combine sets.
- **Intersection (A ∩ B):** common elements.
- **Complement (Aᶜ):** everything not in A.

## ⚖️ Comparison Operators

- **≥, ≤, ==, !=** → inequalities and equality checks.

## 🔑 Eigenvalues & Eigenvectors

- **Eigenvalue (λ):** scalar showing how much a vector is stretched.
- **Eigenvector:** vector that only scales (doesn’t rotate) when multiplied by a matrix.
- Used in PCA and dimensionality reduction.

## 🛠 Functions & Operators

- **max/min:** largest/smallest values.
- **Reciprocal (1/x):** inverse value.
- **Ellipsis (...):** continuing sequence.
- **f(x):** function notation.

## 🎲 Probability & Statistics

- **Conditional Probability (P(x|y)):** probability given another event.
- **Expectation (E[X]):** average value.
- **Variance (Var(X)):** spread of data.
- **Standard Deviation (σ):** square root of variance.
- **Covariance (Cov(X, Y)):** how two variables move together.
- **Correlation (ρ(X, Y)):** normalized covariance (−1 to 1).