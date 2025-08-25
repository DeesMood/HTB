# References

[https://aclanthology.org/P11-1015.pdf](https://www.google.com/url?q=https%3A%2F%2Faclanthology.org%2FP11-1015.pdf)

The `IMDB dataset` introduced by Maas et al. (2011) provides a collection of movie reviews extracted from the Internet Movie Database, annotated for `sentiment analysis`. It includes 50,000 reviews split evenly into training and test sets, and its carefully curated mixture of positive and negative examples allows researchers to benchmark and improve various natural language processing techniques. The `IMDB dataset` has influenced subsequent work in developing vector-based word representations and remains a popular baseline resource for evaluating classification performance and model architectures in sentiment classification tasks ([Maas et al., 2011](http://www.aclweb.org/anthology/P11-1015)).

Your goal is to train a model that can predict whether a movie review is positive (`1`) or negative (`0`). You can download the dataset from the question, or [from here](https://academy.hackthebox.com/storage/modules/292/skills_assessment_data.zip).

Out of interest, these exact same techniques can be applied into things such as text moderation for instance.

---

To evaluate your model, upload it to the evaluation portal running on the Playground VM. If you are not currently using the Playground VM, you can initialize it at the bottom of the page.
# ✅ Best first try (fast + strong)

Logistic Regression (or Linear SVM) on TF-IDF features

Why: Trains in minutes, very hard to beat on short reviews, interpretable.

How:

Clean text (lowercase, keep punctuation like “!” and “?”; keep emojis),

TfidfVectorizer with n-grams (1–2 or 1–3), min_df≈2–5,

Classifier: LogisticRegression (liblinear/saga) or LinearSVC.

Tip: Calibrate SVM (Platt/Isotonic) if you need well-behaved probabilities.

## _For more details look at the FAQ below._

---

1. Download and load the dataset
2. Preprocessing the dataset (removing duplicates, tokenizing, lowercasing, removing punctuations and numbers, deleting stopwords, stemming, join back(?) --> depends on logistic regression)
3. Feature extracting through TfidfVectorizer with ngram (1, 3)
4. Deploying a pipeline using sklearn library with logistic regression by using GridSearchCV
5. Saving the model using joblib

To evaluate your model, upload it to the evaluation portal running on the Playground VM. If you are not currently using the Playground VM, you can initialize it at the bottom of the page.

```python
import requests
import json

# Define the URL of the API endpoint
url = "http://localhost:5000/api/upload"

# Path to the model file you want to upload
model_file_path = "skills_assessment.joblib"

# Open the file in binary mode and send the POST request
with open(model_file_path, "rb") as model_file:
    files = {"model": model_file}
    response = requests.post(url, files=files)

# Pretty print the response from the server
print(json.dumps(response.json(), indent=4))
```

Flag: HTB{s3nt1m3nt_4n4lys1s_d4t4}