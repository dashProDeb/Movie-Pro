# Movie Recommendation System: Model Documentation

This document explains the precomputed data files and the recommendation logic used in this project. The system is built on a **Content-Based Filtering** approach using NLP techniques.

## Overview
The recommendation engine uses movie metadata (overviews, genres, and taglines) to find similarities between movies. It converts text descriptions into numerical vectors using TF-IDF (Term Frequency-Inverse Document Frequency) and calculates similarity using Cosine Similarity.

## Data Files (.pkl)

### 1. `df.pkl` (Cleaned Dataframe)
- **Description:** A pickled pandas DataFrame containing the processed movie metadata.
- **Key Columns:**
  - `title`: The official movie title.
  - `tags`: The primary feature used for recommendation. It is a concatenated string of the movie's overview, genres, and tagline.
  - `vote_average`: User ratings (useful for future filtering/weighting).
- **Processing:** This data has been cleaned of duplicates, handled null values, and the `tags` column has undergone NLP preprocessing (lowercasing, punctuation removal, stop-word removal, and lemmatization).

### 2. `tfidf.pkl` (TF-IDF Vectorizer)
- **Description:** The trained `TfidfVectorizer` object from `scikit-learn`.
- **Parameters:**
  - `max_features=5000`: Limits the vocabulary to the top 5,000 most significant words/bigrams.
  - `ngram_range=(1,2)`: Considers both individual words and pairs of words.
- **Use Case:** Used to transform new text into the same vector space as the existing database.

### 3. `tfidf_matrix.pkl` (Vector Matrix)
- **Description:** A Compressed Sparse Row (CSR) matrix containing the TF-IDF vectors for every movie in `df.pkl`.
- **Shape:** `(Number of Movies, 5000)`
- **Role:** This is the "knowledge base" against which similarity comparisons are performed.

### 4. `indices.pkl` (Title Mapping)
- **Description:** A pandas Series mapping movie titles to their integer row index in the `df.pkl` and `tfidf_matrix.pkl`.
- **Role:** Enables $O(1)$ or $O(\log n)$ lookup to find the vector index for a given movie title.

## Recommendation Workflow

1.  **Input:** User provides a movie title (e.g., *"Toy Story"*).
2.  **Index Lookup:** The system uses `indices.pkl` to find the row index (e.g., index `0`).
3.  **Vector Retrieval:** The TF-IDF vector for that index is pulled from `tfidf_matrix.pkl`.
4.  **Similarity Calculation:** The system calculates the **Cosine Similarity** between the input vector and all other vectors in the matrix.
5.  **Sorting:** Movies are sorted by their similarity score in descending order.
6.  **Output:** The titles of the top $N$ most similar movies are returned (excluding the input movie itself).

## Dependencies
To use these files, the following Python libraries are required:
- `pandas`
- `scikit-learn`
- `pickle`
