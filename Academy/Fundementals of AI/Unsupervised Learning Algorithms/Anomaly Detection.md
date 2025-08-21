![](Pasted%20image%2020250821081016.png)
`Anomaly detection`, also known as outlier detection, is crucial in `unsupervised learning`. It identifies data points that deviate significantly from normal behavior within a dataset.

Anomalies can be broadly categorized into three types:

- `Point Anomalies:` Individual data points significantly differ from the rest—for example, a sudden spike in network traffic or an unusually high credit card transaction amount.
- `Contextual Anomalies:` Data points considered anomalous within a specific context but not necessarily in isolation. For example, a temperature reading of 30°C might be expected in summer but anomalous in winter.
- `Collective Anomalies:` A group of data points that collectively deviate from the normal behavior, even though individual data points might not be considered anomalous. For example, a sudden surge in login attempts from multiple unknown IP addresses could indicate a coordinated attack.

Various techniques are employed for anomaly detection, including:

- `Statistical Methods:` These methods assume that normal data points follow a specific statistical distribution (e.g., Gaussian distribution) and identify outliers as data points that deviate significantly from this distribution. Examples include z-score, modified z-score, and boxplots.
- `Clustering-Based Methods:` These methods group similar data points together and identify outliers as data points that do not belong to any cluster or belong to small, sparse clusters. `K-means clustering` and density-based clustering are commonly used for anomaly detection.
- `Machine Learning-Based Methods:` These methods utilize machine learning algorithms to learn patterns from normal data and identify outliers as data points that do not conform to these patterns. Examples include `One-Class SVM`, `Isolation Forest`, and `Local Outlier Factor (LOF)`.

### One-Class SVM

![](Pasted%20image%2020250821081205.png)
`One-Class SVM` is a machine learning algorithm specifically designed for anomaly detection. It learns a boundary that encloses the normal data points and identifies any data point falling outside this boundary as an outlier. It's like drawing a fence around a sheep pen – any sheep found outside the fence is likely an anomaly. `One-Class SVM` can handle non-linear relationships using kernel functions, similar to SVMs used for classification.
### Isolation Forest

![](Pasted%20image%2020250821081236.png)

![](Pasted%20image%2020250821081347.png)

### Local Outlier Factor (LOF)

![](Pasted%20image%2020250821081357.png)

`Local Outlier Factor (LOF)` is a density-based algorithm designed to identify outliers in datasets by comparing the local density of a data point to that of its neighbors.  It is particularly effective in detecting anomalies in regions where the density of points varies significantly.
![](Pasted%20image%2020250821081449.png)

### Local Reachability Density
![](Pasted%20image%2020250821081506.png)
### Data Assumptions
- `Normal Data Distribution:` Some methods assume that normal data points, such as Gaussian distribution, follow a specific distribution.
- `Feature Relevance:` The choice of features can significantly impact the performance of anomaly detection algorithms.
- `Labeled Data (for some methods):` Some machine learning-based methods require labeled data to train the model.


