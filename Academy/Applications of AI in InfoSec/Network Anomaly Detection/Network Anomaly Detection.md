`Anomaly detection` identifies data points that deviate significantly from the norm.

## Random Forests

- It’s an **ensemble method** → meaning it combines the results of many models (here, decision trees) to make one stronger model.
    
- The “forest” = a collection of decision trees.
    
- Each tree is trained slightly differently (on random subsets of data and features).

- **Training phase**:
    
    - Take random samples of the dataset (bootstrapping).
        
    - For each sample, build a decision tree.
        
    - At each split in the tree, consider only a random subset of features (this makes trees more diverse).
        
- **Prediction phase**:
    
    - **Classification**: Each tree votes for a class (spam vs ham, fraud vs not fraud, etc.). The final prediction is the class with the **majority of votes**.
        
    - **Regression**: Each tree outputs a number (like predicting house prices). The final prediction is the **average of all tree outputs**.

By combining the outputs of multiple trees, random forests often generalize better than a single decision tree, reducing `overfitting` and providing robust performance even in high-dimensional feature spaces.

Three key concepts shape the construction of a random forest:

1. `Bootstrapping`: Multiple subsets of the training data are created via sampling with replacement. Each subset trains a separate decision tree.
2. `Tree Construction` (random feature selection): For each tree, a random subset of features is considered at every split, ensuring diversity and reducing correlations among trees.
3. `Voting`: After all trees are trained, classification involves majority voting, while regression involves averaging predictions.

## Random Forests for Anomaly Detection

When used for anomaly detection, a random forest is trained exclusively on data representing normal conditions. New, unseen data points are then evaluated against this learned normal behavior. Points that do not fit well, or that produce low confidence predictions, are flagged as potential anomalies.
## NSL-KDD Dataset

The `NSL-KDD` dataset refines the original `KDD Cup 1999` dataset by eliminating redundant entries and correcting imbalanced class distributions. Researchers commonly adopt it as a standard reference for measuring the performance of various intrusion detection models.

We'll be using a modified version of this dataset.
## Downloading the Dataset

Before loading the NSL-KDD dataset, we must retrieve it from the provided URL. We can download the `.zip` file using Python's standard libraries and then extract it locally for further processing.

```python
import requests, zipfile, io

# URL for the NSL-KDD dataset
url = "https://academy.hackthebox.com/storage/modules/292/KDD_dataset.zip"

# Download the zip file and extract its contents
response = requests.get(url)
z = zipfile.ZipFile(io.BytesIO(response.content))
z.extractall('.')  # Extracts to the current directory
```
## Loading the Dataset

Properly loading the NSL-KDD dataset is essential before starting the preprocessing stage. This ensures that the data is consistently structured, with each column containing the correct information. Once loaded, the dataset can be inspected for quality, completeness, and potential preprocessing needs.

### Importing Libraries

```python
import numpy as np
import pandas as pd
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score, confusion_matrix, classification_report
import seaborn as sns
import matplotlib.pyplot as plt
```
In this snippet:

- `numpy` and `pandas` handle data loading and cleaning.
- `RandomForestClassifier` provides the algorithm we will use for anomaly detection.
- `train_test_split` and other metrics from `sklearn.metrics` support model evaluation and validation.
- `seaborn` and `matplotlib` assist in visualizing distributions, relationships, and model results.

### Defining Column Names and File Path

The NSL-KDD dataset includes a set of predefined features and labels. We must map these features to meaningful column names to work with them directly. We define a list of column names corresponding to the various observed characteristics of network connections and attacks. Additionally, we set `file_path` to point to the dataset file, ensuring that `pandas` know where to read the data from.

```python
# Set the file path to the dataset
file_path = r'KDD+.txt'

# Define the column names corresponding to the NSL-KDD dataset
columns = [
    'duration', 'protocol_type', 'service', 'flag', 'src_bytes', 'dst_bytes', 
    'land', 'wrong_fragment', 'urgent', 'hot', 'num_failed_logins', 'logged_in', 
    'num_compromised', 'root_shell', 'su_attempted', 'num_root', 'num_file_creations', 
    'num_shells', 'num_access_files', 'num_outbound_cmds', 'is_host_login', 'is_guest_login', 
    'count', 'srv_count', 'serror_rate', 'srv_serror_rate', 'rerror_rate', 'srv_rerror_rate', 
    'same_srv_rate', 'diff_srv_rate', 'srv_diff_host_rate', 'dst_host_count', 'dst_host_srv_count', 
    'dst_host_same_srv_rate', 'dst_host_diff_srv_rate', 'dst_host_same_src_port_rate', 
    'dst_host_srv_diff_host_rate', 'dst_host_serror_rate', 'dst_host_srv_serror_rate', 
    'dst_host_rerror_rate', 'dst_host_srv_rerror_rate', 'attack', 'level'
]
```

These column names ensure that each feature and label is properly identified. They include generic network statistics (e.g., `duration`, `src_bytes`, `dst_bytes`), categorical fields (`protocol_type`, `service`), and labels (`attack`, `level`), which classify the type of traffic observed.

### Reading the Dataset into a DataFrame

With the file path and column names defined, we load the data into a `pandas` DataFrame. This provides a structured, tabular representation of the dataset, making it easier to inspect, preprocess, and visualize.

```python
# Read the combined NSL-KDD dataset into a DataFrame
df = pd.read_csv(file_path, names=columns)
```

By executing this code, we now have a DataFrame `df` containing all the data from the NSL-KDD dataset with the appropriate column headers. The DataFrame is ready for further inspection, cleaning, and preprocessing steps. Before proceeding, we can briefly examine the dataset’s structure, check for missing values, and confirm that all features align with their intended data types.

![](attachments/Pasted%20image%2020250823181305.png)