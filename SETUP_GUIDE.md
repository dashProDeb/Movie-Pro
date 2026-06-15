# 🎬 Movie Recommender Setup Guide

This guide will help you set up and run the Movie Recommender project on any machine. The project consists of a **FastAPI** backend and a **Streamlit** frontend.

---

## 📋 Prerequisites

Before you begin, ensure you have the following:

1.  **Python 3.8+**: Installed on your machine.
2.  **TMDB API Key**: 
    *   This project uses [The Movie Database (TMDB) API](https://www.themoviedb.org/documentation/api) to fetch movie posters, backdrops, and details.
    *   **How to get one:** 
        1.  Create an account on [themoviedb.org](https://www.themoviedb.org/).
        2.  Go to your account settings -> **API**.
        3.  Apply for an API Key (choose 'Developer').
        4.  Copy your **API Read Access Token** or **API Key (v3 auth)**.
3.  **Large Data Files**: Ensure the following `.pkl` files are in the `project-ai/` directory (these are generated from the movie dataset):
    *   `df.pkl`
    *   `indices.pkl`
    *   `tfidf_matrix.pkl`
    *   `tfidf.pkl`

---

## 🚀 Step-by-Step Installation

### 1. Clone the Repository
```bash
git clone https://github.com/dashProDeb/Movie-Pro.git
cd Movie-Pro/project-ai
```

### 2. Create a Virtual Environment
It is highly recommended to use a virtual environment to avoid dependency conflicts.

**Windows:**
```powershell
python -m venv .venv
.\.venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables
Create a file named `.env` in the `project-ai/` directory and add your TMDB API Key:

```env
TMDB_API_KEY=your_api_key_here
```

---

## 🏃 Running the Application

You need to run **two separate processes**: the Backend (FastAPI) and the Frontend (Streamlit).

### Step A: Start the Backend (API)
Open a terminal/command prompt in the `project-ai/` directory and run:
```bash
uvicorn main:app --reload
```
*The API will start at `http://127.0.0.1:8000`.*

### Step B: Start the Frontend (UI)
Open a **new** terminal/command prompt in the `project-ai/` directory, activate the virtual environment, and run:
```bash
streamlit run app.py
```
*The UI will open in your browser (usually at `http://localhost:8501`).*

---

## 🛠️ Troubleshooting

*   **Missing API Key**: If posters aren't loading, check your `.env` file and ensure the key is correct.
*   **Pickle Errors**: If the backend fails to start, ensure `df.pkl`, `indices.pkl`, and the other pickle files are present in the same directory as `main.py`.
*   **Port Conflicts**: If port 8000 or 8501 is already in use, you can specify different ports:
    *   Backend: `uvicorn main:app --port 8001`
    *   Frontend: `streamlit run app.py --server.port 8502` (Note: If you change the backend port, you may need to update the `API_BASE` in `app.py` or set it via environment variable).

---

## 📂 Project Structure
*   `main.py`: The FastAPI backend handling the recommendation logic and TMDB integration.
*   `app.py`: The Streamlit frontend providing the user interface.
*   `requirements.txt`: List of Python libraries needed.
*   `.env`: (You create this) Stores your private API keys.
