![](Pasted%20image%2020250821074135.png)

`Support Vector Machines` (SVMs) are powerful `supervised learning` algorithms for `classification` and `regression` tasks. They are particularly effective in handling high-dimensional data and complex non-linear relationships between features and the target variable. SVMs aim to find the optimal `hyperplane` that maximally separates different classes or fits the data for regression. An SVM aims to find the hyperplane that maximizes the `margin`. The `margin` is the distance between the hyperplane and the nearest data points of each class. These nearest data points are called `support vectors` and are crucial in defining the hyperplane and the margin.

A `linear SVM` is used when the data is linearly separable, meaning a straight line or hyperplane can perfectly separate the classes.

# **Finding the Optimal Hyperplane**

![](Pasted%20image%2020250821074143.png)

The `optimal hyperplane` is the one that maximizes the margin between the closest data points of different classes.

![](Pasted%20image%2020250821074156.png)

# **Non-Linear SVM**

![](Pasted%20image%2020250821074205.png)

`Non-linear SVMs` utilize a technique called the `kernel trick`. This involves using a `kernel function` to map the original data points into a higher-dimensional space where they become linearly separable.

Imagine separating a mixture of red and blue marbles on a table. If the marbles are mixed in a complex pattern, you might be unable to draw a straight line to separate them. However, if you could lift some marbles off the table (into a higher dimension), you might be able to find a plane that separates them.

### Kernel Functions

Several kernel functions are commonly used in `non-linear SVMs`:

- `Polynomial Kernel:` This kernel introduces polynomial terms (like x², x³, etc.) to capture non-linear relationships between features. It's like adding curves to the decision boundary.
- `Radial Basis Function (RBF) Kernel:` This kernel uses a Gaussian function to map data points to a higher-dimensional space. It's one of the most popular and versatile kernel functions, capable of capturing complex non-linear patterns.
- `Sigmoid Kernel:` This kernel is similar to the sigmoid function used in logistic regression. It introduces non-linearity by mapping the data points to a space with a sigmoid-shaped decision boundary.

`Non-linear SVMs` are particularly useful in applications like image classification. Images often have complex patterns that linear boundaries cannot separate.

![](Pasted%20image%2020250821074222.png)

# **Data Assumptions**

- `No Distributional Assumptions:` SVMs do not make strong assumptions about the underlying distribution of the data.
- `Handles High Dimensionality:` They are effective in high-dimensional spaces, where the number of features is larger than the number of data points.
- `Robust to Outliers:` SVMs are relatively robust to outliers, focusing on maximizing the margin rather than fitting all data points perfectly.