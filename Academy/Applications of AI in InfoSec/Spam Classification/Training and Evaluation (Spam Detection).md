## Training

After preprocessing the text data and extracting meaningful features, we train a machine-learning model for spam detection. We use the `Multinomial Naive Bayes` classifier, which is well-suited for text classification tasks due to its probabilistic nature and ability to efficiently handle large, sparse feature sets.

To streamline the entire process, we employ a `Pipeline`. A pipeline chains together the vectorization and modeling steps, ensuring that the same data transformation (in this case, `CountVectorizer`) is consistently applied before feeding the transformed data into the classifier. This approach simplifies both development and maintenance by encapsulating the feature extraction and model training into a single, unified workflow.

```python
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.naive_bayes import MultinomialNB
from sklearn.pipeline import Pipeline

# Build the pipeline by combining vectorization and classification
pipeline = Pipeline([
    ("vectorizer", vectorizer),
    ("classifier", MultinomialNB())
])
```

With the pipeline in place, we can easily integrate hyperparameter tuning to improve model performance. The objective is to find optimal parameter values for the classifier, ensuring that the model generalizes well and avoids overfitting.

To achieve this, we use `GridSearchCV`. This method systematically searches through specified hyperparameter values to identify the configuration that produces the best performance. In the case of `MultinomialNB`, we focus on the `alpha` parameter, a smoothing factor that adjusts how the model handles unseen words and prevents probabilities from being zero. We can balance bias and variance by tuning `alpha`, ultimately improving the model’s robustness.

### 🔹 What is **GridSearchCV**?

Think of it like a **trial-and-error machine**:

- You give it a list of possible parameter values.
    
- It tries each one.
    
- It tells you which one works best.
    

---

### 🔹 For **MultinomialNB** (Naive Bayes)

- The important parameter is **alpha**.
    
- **Alpha** = smoothing factor → prevents the model from giving **zero probability** to words it hasn’t seen before.
    
- Small alpha → fits the training data closely (low bias, but risk of overfitting).
    
- Larger alpha → more smoothing, ignores tiny details (higher bias, less variance).

```python
# Define the parameter grid for hyperparameter tuning
param_grid = {
    "classifier__alpha": [0.01, 0.1, 0.15, 0.2, 0.25, 0.5, 0.75, 1.0]
}

# Perform the grid search with 5-fold cross-validation and the F1-score as metric
grid_search = GridSearchCV(
    pipeline,
    param_grid,
    cv=5,
    scoring="f1"
)

# Fit the grid search on the full dataset
grid_search.fit(df["message"], y)

# Extract the best model identified by the grid search
best_model = grid_search.best_estimator_
print("Best model parameters:", grid_search.best_params_)
```

![](attachments/Pasted%20image%2020250823172623.png)

## Evaluation

![](attachments/Pasted%20image%2020250823172659.png)

After training and fine-tuning the spam detection model, assessing its performance on new, unseen SMS messages is critical. This evaluation helps verify how well the model generalizes to real-world data and highlights improvement areas. The evaluation mirrors the preprocessing and feature extraction steps applied during training, ensuring a consistent and fair assessment of the model’s true predictive capabilities.

### Setting Up the Evaluation Messages

We begin by providing a list of new SMS messages for evaluation. These messages represent the types of inputs the model might receive in real-world use, including promotional offers, routine communications, urgent alerts, reminders, and incentive-based spam.

```python
# Example SMS messages for evaluation
new_messages = [
    "Congratulations! You've won a $1000 Walmart gift card. Go to http://bit.ly/1234 to claim now.",
    "Hey, are we still meeting up for lunch today?",
    "Urgent! Your account has been compromised. Verify your details here: www.fakebank.com/verify",
    "Reminder: Your appointment is scheduled for tomorrow at 10am.",
    "FREE entry in a weekly competition to win an iPad. Just text WIN to 80085 now!",
]
```

### Preprocessing New Messages

Before predicting with the trained model, we must preprocess the new messages using the same steps applied during training. Consistent preprocessing ensures that the model receives data in the same format it was trained on. The `preprocess_message` function converts each message to lowercase, removes non-alphabetic characters, tokenizes the text, removes stop words, and applies stemming.

```python
import numpy as np
import re

# Preprocess function that mirrors the training-time preprocessing
def preprocess_message(message):
    message = message.lower()
    message = re.sub(r"[^a-z\s$!]", "", message)
    tokens = word_tokenize(message)
    tokens = [word for word in tokens if word not in stop_words]
    tokens = [stemmer.stem(word) for word in tokens]
    return " ".join(tokens)
```

```python
# Preprocess and vectorize messages
processed_messages = [preprocess_message(msg) for msg in new_messages]
```

### Vectorizing the Processed Messages

The model expects numerical input features. To achieve this, we apply the same vectorization method used during training. The `CountVectorizer` saved within the pipeline (`best_model.named_steps["vectorizer"]`) transforms the preprocessed text into a numerical feature matrix.

```python
# Transform preprocessed messages into feature vectors
X_new = best_model.named_steps["vectorizer"].transform(processed_messages)
```
### Making Predictions

With the data properly preprocessed and vectorized, we feed the new messages into the trained `MultinomialNB` classifier (`best_model.named_steps["classifier"]`). This classifier outputs both a predicted label (spam or not spam) and class probabilities, indicating the model’s confidence in its decision.

```python
# Predict with the trained classifier
predictions = best_model.named_steps["classifier"].predict(X_new)
prediction_probabilities = best_model.named_steps["classifier"].predict_proba(X_new)
```

### Displaying Predictions and Probabilities

The next step is to present the evaluation results. For each message, we display:

- The original text of the message.
- The predicted label (`Spam` or `Not-Spam`).
- The probability that the message is spam.
- The probability that the message is not spam.

This output provides insight into the model’s reasoning and confidence levels, making it easier to understand and trust the predictions.

```python
# Display predictions and probabilities for each evaluated message
for i, msg in enumerate(new_messages):
    prediction = "Spam" if predictions[i] == 1 else "Not-Spam"
    spam_probability = prediction_probabilities[i][1]  # Probability of being spam
    ham_probability = prediction_probabilities[i][0]   # Probability of being not spam
    
    print(f"Message: {msg}")
    print(f"Prediction: {prediction}")
    print(f"Spam Probability: {spam_probability:.2f}")
    print(f"Not-Spam Probability: {ham_probability:.2f}")
    print("-" * 50)
```

![](attachments/Pasted%20image%2020250823173625.png)

These results show that the model can differentiate between benign messages and a range of spam content, providing both a categorical decision and the underlying probability estimates.
### Using joblib for Saving Models

After confirming satisfactory performance, preserving the trained model to be reused later is often necessary. By saving the model to a file, users can avoid the computational expense of retraining it from scratch each time. This is especially helpful in production environments where quick predictions are required.

`joblib` is a Python library designed to efficiently serialize and deserialize Python objects, particularly those containing large arrays such as NumPy arrays or scikit-learn models. `Serialization` converts an in-memory object into a format that can be stored on disk or transmitted across networks. `Deserialization` involves converting the stored representation back into an in-memory object with the exact same state it had when saved.

```python
import joblib

# Save the trained model to a file for future use
model_filename = 'spam_detection_model.joblib'
joblib.dump(best_model, model_filename)

print(f"Model saved to {model_filename}")
```

![](attachments/spam_detection_model.joblib)

In this example, `best_model` likely refers to a finalized and tested pipeline or classifier. The file `spam_detection_model.joblib` will contain all the necessary information to predict new data. To reuse the model later, load it back into the environment:

```python
loaded_model = joblib.load(model_filename)
predictions = loaded_model.predict(new_messages)
```

