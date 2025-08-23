`Data preprocessing` transforms raw data into a suitable format for machine learning algorithms. Key techniques include:

- `Data Cleaning`: Handling missing values, removing duplicates, and smoothing noisy data.
- `Data Transformation`: Normalizing, encoding, scaling, and reducing data.
- `Data Integration`: Merging and aggregating data from multiple sources.
- `Data Formatting`: Converting data types and reshaping data structures.

## Identifying Invalid Values

In addition to missing values, we need to check for invalid values in specific columns. Here are some common checks for the given dataset.

### Checking for Invalid IP Addresses
To identify invalid `source_ip` values, you can use a regular expression to validate the IP addresses:
```python
import re

def is_valid_ip(ip):
    pattern = re.compile(r'^((25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$')
    return bool(pattern.match(ip))

# Check for invalid IP addresses
invalid_ips = data[~data['source_ip'].astype(str).apply(is_valid_ip)]
print(invalid_ips)
```
![](attachments/Pasted%20image%2020250822075900.png)

### Checking for Invalid Port Numbers
To identify invalid `destination_port` values, you can check if the port numbers are within the valid range (0-65535):
```python
def is_valid_port(port):
    try:
        port = int(port)
        return 0 <= port <= 65535
    except ValueError:
        return False

# Check for invalid port numbers
invalid_ports = data[~data['destination_port'].apply(is_valid_port)]
print(invalid_ports)
```
![](attachments/Pasted%20image%2020250822075939.png)

### Checking for Invalid Protocol Values
To identify invalid `protocol` values, you can check against a list of known protocols:
```python
valid_protocols = ['TCP', 'TLS', 'SSH', 'POP3', 'DNS', 'HTTPS', 'SMTP', 'FTP', 'UDP', 'HTTP']

# Check for invalid protocol values
invalid_protocols = data[~data['protocol'].isin(valid_protocols)]
print(invalid_protocols)
```
![](attachments/Pasted%20image%2020250822080208.png)

### Checking for Invalid Bytes Transferred
To identify invalid `bytes_transferred` values, you can check if the values are numeric and non-negative:
```python
def is_valid_bytes(bytes):
    try:
        bytes = int(bytes)
        return bytes >= 0
    except ValueError:
        return False

# Check for invalid bytes transferred
invalid_bytes = data[~data['bytes_transferred'].apply(is_valid_bytes)]
print(invalid_bytes)
```
![](attachments/Pasted%20image%2020250822080604.png)
### Checking for Invalid Threat Levels
To identify invalid `threat_level` values, you can check if the values are within a valid range (e.g., 0-2):
```python
def is_valid_threat_level(threat_level):
    try:
        threat_level = int(threat_level)
        return 0 <= threat_level <= 2
    except ValueError:
        return False

# Check for invalid threat levels
invalid_threat_levels = data[~data['threat_level'].apply(is_valid_threat_level)]
print(invalid_threat_levels)
```
![](attachments/Pasted%20image%2020250822080932.png)
## Handling Invalid Entries
There are a few different ways we can approach this bad data.
### Dropping Invalid Entries
The most straightforward approach is to discard the invalid entries entirely. This ensures that the remaining dataset is clean and free of potentially misleading information.

```python
# the ignore errors covers the fact that there might be some overlap between indexes that match other invalid criteria
data = data.drop(invalid_ips.index, errors='ignore') 
data = data.drop(invalid_ports.index, errors='ignore')
data = data.drop(invalid_protocols.index, errors='ignore')
data = data.drop(invalid_bytes.index, errors='ignore')
data = data.drop(invalid_threat_levels.index, errors='ignore')

print(data.describe(include='all'))
```
![](attachments/Pasted%20image%2020250822082038.png)

This method is generally preferred when data accuracy is paramount, and the loss of some data points does not significantly compromise the overall analysis. However, it may not always be feasible, especially if the dataset is small or the invalid entries constitute a substantial portion of the data.

After dropping the bad data from our dataset, we are only left with 77 clean entries.

### Imputing Missing Values

`Imputing` is the process of replacing missing or invalid values in a dataset with estimated values.

First, convert all invalid or corrupted entries, such as `MISSING_IP`, `INVALID_IP`, `STRING_PORT`, `UNUSED_PORT`, `NON_NUMERIC`, or `?`, into `NaN`.

```python
import pandas as pd
import numpy as np
import re
from ipaddress import ip_address

df = pd.read_csv('demo_dataset.csv')

invalid_ips = ['INVALID_IP', 'MISSING_IP']
invalid_ports = ['STRING_PORT', 'UNUSED_PORT']
invalid_bytes = ['NON_NUMERIC', 'NEGATIVE']
invalid_threat = ['?']

df.replace(invalid_ips + invalid_ports + invalid_bytes + invalid_threat, np.nan, inplace=True)

df['destination_port'] = pd.to_numeric(df['destination_port'], errors='coerce')
df['bytes_transferred'] = pd.to_numeric(df['bytes_transferred'], errors='coerce')
df['threat_level'] = pd.to_numeric(df['threat_level'], errors='coerce')

def is_valid_ip(ip):
    pattern = re.compile(r'^((25[0-5]|2[0-4][0-9]|[01]?\d?\d)\.){3}(25[0-5]|2[0-4]\d|[01]?\d?\d)$')
    if pd.isna(ip) or not pattern.match(str(ip)):
        return np.nan
    return ip

df['source_ip'] = df['source_ip'].apply(is_valid_ip)
```

After this step, `NaN` represents all missing or invalid data points.

For basic numeric columns like `bytes_transferred`, use simple methods such as the median or mean. For categorical columns like `protocol`, use the most frequent value.

```python
from sklearn.impute import SimpleImputer

numeric_cols = ['destination_port', 'bytes_transferred', 'threat_level']
categorical_cols = ['protocol']

num_imputer = SimpleImputer(strategy='median')
df[numeric_cols] = num_imputer.fit_transform(df[numeric_cols])

cat_imputer = SimpleImputer(strategy='most_frequent')
df[categorical_cols] = cat_imputer.fit_transform(df[categorical_cols])
```

These imputations ensure that all columns have valid, non-missing values, though they do not consider complex relationships among features.

For more sophisticated scenarios, employ advanced techniques like `KNNImputer` or `IterativeImputer`. These methods consider relationships among features to produce contextually meaningful imputations.

```python
from sklearn.impute import KNNImputer

knn_imputer = KNNImputer(n_neighbors=5)
df[numeric_cols] = knn_imputer.fit_transform(df[numeric_cols])
```

- **Missing IPs** → if no IP is available, replace it with a placeholder like `0.0.0.0`.
    
- **Protocols** → check that the protocol (like TCP, HTTP, UDP) is one of the valid, known ones.
    
- **Ports** → make sure port numbers are only between **0 and 65535** (the valid range).
    
- **Protocol-port rules** → sometimes a protocol implies certain ports (e.g., HTTP usually uses port 80). In such cases, you can use the most common value (mode) or rules specific to your field.

```python
valid_protocols = ['TCP', 'TLS', 'SSH', 'POP3', 'DNS', 'HTTPS', 'SMTP', 'FTP', 'UDP', 'HTTP']
df.loc[~df['protocol'].isin(valid_protocols), 'protocol'] = df['protocol'].mode()[0]

df['source_ip'] = df['source_ip'].fillna('0.0.0.0')
df['destination_port'] = df['destination_port'].clip(lower=0, upper=65535)
```

### ✅ Why you need both

- **Step 1: `SimpleImputer`** → fixes missing values (`NaN`).
    
- **Step 2: `.loc`** → fixes wrong/unknown values (like `"INVALID_PROTO"`).

Perform final verification steps to confirm that distributions are reasonable and categorical sets remain valid. Adjust imputation strategies and transformations or remove problematic records if anomalies persist.

```python
print(df.describe(include='all'))
```