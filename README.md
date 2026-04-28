# Applied Text Analytics: Emirates Airline Employee Experience and Workplace Culture Analysis

## Project Overview
This project focuses on analyzing employee experiences and workplace culture at Emirates Airline through sentiment analysis and topic modeling of YouTube comments. The goal is to extract insights from public discussions to understand employee sentiment, identify key themes, and provide actionable recommendations.

## Table of Contents
1.  [Objective](#objective)
2.  [Methodology](#methodology)
    *   [Data Collection](#data-collection)
    *   [Data Cleaning & Preprocessing](#data-cleaning--preprocessing)
    *   [Sentiment Analysis](#sentiment-analysis)
    *   [Feature Extraction & Model Training](#feature-extraction--model-training)
    *   [Topic Modeling](#topic-modeling)
3.  [Key Findings & Insights](#key-findings--insights)
4.  [How to Run the Project](#how-to-run-the-project)
5.  [Generated Files](#generated-files)

## Objective
The primary objective of this project is to build a real-world dataset of employee-related discussions by automatically collecting public comments from YouTube using the YouTube Data API. These comments are then analyzed to uncover diverse opinions, experiences, and sentiments about Emirates Airline's employee experience and workplace culture.

## Methodology

### Data Collection
Public comments related to "working at Emirates," "Emirates employee experience," etc., were collected from YouTube using the YouTube Data API. A custom scraping function was developed to gather comments from relevant videos, aiming for a target number of comments.

### Data Cleaning & Preprocessing
-   Initial data quality checks were performed for missing values, duplicates, and comment length.
-   Comments were cleaned by removing URLs, mentions, emojis, and extra spaces.
-   Language detection was used to filter for English-only comments.
-   A custom heuristic-based function (`looks_like_employee_post`) was developed to identify and retain only employee-relevant comments, filtering out customer-related feedback or application questions.
-   Text preprocessing steps included lowercasing, punctuation removal, stop word removal, and lemmatization.

### Sentiment Analysis
-   Both TextBlob and VADER (Valence Aware Dictionary and sEntiment Reasoner) sentiment analysis tools were applied to each cleaned comment.
-   A consensus-based labeling strategy was adopted: if both TextBlob and VADER agreed, that label was used. If they disagreed, VADER's label was chosen due to its optimization for social media text.
-   The dataset was split into 80% training and 20% testing sets, stratified to maintain class distribution.

### Feature Extraction & Model Training
-   **Feature Representations**: Several techniques were used for converting text into numerical features:
    -   Binary Bag-of-Words (unigrams)
    -   Count Bag-of-Words (unigrams)
    -   TF-IDF (unigrams, bigrams, and 1-3 grams)
-   **Classification Models**: Six different classifiers were implemented and compared:
    -   Multinomial Naive Bayes
    -   Bernoulli Naive Bayes
    -   Logistic Regression (L2 and L1 regularization)
    -   Linear SVM
    -   Random Forest
-   Models were trained and evaluated across all feature representations, and performance metrics (Accuracy, Precision, Recall, F1-Score) were recorded.

### Topic Modeling
-   Latent Dirichlet Allocation (LDA) was used to identify latent topics within the corpus of employee-relevant comments. The `gensim` library was employed for this purpose.
-   Human-readable labels were assigned to the discovered topics to facilitate interpretation.
-   An interactive visualization of the LDA model was generated using `pyLDAvis`.
-   The dominant topic for each comment was identified, and the distribution of sentiments across these topics was analyzed and visualized.

## Key Findings & Insights

**Overall Sentiment:**
-   76.7% of comments were positive.
-   13.9% were negative.
-   9.4% were neutral.

**Most Discussed Topics:**
-   **Employment Conditions**: 29.8% of mentions.
-   **Aspirations & Dreams**: 20.2% of mentions.
-   **Work Experience & Career**: 18.2% of mentions.

**Common Positive Themes:**
-   Brand prestige, unique travel benefits, cultural diversity, and career development opportunities (e.g., training, international exposure).

**Common Concerns (Negative Themes):**
-   Work-life balance (due to demanding schedules), compensation compared to the cost of living in Dubai, management issues, and job security.

**Best Performing Model:**
-   The best text analytics pipeline for sentiment classification utilized a **Logistic Regression (L2) classifier** with **BOW (Bag-of-Words) Count** for feature extraction (after lemmatization). This combination achieved an accuracy of 80.19% and an F1-Score of 76.32% on the test set.

## How to Run the Project

1.  **Dependencies**: Ensure all required libraries are installed by running the first code cell (`!pip install ...`). The Python packages include `google-api-python-client`, `pandas`, `numpy`, `matplotlib`, `seaborn`, `plotly`, `wordcloud`, `nltk`, `textblob`, `vaderSentiment`, `scikit-learn`, `gensim`, `pyLDAvis`, `xgboost`, `imbalanced-learn`, `langdetect`, and `tqdm`.
2.  **NLTK Data**: Download necessary NLTK data by running the `nltk.download()` commands.
3.  **YouTube Data API Key**: Obtain a YouTube Data API v3 key and replace the placeholder `API_KEY` in the notebook with your actual key. **Ensure your API key is kept secure and not directly committed to public repositories.**
4.  **Execute Cells**: Run all cells in the notebook sequentially. The notebook will:
    -   Scrape YouTube comments.
    -   Clean and filter the comments for employee relevance.
    -   Perform sentiment analysis.
    -   Train and evaluate various classification models.
    -   Perform topic modeling with LDA.
    -   Generate visualizations and summarize key insights.

## Generated Files
Upon successful execution, the following files will be generated:
-   `emirates_employee_reviews_youtube.csv`: Raw scraped comments.
-   `emirates_labelled_dataset.csv`: The final curated and sentiment-labeled dataset.
-   `emirates_train.csv`: Training set for sentiment classification.
-   `emirates_test.csv`: Testing set for sentiment classification.
-   `best_model.pkl`: The trained best-performing sentiment classification model.
-   `best_vectorizer.pkl`: The vectorizer used by the best-performing model.
-   `model_comparison_results.csv`: A CSV file detailing the performance of all tested models and feature combinations.
-   `lda_visualization.html`: An interactive HTML file for exploring the LDA topics.
