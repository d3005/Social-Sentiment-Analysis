# Social-Sentiment-Analysis
# Sentiment Analysis Report

## Overview

This project involved the analysis of tweet data to classify the sentiment of each tweet as either positive, negative, or neutral. The following steps were taken to preprocess the data, extract features, train a classification model, and evaluate its performance.

## Dataset

- **Source**: A CSV file containing tweet data.
- **Columns**:
  - `textID`: A unique identifier for each tweet.
  - `text`: The full text of the tweet.
  - `selected_text`: The specific part of the tweet that was highlighted as relevant to the sentiment.
  - `sentiment`: The sentiment label associated with the tweet (e.g., positive, negative, neutral).

## Technologies Used

### 1. **Pandas**
   - **Purpose**: Data loading and manipulation.
   - **Functions**:
     - `pd.read_csv()`: To load the CSV file.
     - `data['column_name'].apply()`: To apply the preprocessing function to each tweet.

### 2. **Regular Expressions (re)**
   - **Purpose**: Text preprocessing.
   - **Functions**:
     - `re.sub()`: To remove URLs, mentions, hashtags, numbers, special characters, and extra spaces.

### 3. **Scikit-learn (sklearn)**
   - **Purpose**: Feature extraction, model training, and evaluation.
   - **Modules**:
     - `TfidfVectorizer`: Converts the cleaned text into numerical features.
     - `train_test_split`: Splits the data into training and testing sets.
     - `LogisticRegression`: A simple and effective linear classifier for sentiment analysis.
     - `accuracy_score`: Measures the accuracy of the model's predictions.
     - `classification_report`: Provides a detailed classification report including precision, recall, F1-score, and support.

### 4. **Natural Language Toolkit (NLTK)**
   - **Purpose**: Originally intended for stopword removal, but this step was removed in the final version.
   - **Modules**:
     - `nltk.corpus.stopwords`: Stopword removal (not used in the final version).

## Preprocessing

The text in the tweets was preprocessed to remove unnecessary elements that could hinder the classification process. The following steps were applied:

1. **Removing URLs**: `re.sub(r'http\S+', '', text)`
2. **Removing Mentions**: `re.sub(r'@\w+', '', text)`
3. **Removing Hashtags**: `re.sub(r'#\w+', '', text)`
4. **Removing Numbers**: `re.sub(r'\d+', '', text)`
5. **Converting to Lowercase**: `text.lower()`
6. **Removing Special Characters**: `re.sub(r'\W', ' ', text)`
7. **Removing Extra Spaces**: `re.sub(r'\s+', ' ', text)`
8. **Trimming Whitespace**: `text.strip()`

## Feature Extraction

The preprocessed text was transformed into numerical features using the **TF-IDF (Term Frequency-Inverse Document Frequency)** vectorizer:

- **Maximum Features**: 5000 (limits the feature space to the top 5000 most frequent terms).

Here's the entire report in Markdown format:

markdown
Copy code
# Sentiment Analysis Report

## Overview

This project involved the analysis of tweet data to classify the sentiment of each tweet as either positive, negative, or neutral. The following steps were taken to preprocess the data, extract features, train a classification model, and evaluate its performance.

## Dataset

- **Source**: A CSV file containing tweet data.
- **Columns**:
  - `textID`: A unique identifier for each tweet.
  - `text`: The full text of the tweet.
  - `selected_text`: The specific part of the tweet that was highlighted as relevant to the sentiment.
  - `sentiment`: The sentiment label associated with the tweet (e.g., positive, negative, neutral).

## Technologies Used

### 1. **Pandas**
   - **Purpose**: Data loading and manipulation.
   - **Functions**:
     - `pd.read_csv()`: To load the CSV file.
     - `data['column_name'].apply()`: To apply the preprocessing function to each tweet.

### 2. **Regular Expressions (re)**
   - **Purpose**: Text preprocessing.
   - **Functions**:
     - `re.sub()`: To remove URLs, mentions, hashtags, numbers, special characters, and extra spaces.

### 3. **Scikit-learn (sklearn)**
   - **Purpose**: Feature extraction, model training, and evaluation.
   - **Modules**:
     - `TfidfVectorizer`: Converts the cleaned text into numerical features.
     - `train_test_split`: Splits the data into training and testing sets.
     - `LogisticRegression`: A simple and effective linear classifier for sentiment analysis.
     - `accuracy_score`: Measures the accuracy of the model's predictions.
     - `classification_report`: Provides a detailed classification report including precision, recall, F1-score, and support.

### 4. **Natural Language Toolkit (NLTK)**
   - **Purpose**: Originally intended for stopword removal, but this step was removed in the final version.
   - **Modules**:
     - `nltk.corpus.stopwords`: Stopword removal (not used in the final version).

## Preprocessing

The text in the tweets was preprocessed to remove unnecessary elements that could hinder the classification process. The following steps were applied:

1. **Removing URLs**: `re.sub(r'http\S+', '', text)`
2. **Removing Mentions**: `re.sub(r'@\w+', '', text)`
3. **Removing Hashtags**: `re.sub(r'#\w+', '', text)`
4. **Removing Numbers**: `re.sub(r'\d+', '', text)`
5. **Converting to Lowercase**: `text.lower()`
6. **Removing Special Characters**: `re.sub(r'\W', ' ', text)`
7. **Removing Extra Spaces**: `re.sub(r'\s+', ' ', text)`
8. **Trimming Whitespace**: `text.strip()`

## Feature Extraction

The preprocessed text was transformed into numerical features using the **TF-IDF (Term Frequency-Inverse Document Frequency)** vectorizer:

- **Maximum Features**: 5000 (limits the feature space to the top 5000 most frequent terms).
### Model Training
A Logistic Regression model was used to classify the sentiment of the tweets:

**Training:** The model was trained on 80% of the dataset.
**Testing:** The remaining 20% was used for evaluation.

```python
tfidf = TfidfVectorizer(max_features=5000)
X = tfidf.fit_transform(data['cleaned_text']).toarray()
y = data['sentiment']
```
## Evaluation
The model's performance was evaluated using the following metrics:

**Accuracy:** The overall accuracy of the model on the test set.
**Classification Report:** A detailed breakdown of precision, recall, F1-score, and support for each sentiment class.
'''python
y_pred = model.predict(X_test)
accuracy = accuracy_score(y_test, y_pred)
classification_rep = classification_report(y_test, y_pred)

print("Accuracy:", accuracy)
print("Classification Report:\n", classification_rep)
