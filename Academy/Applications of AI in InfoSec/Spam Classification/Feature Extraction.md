`Feature extraction` transforms preprocessed SMS messages into numerical vectors suitable for machine learning algorithms.

## Representing Text as Numerical Features

## 1. Bag-of-Words (BoW) model

- **Idea**: Turn text into numbers by counting word occurrences.
    
- **Process**:
    
    1. Build a vocabulary = all unique words in your dataset.  
        Example: `["free", "prize", "win", "today"]`
        
    2. Represent each message as a vector, where each element is the count of a vocabulary word in that message.
        

Example:  
Message: `"win a free prize"`  
Vector (BoW): `[1, 1, 1, 0]`  
(corresponds to `"free":1, "prize":1, "win":1, "today":0`)

👉 Notice: **order of words is ignored**. `"free prize"` and `"prize free"` get the same vector.

---

## 2. Limitation: Word order is lost

- Using **only unigrams** (individual words) treats text as a “bag” — we know which words appear and how often, but not in what sequence.
    
- Example:
    
    - `"dog bites man"` vs. `"man bites dog"`
        
    - Both give the same BoW representation, even though meaning is totally different.

## 3. Adding **bigrams**

- To regain some order information, we include **bigrams** (pairs of consecutive words).
    
- Now the vocabulary might include:
    
    - unigrams: `"free"`, `"prize"`, `"win"`
        
    - bigrams: `"free prize"`, `"win today"`
        

So the model not only knows that `"free"` and `"prize"` appear, but also that they appear **together in sequence**.

Example:  
Message: `"win a free prize"`  
Vector includes:

- `"free"` = 1
    
- `"prize"` = 1
    
- `"free prize"` = 1
    

This lets the model detect patterns like **“free prize”** (spammy) vs just “free” (maybe not spam).

## Using CountVectorizer for the Bag-of-Words Approach

`CountVectorizer` from the `scikit-learn` library efficiently implements the bag-of-words approach. It converts a collection of documents into a matrix of term counts, where each row represents a message and each column corresponds to a term (unigram or bigram). Before transformation, `CountVectorizer` applies tokenization, builds a vocabulary, and then maps each document to a numeric vector.

Key parameters for refining the feature set:

- `min_df=1`: A term must appear in at least one document to be included. While this threshold is set to `1` here, higher values can be used in practice to exclude rare terms.
- `max_df=0.9`: Terms that appear in more than 90% of the documents are excluded, removing overly common words that provide limited differentiation.
- `ngram_range=(1, 2)`: The feature matrix captures individual words and common word pairs by including unigrams and bigrams, potentially improving the model’s ability to detect spam patterns.

```python
from sklearn.feature_extraction.text import CountVectorizer

# Initialize CountVectorizer with bigrams, min_df, and max_df to focus on relevant terms
vectorizer = CountVectorizer(min_df=1, max_df=0.9, ngram_range=(1, 2))

# Fit and transform the message column
X = vectorizer.fit_transform(df["message"])

# Labels (target variable)
y = df["label"].apply(lambda x: 1 if x == "spam" else 0)  # Converting labels to 1 and 0
```

After this step, `X` becomes a numerical feature matrix ready to be fed into a classifier, such as Naive Bayes.
### How CountVectorizer Works

`CountVectorizer` operates in three main stages:

1. `Tokenization`: Splits the text into tokens based on the specified `ngram_range`. For `ngram_range=(1, 2)`, it extracts both unigrams (like "`message`") and bigrams (like "`free prize`").
2. `Building the Vocabulary`: Uses `min_df` and `max_df` to decide which terms to include. Terms that are too rare or common are filtered out, leaving a vocabulary that balances informative and distinctive terms.
3. `Vectorization`: Transforms each document into a vector of term counts. Each vector entry corresponds to a term from the vocabulary, and its value represents how many times that term appears in the document.
### Example with Unigrams

1. `The free prize is waiting for you`
2. `The spam message offers a free prize now`
3. `The spam filter might detect this`
4. `The important news says you won a free trip`
5. `The message truly is important`

If we use `ngram_range=(1, 1)` (unigrams only) and `min_df=1`, `max_df=0.9`, the word `The` will be removed from unigram vocabulary by `max_df=0.9` since it appears more than 90% in the documents, leaving the below unigram matrix:

|Document|free|prize|is|waiting|for|you|spam|message|offers|a|now|filter|might|detect|this|important|news|says|won|trip|truly|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1|1|1|1|1|1|1|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|
|2|1|1|0|0|0|0|1|1|1|1|1|0|0|0|0|0|0|0|0|0|0|
|3|0|0|0|0|0|0|1|0|0|0|0|1|1|1|1|0|0|0|0|0|0|
|4|1|0|0|0|0|1|0|0|0|1|0|0|0|0|0|1|1|1|1|1|0|
|5|0|0|1|0|0|0|0|1|0|0|0|0|0|0|0|1|0|0|0|0|1|

### Example with Bigrams

Using `ngram_range=(1, 2)`, the final vocabulary includes all of the above unigrams and any valid bigrams containing those unigrams. For instance, `free prize` occurs in Documents 1 and 2. The resulting matrix provides additional context, helping the model differentiate messages more effectively:

|Document|free|prize|is|waiting|for|you|spam|message|offers|a|now|filter|might|detect|this|important|news|says|won|trip|truly|free prize|prize is|is waiting|waiting for|for you|spam message|message offers|offers a|a free|prize now|spam filter|filter might|might detect|detect this|important news|news says|says you|you won|won a|free trip|message truly|truly is|is important|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1|1|1|1|1|1|1|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|1|1|1|1|1|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|
|2|1|1|0|0|0|0|1|1|1|1|1|0|0|0|0|0|0|0|0|0|0|1|0|0|0|0|1|1|1|1|1|0|0|0|0|0|0|0|0|0|0|0|0|0|
|3|0|0|0|0|0|0|1|0|0|0|0|1|1|1|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|1|1|1|1|0|0|0|0|0|0|0|0|0|
|4|1|0|0|0|0|1|0|0|0|1|0|0|0|0|1|1|1|1|1|0|0|0|0|0|0|0|0|0|0|1|0|0|0|0|0|1|1|1|1|1|1|0|0|0|
|5|0|0|1|0|0|0|0|1|0|0|0|0|0|0|1|0|0|0|0|0|1|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|1|1|1|







