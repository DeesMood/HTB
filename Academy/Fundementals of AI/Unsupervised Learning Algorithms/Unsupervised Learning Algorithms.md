`Unsupervised learning` algorithms explore unlabeled data, where the goal is not to predict a specific outcome but to discover hidden patterns, structures, and relationships within the data.

Think of it as exploring a new city without a map. You observe the surroundings, identify landmarks, and notice how different areas are connected.

# **How Unsupervised Learning Works**

`Unsupervised learning` algorithms identify similarities, differences, and patterns in the data. They can group similar data points together, reduce the number of variables while preserving essential information, or identify unusual data points that deviate from the norm.

`Unsupervised learning` problems can be broadly categorized into:

1. `Clustering:` Grouping similar data points together based on their characteristics.
2. `Dimensionality Reduction:` Reducing the number of variables (features) in the data while preserving essential information.
3. `Anomaly Detection:` Identifying unusual data points that deviate significantly from the norm.

# **Core Concepts in Unsupervised Learning**

## **Similarity Measures**

Many `unsupervised learning` algorithms rely on quantifying the similarity or dissimilarity between data points. Common measures include:

- `Euclidean Distance:` Measures the straight-line distance between two points in a multi-dimensional space.
- `Cosine Similarity:` Measures the angle between two vectors, representing data points, with higher values indicating greater similarity.
- `Manhattan Distance:` Calculates the distance between two points by summing the absolute differences of their coordinates.

## **Clustering Tendency**

`Clustering tendency` refers to the data's inherent propensity to form clusters or groups.

## **Cluster Validity**

Evaluating the quality and meaningfulness of the clusters produced by a clustering algorithm is crucial. `Cluster validity` involves assessing metrics like:

- `Cohesion:` Measures how similar data points are within a cluster. Higher cohesion indicates a more compact and well-defined cluster.
- `Separation:` Measures how different clusters are from each other. Higher separation indicates more distinct and well-separated clusters.

## **Dimensionality**

`Dimensionality` refers to the number of features or variables in the data.

## **Intrinsic Dimensionality**

The `intrinsic dimensionality` of data represents its inherent or underlying dimensionality, which may be lower than the actual number of features. It captures the essential information contained in the data. Dimensionality reduction techniques aim to reduce the number of features while preserving this intrinsic dimensionality.

## **Anomaly**

An `anomaly` is a data point that deviates significantly from the norm or expected pattern in the data.

## **Outlier**

An `outlier` is a data point that is far away from the majority of other data points.

## **Feature Scaling**

`Feature scaling` is essential in `unsupervised learning` to ensure that all features contribute equally to the distance calculations and other computations. Common techniques include:

- `Min-Max Scaling:` Scales features to a fixed range.
- `Standardization (Z-score normalization):` Transforms features to have zero mean and unit variance.