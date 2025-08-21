![](Pasted%20image%2020250821073914.png)

Despite its name, `logistic regression` is a `supervised learning` algorithm primarily used for `classification`, not regression. It predicts a categorical target variable with two possible outcomes (binary classification). These outcomes are typically represented as binary values (e.g., 0 or 1, true or false, yes or no).

For example, logistic regression can predict whether an email is spam or not or whether a customer will click on an ad.

# **What is Classification?**

Unlike regression, which predicts a continuous value, classification predicts a discrete label.

Examples of classification problems include:

- Identifying fraudulent transactions (fraudulent or not fraudulent)
- Classifying images of animals (cat, dog, bird, etc.)
- Diagnosing diseases based on patient symptoms (disease present or not present)

# **How Logistic Regression Works**

Unlike `linear regression`, which outputs a continuous value, `logistic regression` outputs a probability score between 0 and 1.

# **What is a Sigmoid Function?**

![](Pasted%20image%2020250821073924.png)
![](Pasted%20image%2020250821073937.png)
# **Decision Boundary**

A crucial aspect of `logistic regression` is the `decision boundary`. In a simplified scenario with two features, imagine a line separating the data points into two classes. This separator is the `decision boundary`, determined by the model's learned parameters and the chosen threshold probability.

# **Understanding Hyperplanes**

![](Pasted%20image%2020250821073957.png)

# **Threshold Probability**

- If a given data point's predicted probability `P(x)` falls above the threshold, the instance is classified as the positive class.
- If `P(x)` falls below the threshold, it's classified as the negative class.

# **Data Assumptions**

- `Binary Outcome:` The target variable must be categorical, with only two possible outcomes.
- `Linearity of Log Odds:` It assumes a linear relationship between the predictor variables and the log-odds of the outcome. `Log odds` are a transformation of probability, representing the logarithm of the odds ratio (the probability of an event occurring divided by the probability of it not occurring).
- `No or Little Multicollinearity:` Ideally, there should be little to no `multicollinearity` among the predictor variables. `Multicollinearity` occurs when predictor variables are highly correlated, making it difficult to determine their individual effects on the outcome.
- `Large Sample Size:` Logistic regression performs better with larger datasets, allowing for more reliable parameter estimation.