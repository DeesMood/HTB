## Scikit-learn
`Scikit-learn` is a comprehensive library built on `NumPy`, `SciPy`, and `Matplotlib`.

- `Supervised Learning:` `Scikit-learn` provides a vast collection of supervised learning algorithms, including:
    - `Linear Regression`
    - `Logistic Regression`
    - `Support Vector Machines (SVMs)`
    - `Decision Trees`
    - `Naive Bayes`
    - `Ensemble Methods` (e.g., Random Forests, Gradient Boosting)
- `Unsupervised Learning:` It also offers various unsupervised learning algorithms, such as:
    - `Clustering` (K-Means, DBSCAN)
    - `Dimensionality Reduction` (PCA, t-SNE)
- `Model Selection and Evaluation:` `Scikit-learn` includes tools for model selection, hyperparameter tuning, and performance evaluation, enabling developers to optimize their models effectively.
- `Data Preprocessing:` It provides functionalities for data preprocessing, including:
    - Feature scaling and normalization
    - Handling missing values
    - Encoding categorical variables
### Data Preprocessing
`Scikit-learn` offers a rich set of tools for preprocessing data, a crucial step in preparing data for machine learning algorithms. These tools help transform raw data into a suitable format that improves the accuracy and efficiency of models.
`Scikit-learn` provides various scaling techniques:

- `StandardScaler` : Standardizes features by removing the mean and scaling to unit variance.
- `MinMaxScaler` : Scales features to a given range, typically between 0 and 1.
- `RobustScaler` : Scales features using statistics that are robust to outliers.
```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```
Categorical features, representing data in categories or groups, need to be converted into numerical representations for machine learning algorithms to process them. `Scikit-learn` offers encoding techniques:

- `OneHotEncoder` : Creates binary (0 or 1) columns for each category.
- `LabelEncoder` : Assigns a unique integer to each category.
```python
from sklearn.preprocessing import OneHotEncoder

encoder = OneHotEncoder()
X_encoded = encoder.fit_transform(X)
```
Real-world datasets often contain missing values. `Scikit-learn` provides methods to handle these missing values:

- `SimpleImputer` : Replaces missing values with a specified strategy (e.g., mean, median, most frequent).
- `KNNImputer` : Imputes missing values using the k-Nearest Neighbors algorithm.
```python
from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy='mean')
X_imputed = imputer.fit_transform(X)
```
### Model Selection and Evaluation
`Scikit-learn` offers tools for selecting the best model and evaluating its performance.

Splitting data into training and testing sets is crucial to evaluating the model's generalization ability to unseen data.
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
```
Cross-validation provides a more robust evaluation by splitting the data into multiple folds and training/testing on different combinations.
```python
from sklearn.model_selection import cross_val_score

scores = cross_val_score(model, X, y, cv=5)
```

`Scikit-learn` provides various metrics to evaluate model performance:

- `accuracy_score` : For classification tasks.
- `mean_squared_error` : For regression tasks.
- `precision_score`, `recall_score`, `f1_score` : For classification tasks with imbalanced classes.
```python
from sklearn.metrics import accuracy_score

accuracy = accuracy_score(y_test, y_pred)
```

### Model Training and Prediction
`Scikit-learn` follows a consistent API for training and predicting with different models.

Create an instance of the desired model with appropriate hyperparameters.

Code: python

```python
from sklearn.linear_model import LogisticRegression

model = LogisticRegression(C=1.0)
```

Train the model using the `fit()` method with the training data.

Code: python

```python
model.fit(X_train, y_train)
```

Make predictions on new data using the `predict()` method.

Code: python

```python
y_pred = model.predict(X_test)
```

## PyTorch
`PyTorch` is an open-source machine learning library developed by Facebook's AI Research lab. It provides a flexible and powerful framework for building and deploying various types of machine learning models, including deep learning models.

### Key Features

- `Deep Learning:` `PyTorch` excels in deep learning, enabling the development of complex neural networks with multiple layers and architectures.
- `Dynamic Computational Graphs:` Unlike static computational graphs used in libraries like TensorFlow, `PyTorch` uses dynamic computational graphs, which allow for more flexible and intuitive model building and debugging.
- `GPU Support:` `PyTorch` supports GPU acceleration, significantly speeding up the training process for computationally intensive models.
- `TorchVision Integration:` `TorchVision` is a library integrated with `PyTorch` that provides a user-friendly interface for image datasets, pre-trained models, and common image transformations.
- `Automatic Differentiation:` `PyTorch` uses `autograd` to automatically compute gradients, simplifying the process of backpropagation.
- `Community and Ecosystem:` `PyTorch` has a large and active community, leading to a rich ecosystem of tools, libraries, and resources.

### Dynamic Computational Graphs and Tensors
`Tensors` are multi-dimensional arrays that hold the data being processed. They can be constants, variables, or placeholders. `PyTorch` tensors are similar to NumPy arrays but can run on GPUs for faster computation.
```python
import torch

# Creating a tensor
x = torch.tensor([1.0, 2.0, 3.0])

# Tensors can be moved to GPU if available
if torch.cuda.is_available():
    x = x.to('cuda')
```

### Building Models with PyTorch
The `Sequential` API allows building models layer by layer, adding each layer sequentially.
```python
import torch.nn as nn

model = nn.Sequential(
    nn.Linear(784, 128),
    nn.ReLU(),
    nn.Linear(128, 10),
    nn.Softmax(dim=1)
)
```
