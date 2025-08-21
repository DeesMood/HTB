`Supervised learning` algorithms form the cornerstone of many `Machine Learning` (`ML`) applications, enabling systems to learn from labeled data and make accurate predictions.

The algorithm aims to learn a mapping function to predict the label for new, unseen data.

# **How Supervised Learning Works**

Imagine you're teaching a child to identify different fruits. You show them an apple and say, "This is an apple." You then show them an orange and say, "This is an orange." By repeatedly presenting examples with labels, the child learns to distinguish between the fruits based on their characteristics, such as color, shape, and size.

Supervised learning problems can be broadly categorized into two main types:

1. `Classification`: In classification problems, the goal is to predict a categorical label. For example, classifying emails as spam or not or identifying images of cats, dogs, or birds.
2. `Regression`: In regression problems, the goal is to predict a continuous value. For example, one could predict the price of a house based on its size, location, and other features or forecast the stock market.

# **Core Concepts in Supervised Learning**

## 🧩 Key Building Blocks

- **Training Data** → Examples with both inputs (features) and correct outputs (labels).
- **Features** → The input variables (e.g., house size, location).
- **Labels** → The target outcomes (e.g., actual house price).
- **Model** → The learned function mapping features → labels.

## ⚙️ The Learning Process

1. **Training** → Feed training data to the algorithm, adjust parameters to reduce error.
2. **Prediction** → Use trained model on unseen features to output labels.
3. **Inference** → Beyond prediction, also analyze relationships (e.g., which features matter most).
4. **Evaluation** → Measure performance using metrics:
    - Accuracy (overall correctness)
    - Precision (correct positive predictions)
    - Recall (capturing all true positives)
    - F1-score (balance of precision & recall)

## 🎯 Generalization & Model Quality

- **Generalization** → How well the model works on new, unseen data.
- **Overfitting** → Model memorizes training data (poor generalization).
- **Underfitting** → Model is too simple to capture patterns (bad on both training & test).

## 🛠 Techniques for Better Models

- **Cross-Validation** → is a technique used to assess how well a model will generalize to an independent dataset. It involves splitting the data into multiple subsets (folds) and training the model on different combinations of these folds while validating it on the remaining fold. This helps reduce overfitting and provides a more reliable estimate of the model's performance.
- **Regularization** → `Regularization` is a technique used to prevent overfitting by adding a penalty term to the loss function.
    - `L1 Regularization:` Adds a penalty equal to the absolute value of the magnitude of coefficients.
    - `L2 Regularization:` Adds a penalty equal to the square of the magnitude of coefficients.