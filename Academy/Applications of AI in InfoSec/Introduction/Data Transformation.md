`Data transformations` improve the representation and distribution of features, making them more suitable for machine learning models.
## Encoding Categorical Features

`Encoding` converts categorical values into numeric form so machine learning algorithms can utilize these features. Depending on the situation, you can choose:

- `OneHotEncoder` for binary indicator features that represent each category separately. Makes a **separate column for each category**.
- `LabelEncoder` for integer codes, though this may imply unintended order. Gives each category a **number (integer code)**.
- `HashingEncoder` or frequency-based methods to handle high-cardinality features and control feature space size. Turns categories into numbers using a hashing function, controlling the number of output columns (good for huge category sets).

### One-Hot Encoding
`One-hot encoding` takes a categorical feature and converts it into a set of new binary features, where each binary feature corresponds to one possible category value. This process creates a set of indicator columns that hold `1` or `0`, indicating the presence or absence of a particular category in each row.

For example, consider the categorical feature `color`, which can take on the values `red`, `green`, or `blue`. In a dataset, you might have rows where `color` is `red` in one instance, `green` in another, and so on. By applying `one-hot encoding`, instead of keeping a single column with values like `red`, `green`, or `blue`, the encoding creates three new binary columns:

- `color_red`
- `color_green`
- `color_blue`

Each of these new columns corresponds to one of the original categories. If a row had `color` set to `red`, the `color_red` column for that row would be `1`, and the other two columns (`color_green` and `color_blue`) would be `0`. Similarly, if `color` was originally `green`, then the `color_green` column would be `1`, while the `color_red` and `color_blue` columns would be `0`.

![](attachments/Pasted%20image%2020250822153436.png)

In this case, we are going to encode the `protocol` feature.

```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder(handle_unknown='ignore', sparse_output=False)
encoded = encoder.fit_transform(df[['protocol']])

encoded_df = pd.DataFrame(encoded, columns=encoder.get_feature_names_out(['protocol']))
df = pd.concat([df.drop('protocol', axis=1), encoded_df], axis=1)
```

The original `protocol` feature is replaced with distinct binary columns, ensuring the model interprets each category independently.

## Handling Skewed Data
When a feature is `skewed`, its values are unevenly distributed, often with most observations clustered near one end and a few extreme values stretching out the distribution.
`Scaling` or transforming these skewed features helps models better capture patterns in the data. One common transformation is applying a `log` transform to compress large values more than small ones, resulting in a more balanced distribution and less dominated by outliers.
Below, we show how to apply a `log` transform using the `log1p` function. This approach adds 1 to each value before taking the `log`, ensuring that the transform is defined even for values at or near zero.

```python
import numpy as np

# Apply logarithmic transformation to a skewed feature to reduce its skewness
df["bytes_transferred"] = np.log1p(df["bytes_transferred"])  # Add 1 to avoid log(0)
```

The code above transforms the `bytes_transferred` feature. Before this transformation, the feature might have had a few very large values, overshadowing the majority of smaller observations. After the transformation, the distribution is evener, helping the model treat all data points fairly and reducing the risk of overfitting outliers.

### Left: Original Distribution

- The feature `bytes_transferred` is plotted.
    
- The bars are uneven and “skewed” — lots of values are bunched at the low end, while some very large values stretch far to the right.
    
- This makes it **hard for a model** to notice patterns, because the extreme values dominate.

### Right: Log-Transformed Distribution

- Instead of looking at the raw numbers, we take the **logarithm** (`log1p`, which means log(x+1)) of each value.
    
- The log “compresses” large numbers and “stretches out” small numbers.
    
- Now the distribution is more balanced and closer to normal (bell-shaped).

![](attachments/Pasted%20image%2020250822155216.png)
## Data Splitting

`Data splitting` involves dividing a dataset into three distinct subsets—`training`, `validation`, and `testing`—to ensure reliable model evaluation. By having separate sets, you can train your model on one subset, fine-tune it on another, and finally test its performance on data it has never seen before.

- `Training Set`: Used to fit the model. Typically accounts for around 60-80% of the entire dataset.
- `Validation Set`: Used for tuning hyperparameters and model selection. Often around 10-20% of the entire dataset.
A **validation set** is used to **try out different versions of your model** and see which one works better.

- Example: Should the model learn **fast or slow**?
    
- Should it use **5 layers or 10 layers**?
    
- Should it look at **3 neighbors or 7 neighbors**?

- `Test Set`: Used only after all model selections and tuning are complete. Often around 10-20% of the entire dataset.

The code below demonstrates one approach using `train_test_split` from `scikit-learn`. The initial split allocates 80% of the data for training and 20% for testing. A subsequent split divides the 80% training portion into 60% for final training and 20% for validation.

Note that `test_size=0.25` in the second split refers to 25% of the previously created training subset (which is 80% of the data). In other words, `0.8 × 0.25 = 0.2` (20% of the entire dataset), leaving 60% for training and 20% for validation overall.

```python
from sklearn.model_selection import train_test_split

# Separate features (X) and target (y)
X = df.drop("threat_level", axis=1)
y = df["threat_level"]

# Initial split: 80% training, 20% testing
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1337)

# Second split: from the 80% training portion, allocate 60% for final training and 20% for validation
X_train, X_val, y_train, y_val = train_test_split(X_train, y_train, test_size=0.25, random_state=1337)
```

These subsets support a structured workflow:

- Train the model on `X_train` and `y_train`.
- Tune hyperparameters or compare different models using `X_val` and `y_val`.
- Finally, evaluate the performance on the untouched `X_test` and `y_test`.



