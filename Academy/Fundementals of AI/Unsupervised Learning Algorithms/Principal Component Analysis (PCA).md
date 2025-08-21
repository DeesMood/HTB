![](Pasted%20image%2020250821074743.png)
`Principal Component Analysis` (PCA) is a dimensionality reduction technique that transforms high-dimensional data into a lower-dimensional representation while preserving as much original information as possible.

Think of it as finding the most important "directions" in the data. Imagine a scatter plot of data points. PCA finds the lines that best capture the spread of the data. These lines represent the principal components.

There are three key concepts to PCA:

- `Variance:` Variance measures the spread or dispersion of data points around the mean. PCA aims to find principal components that maximize variance, capturing the most significant information in the data.
- `Covariance:` Covariance measures the relationship between two variables. PCA considers the covariance between different features to identify the directions of maximum variance.
- `Eigenvectors and Eigenvalues:` Eigenvectors represent the directions of the principal components, and eigenvalues represent the amount of variance explained by each principal component.

The PCA algorithm follows these steps:

1. `Standardize the data:` Subtract the mean and divide by the standard deviation for each feature to ensure that all features have the same scale.
2. `Calculate the covariance matrix:` Compute the covariance matrix of the standardized data, which represents the relationships between different features.
3. `Compute the eigenvectors and eigenvalues:` Determine the eigenvectors and eigenvalues of the covariance matrix. The eigenvectors represent the directions of the principal components, and the eigenvalues represent the amount of variance explained by each principal component.
4. `Sort the eigenvectors:` Sort the eigenvectors in descending order of their corresponding eigenvalues. The eigenvectors with the highest eigenvalues capture the most variance in the data.
5. `Select the principal components:` Choose the top `k` eigenvectors, where `k` is the desired number of dimensions in the reduced representation.
6. `Transform the data:` Project the original data onto the selected principal components to obtain the lower-dimensional representation.

## Eigenvalues and Eigenvectors
![](Pasted%20image%2020250821074954.png)
![](Pasted%20image%2020250821075007.png)

### The Eigenvalue Equation in Principal Component Analysis (PCA)
![](Pasted%20image%2020250821075102.png)

### Solving the Eigenvalue Equation
Solving this equation involves finding the eigenvectors and eigenvalues of the covariance matrix. This can be done using techniques like:

- `Eigenvalue Decomposition`: Directly computing the eigenvalues and eigenvectors.
- `Singular Value Decomposition (SVD)`: A more numerically stable method that decomposes the data matrix into singular vectors and singular values related to the eigenvectors and eigenvalues of the covariance matrix.

### Selecting Principal Components
Once the eigenvectors and eigenvalues are found, they are sorted in descending order of their corresponding eigenvalues. The top `k` eigenvectors (those with the largest eigenvalues) are selected to form the new feature space. These top `k` eigenvectors represent the principal components that capture the most significant variance in the data.
![](Pasted%20image%2020250821075440.png)
## Choosing the Number of Components
The number of principal components to retain is a crucial decision in PCA. It determines the trade-off between dimensionality reduction and information preservation.
## Data Assumptions
PCA makes certain assumptions about the data:

- `Linearity:` It assumes that the relationships between features are linear.
- `Correlation:` It works best when there is a significant correlation between features.

**What is the difference between linearity and correlation?**
****
### 1. **Linearity**

- Means the **model assumes a straight-line (linear) relationship** between input features and the output.
    
- Example: In linear regression, the model assumes
    
    y=β0+β1x1+β2x2+⋯+ϵy = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \epsilony=β0​+β1​x1​+β2​x2​+⋯+ϵ
    
    where the effect of each feature adds up linearly.
    
- If the true relationship is non-linear (e.g., quadratic, exponential), linear models may not fit well.
    

---

### 2. **Correlation**

- Refers to the **strength of relationship between features and the target (or between features themselves)**.
    
- For a linear model to work well, features should ideally have **some correlation with the target** (so they provide predictive signal).
    
- High correlation _between features_ (multicollinearity), however, can cause problems (unstable coefficients).

- `Scale:` It is sensitive to the scale of the features, so it is important to standardize the data before applying PCA. If one feature has a **larger numeric range** than others, it will dominate the principal components, even if it’s not actually more important.