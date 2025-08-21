![](Pasted%20image%2020250821074100.png)

`Naive Bayes` is a probabilistic algorithm used for `classification` tasks. It's based on `Bayes' theorem. Naive Bayes` is a popular choice for tasks like spam filtering and sentiment analysis due to its simplicity, efficiency, and surprisingly good performance in many real-world scenarios.

# **Bayes' Theorem**

![](Pasted%20image%2020250821074112.png)

# **How Naive Bayes Works**

The `Naive Bayes` classifier leverages `Bayes' theorem` to predict the probability of a data point belonging to a particular class given its features. To do this, it makes the "naive" assumption of conditional independence among the features. This means it assumes that the presence or absence of one feature doesn't affect the presence or absence of any other feature, given that we know the class label.

Let's break down how this works in practice:

- `Calculate Prior Probabilities:` The algorithm first calculates the prior probability of each class.
- `Calculate Likelihoods:` Next, the algorithm calculates the likelihood of observing each feature given each class.
- `Apply Bayes' Theorem:` For a new data point, the algorithm combines the prior probabilities and likelihoods using `Bayes' theorem` to calculate the `posterior probability` of the data point belonging to each class.
- `Predict the Class:` Finally, the algorithm assigns the data point to the class with the highest posterior probability.

# **Types of Naive Bayes Classifiers**

- `Gaussian Naive Bayes:` This is used when the features are continuous and assumed to follow a Gaussian distribution (a bell curve).
- `Multinomial Naive Bayes:` This is suitable for discrete features and is often used in text classification. For instance, in spam filtering, the frequency of words like "free" or "money" might be the features, and `Multinomial Naive Bayes` would model the probability of these words appearing in spam and non-spam emails.
- `Bernoulli Naive Bayes:` This type is employed for binary features, where the feature is either present or absent.

## Data Assumptions

While Naive Bayes is relatively robust, it's helpful to be aware of some data assumptions:

- `Feature Independence:` As discussed, the core assumption is that features are conditionally independent given the class.
- `Data Distribution:` The choice of Naive Bayes classifier (Gaussian, Multinomial, Bernoulli) depends on the assumed distribution of the features.
- `Sufficient Training Data:` Although Naive Bayes can work with limited data, it is important to have sufficient data to estimate probabilities accurately.