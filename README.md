# 🎬 Movie Recommender Pro

A full-stack Movie Recommender application built with **FastAPI** and **Streamlit**. It combines local Machine Learning (TF-IDF Content-Based Filtering) with real-time data from **The Movie Database (TMDB)**.

---

## 📸 Overview
The Movie Recommender Pro allows users to discover movies, view detailed information, and get personalized recommendations. The system uses a hybrid approach:
- **TF-IDF Similarity**: Analyzes movie metadata to find similar films in a local dataset.
- **TMDB Integration**: Fetches real-time posters, backdrops, and trending movie lists.

---

## 🛠️ Project Structure & Components

### 1. **Backend (`project-ai/main.py`)** - FastAPI
The engine of the application. It handles:
- **ML Inference**: Performs cosine similarity calculations using precomputed TF-IDF matrices.
- **API Orchestration**: Combines local model results with dynamic data from TMDB.
- **Endpoints**:
    - `/home`: Fetches trending/popular movies from TMDB.
    - `/movie/search`: The "Bundle" endpoint that returns movie details + TF-IDF recommendations + Genre recommendations.
    - `/tmdb/search`: Handles autocomplete search suggestions.

### 2. **Frontend (`project-ai/app.py`)** - Streamlit
A modern web interface featuring:
- **Responsive Grid**: Interactive movie posters with "Open" functionality.
- **Navigation**: Deep-linking support (you can share URLs for specific movies).
- **Caching**: Optimized performance to ensure a smooth user experience.

### 3. **Machine Learning Model**
Located in `project-ai/`, these serialized files power the recommendation engine:
- `tfidf_matrix.pkl`: The numerical representation of our movie database.
- `tfidf.pkl`: The vectorizer used to process movie descriptions.
- `df.pkl`: The metadata dataframe.
- `indices.pkl`: A fast mapping of movie titles to their matrix positions.

---

## 🚀 Getting Started (Setup Guide)

### 📋 Prerequisites
1. **Python 3.8+**
2. **TMDB API Key**: 
    - Create an account at [themoviedb.org](https://www.themoviedb.org/).
    - Generate an API Key (v3) in your settings.

### 🔧 Installation
```bash
# Clone the repo
git clone https://github.com/dashProDeb/Movie-Pro.git
cd Movie-Pro/project-ai

# Create & activate virtual environment
python -m venv .venv
# Windows: .\.venv\Scripts\activate
# Mac/Linux: source .venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 🔑 Configuration
Create a `.env` file in the `project-ai/` directory:
```env
TMDB_API_KEY=your_api_key_here
```

### 🏃 Running the Project
1. **Start Backend**: `uvicorn main:app --reload`
2. **Start Frontend**: `streamlit run app.py`

---

## 🏗️ Architecture
The project follows a decoupled architecture, allowing the frontend and backend to scale independently.

- **Frontend**: Streamlit (Python)
- **Backend**: FastAPI (Asynchronous Python)
- **ML**: Scikit-learn, Pandas, NumPy
- **External API**: TMDB API (via `httpx`)

---

## 📂 Directory Layout
```text
Movie-Pro/
├── project-ai/           # Main application code
│   ├── app.py            # Streamlit Frontend
│   ├── main.py           # FastAPI Backend
│   ├── .env              # Environment secrets (ignored by git)
│   ├── *.pkl             # ML Model files (Large files)
│   └── requirements.txt  # Dependencies
├── data-clean/           # Notebooks and raw data processing
└── README.md             # You are here!
```

---

## 📝 License
This project is for educational purposes. Movie data and images are provided by [TMDB](https://www.themoviedb.org/).
