# Movie Recommender Project Overview

This project is a Movie Recommender system consisting of a FastAPI backend and a Streamlit frontend.

## Architecture

- **Backend (`main.py`)**: FastAPI application that serves movie recommendations using a TF-IDF model.
- **Frontend (`app.py`)**: Streamlit application providing a user interface for searching and viewing movie recommendations.
- **Data/Models**:
  - `df.pkl`: Dataframe containing movie metadata.
  - `indices.pkl`: Mapping of movie titles to indices.
  - `tfidf_matrix.pkl`: Precomputed TF-IDF matrix for similarity calculations.
  - `tfidf.pkl`: TF-IDF vectorizer object.

## Current Status & Observations

1. **Path Issues (Fixed)**: `main.py` has been updated to use paths relative to the script location, ensuring portability across different environments.
2. **API Configuration (Fixed)**: `app.py` has been updated to use `os.getenv("API_BASE", "...")` for flexible configuration and to fix a logic bug.
3. **Environment (Action Required)**: The existing `.venv` directory appears to be broken as it points to absolute paths from a different system. A fresh virtual environment should be created.

## Recommended Setup

To run this project, it is recommended to create a new virtual environment:

```powershell
# 1. Remove the old environment (optional)
# rm -r .venv

# 2. Create a new environment
python -m venv .venv

# 3. Activate and install requirements
.\.venv\Scripts\activate
pip install -r requirements.txt
```

## Running the Project

1. **Backend**: `uvicorn main:app --reload`
2. **Frontend**: `streamlit run app.py`
