![](Pasted%20image%2020250821074025.png)

In essence, a decision tree creates a model that predicts the value of a target variable by learning simple decision rules inferred from the data features.

Imagine you're trying to decide whether to play tennis based on the weather. A decision tree would break down this decision into a series of simple questions: Is it sunny? Is it windy? Is it humid? Based on the answers to these questions, the tree would lead you to a final decision: play tennis or don't play tennis.

Component of a decision tree:

- `Root Node:` This represents the starting point of the tree and contains the entire dataset.
- `Internal Nodes:` These nodes represent features or attributes of the data. Each internal node branches into two or more child nodes based on different decision rules.
- `Leaf Nodes:` These are the terminal nodes of the tree, representing the final outcome or prediction.

# **Building a Decision Tree**

the data at each node. This selection is based on measures like `Gini impurity`, `entropy`, or `information gain.`The goal is to create splits that result in increasingly pure subsets, where the data points within each subset belong predominantly to the same class.

### Gini Impurity

`Gini impurity` measures the probability of misclassifying a randomly chosen element from a set. A lower Gini impurity indicates a more pure set. The formula for Gini impurity is:

Code: python

```python
Gini(S) = 1 - Σ (pi)^2

```

Where:

- `S` is the dataset.
- `pi` is the proportion of elements belonging to class `i` in the set.

Consider a dataset `S` with two classes: `A` and `B`. Suppose there are 30 instances of class `A` and 20 instances of class `B` in the dataset.

- Proportion of class `A`: `pA = 30 / (30 + 20) = 0.6`
- Proportion of class `B`: `pB = 20 / (30 + 20) = 0.4`

The Gini impurity for this dataset is:

Code: python

```python
Gini(S) = 1 - (0.6^2 + 0.4^2) = 1 - (0.36 + 0.16) = 1 - 0.52 = 0.48

```

### Entropy

`Entropy` measures the disorder or uncertainty in a set. A lower entropy indicates a more homogenous set. The formula for entropy is:

Code: python

```python
Entropy(S) = - Σ pi * log2(pi)

```

Where:

- `S` is the dataset.
- `pi` is the proportion of elements belonging to class `i` in the set.

Using the same dataset `S` with 30 instances of class `A` and 20 instances of class `B`:

- Proportion of class `A`: `pA = 0.6`
- Proportion of class `B`: `pB = 0.4`

The entropy for this dataset is:

Code: python

```python
Entropy(S) = - (0.6 * log2(0.6) + 0.4 * log2(0.4))
           = - (0.6 * (-0.73697) + 0.4 * (-1.32193))
           = - (-0.442182 - 0.528772)
           = 0.970954

```

### Information Gain

`Information gain` measures the reduction in entropy achieved by splitting a set based on a particular feature. The feature with the highest information gain is chosen for the split. The formula for information gain is:

Code: python

```python
Information Gain(S, A) = Entropy(S) - Σ ((|Sv| / |S|) * Entropy(Sv))

```

Where:

- `S` is the dataset.
- `A` is the feature used for splitting.
- `Sv` is the subset of `S` for which feature `A` has value `v`.

Consider a dataset `S` with 50 instances and two classes: `A` and `B`. Suppose we consider a feature `F` that can take on two values: `1` and `2`. The distribution of the dataset is as follows:

- For `F = 1`: 30 instances, 20 class `A`, 10 class `B`
- For `F = 2`: 20 instances, 10 class `A`, 10 class `B`

First, calculate the entropy of the entire dataset `S`:

Code: python

```python
Entropy(S) = - (30/50 * log2(30/50) + 20/50 * log2(20/50))
           = - (0.6 * log2(0.6) + 0.4 * log2(0.4))
           = - (0.6 * (-0.73697) + 0.4 * (-1.32193))
           = 0.970954

```

Next, calculate the entropy for each subset `Sv`:

- For `F = 1`:
    - Proportion of class `A`: `pA = 20/30 = 0.6667`
    - Proportion of class `B`: `pB = 10/30 = 0.3333`
    - Entropy(S1) = `(0.6667 * log2(0.6667) + 0.3333 * log2(0.3333)) = 0.9183`
- For `F = 2`:
    - Proportion of class `A`: `pA = 10/20 = 0.5`
    - Proportion of class `B`: `pB = 10/20 = 0.5`
    - Entropy(S2) = `(0.5 * log2(0.5) + 0.5 * log2(0.5)) = 1.0`

Now, calculate the weighted average entropy of the subsets:

Code: python

```python
Weighted Entropy = (|S1| / |S|) * Entropy(S1) + (|S2| / |S|) * Entropy(S2)
                 = (30/50) * 0.9183 + (20/50) * 1.0
                 = 0.55098 + 0.4
                 = 0.95098

```

Finally, calculate the information gain:

Code: python

```python
Information Gain(S, F) = Entropy(S) - Weighted Entropy
                       = 0.970954 - 0.95098
                       = 0.019974

```

The tree stops growing when one of the following conditions is satisfied:

- `Maximum Depth` : The tree reaches a specified maximum depth, preventing it from becoming overly complex and potentially over fitting the data.
- `Minimum Number of Data Points` : The number of data points in a node falls below a specified threshold, ensuring that the splits are meaningful and not based on very small subsets.
- `Pure Nodes` : All data points in a node belong to the same class, indicating that further splits would not improve the purity of the subsets.

## Data Assumptions

One of the advantages of decision trees is that they have minimal assumptions about the data:

- `No Linearity Assumption:` Decision trees can handle linear and non-linear relationships between features and the target variable. This makes them more flexible than algorithms like linear regression, which assume a linear relationship.
- `No Normality Assumption:` The data does not need to be normally distributed. This contrasts some statistical methods that require normality for valid inferences.
- `Handles Outliers:` Decision trees are relatively robust to outliers.