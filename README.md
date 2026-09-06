# 🎬 Movie Recommendation System

> An end-to-end movie recommendation platform built with **Python, FastAPI, Streamlit, TF-IDF, Scikit-learn, and TMDB API**. Search for movies, explore details, and receive personalized recommendations based on content similarity and movie genres.

[![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-Backend-009688?logo=fastapi)](https://fastapi.tiangolo.com/)
[![Streamlit](https://img.shields.io/badge/Streamlit-Frontend-FF4B4B?logo=streamlit)](https://streamlit.io/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-F7931E?logo=scikit-learn)](https://scikit-learn.org/)
[![TMDB](https://img.shields.io/badge/TMDB-API-01B4E4?logo=themoviedatabase)](https://www.themoviedb.org/)

---

## 🌟 Overview

**Movie Recommendation System** is a full-stack machine-learning application that helps users discover movies based on their interests.

The application combines:

* 🔎 Movie search
* 🎯 Content-based recommendations
* 🧠 TF-IDF similarity
* 🎭 Genre-based recommendations
* 🎬 TMDB movie metadata
* 🖼️ Movie posters and backdrops
* ⚡ FastAPI REST backend
* 🖥️ Streamlit interactive frontend

The recommendation engine uses a pre-trained **TF-IDF matrix** and cosine-similarity-style vector multiplication to identify movies that are most similar to the selected movie.

---

## ✨ Features

### 🔍 Movie Search

Search for movies using the TMDB database and browse multiple matching results.

### 🎯 Content-Based Recommendation

The system recommends movies similar to the selected movie using a locally stored TF-IDF representation.

The recommendation process:

```text
Selected Movie
      ↓
Find Movie in Dataset
      ↓
Retrieve TF-IDF Vector
      ↓
Calculate Similarity
      ↓
Rank Similar Movies
      ↓
Return Top Recommendations
```

### 🎭 Genre-Based Recommendations

The application also retrieves the movie's first genre and uses TMDB's discovery functionality to find popular movies from that genre.

### 🎬 TMDB Integration

TMDB is used for:

* Movie search
* Movie details
* Release dates
* Genres
* Ratings
* Posters
* Backdrop images

The backend reads the TMDB API key from the environment using `TMDB_API_KEY`.

### 🖥️ Interactive Streamlit UI

The frontend provides a modern movie browsing interface with:

* Home feed
* Search
* Movie cards
* Posters
* Movie details
* Recommendation sections

The Streamlit application communicates with the FastAPI backend through HTTP requests.

### 🚀 Production-Oriented Architecture

The project separates the application into:

```text
Streamlit Frontend
        │
        ▼
   FastAPI Backend
        │
   ┌────┴─────┐
   ▼          ▼
TF-IDF      TMDB API
Model
```

---

# 🧠 Recommendation Approach

## TF-IDF

The project uses **TF-IDF (Term Frequency-Inverse Document Frequency)** to represent movie information as numerical vectors.

The stored machine-learning resources include:

```text
df.pkl
indices.pkl
tfidf.pkl
tfidf_matrix.pkl
```

The FastAPI backend loads these files when the application starts.

### Recommendation Process

For a selected movie:

1. Normalize the movie title.
2. Find the movie's index.
3. Retrieve its TF-IDF vector.
4. Compare it against the TF-IDF matrix.
5. Calculate similarity scores.
6. Sort movies by similarity.
7. Return the highest-ranked movies.

The implementation calculates similarity through the TF-IDF matrix and ranks the resulting scores in descending order.

---

# 🏗️ Project Architecture

```text
                 ┌─────────────────────┐
                 │      User           │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Streamlit Frontend  │
                 │       app.py        │
                 └──────────┬──────────┘
                            │ HTTP
                            ▼
                 ┌─────────────────────┐
                 │   FastAPI Backend   │
                 │       main.py       │
                 └──────┬────────┬─────┘
                        │        │
             ┌──────────┘        └───────────┐
             ▼                               ▼
     ┌───────────────┐                ┌──────────────┐
     │ TF-IDF Model  │                │   TMDB API   │
     │   .pkl files  │                │ Movie Data   │
     └───────────────┘                └──────────────┘
```

---

# 📁 Project Structure

```text
Movie-Recommendation/
│
├── app.py                  # Streamlit frontend
├── main.py                 # FastAPI backend
│
├── movies.ipynb            # Movie data analysis/model development
│
├── df.pkl                  # Processed movie DataFrame
├── indices.pkl             # Movie title → index mapping
├── tfidf.pkl               # TF-IDF vectorizer
├── tfidf_matrix.pkl        # Pre-computed TF-IDF matrix
│
├── requirements.txt        # Python dependencies
├── runtime.txt             # Python runtime version
│
└── README.md
```

The repository currently contains the frontend, backend, notebook, model artifacts, dependency file, and Python runtime configuration shown above.

---

# 🛠️ Tech Stack

| Technology    | Purpose                     |
| ------------- | --------------------------- |
| Python        | Core programming language   |
| FastAPI       | Backend REST API            |
| Streamlit     | Interactive frontend        |
| Pandas        | Data processing             |
| NumPy         | Numerical computation       |
| Scikit-learn  | TF-IDF and machine learning |
| SciPy         | Sparse matrix operations    |
| HTTPX         | Async API requests          |
| python-dotenv | Environment variables       |
| TMDB API      | Movie metadata and posters  |

The repository currently pins these main dependencies, including FastAPI, Uvicorn, Pandas, NumPy, SciPy, Scikit-learn, Streamlit, HTTPX, and python-dotenv.

---

# ⚙️ Installation

## 1. Clone the Repository

```bash
git clone https://github.com/sarhan-003/Movie-Recommendation.git
cd Movie-Recommendation
```

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# 🔑 Environment Configuration

Create a `.env` file in the project root:

```env
TMDB_API_KEY=your_tmdb_api_key
```

The FastAPI backend expects `TMDB_API_KEY` and raises an error during startup if the variable is missing.

You can obtain a TMDB API key from:

https://www.themoviedb.org/

**Important:** Never commit your `.env` file or expose your API key publicly.

Add this to `.gitignore`:

```gitignore
.env
venv/
__pycache__/
```

---

# ▶️ Running the Application

The project contains two components:

* FastAPI backend
* Streamlit frontend

## Start FastAPI Backend

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

The API will be available at:

```text
http://localhost:8000
```

Interactive API documentation:

```text
http://localhost:8000/docs
```

The FastAPI application exposes `/docs` through its root metadata.

---

## Start Streamlit Frontend

Open another terminal:

```bash
streamlit run app.py
```

The Streamlit application will normally be available at:

```text
http://localhost:8501
```

---

# 🔗 API Endpoints

## Health Check

```http
GET /health
```

Example response:

```json
{
  "status": "ok"
}
```

---

## Home Feed

```http
GET /home
```

Supported categories include:

```text
trending
popular
top_rated
upcoming
now_playing
```

Example:

```text
/home?category=popular&limit=24
```

---

## Search Movies

```http
GET /tmdb/search
```

Example:

```text
/tmdb/search?query=Inception
```

This endpoint returns multiple TMDB search results.

---

## Movie Details

```http
GET /movie/id/{tmdb_id}
```

Example:

```text
/movie/id/27205
```

Returns information such as:

* Movie title
* Overview
* Release date
* Poster
* Backdrop
* Genres

---

## Genre Recommendations

```http
GET /recommend/genre
```

Example:

```text
/recommend/genre?tmdb_id=27205&limit=18
```

The endpoint determines the movie's first genre and retrieves popular movies from that genre.

---

## TF-IDF Recommendations

```http
GET /recommend/tfidf
```

Example:

```text
/recommend/tfidf?title=Inception&top_n=10
```

Returns similar movies with similarity scores.

Example:

```json
[
  {
    "title": "Movie A",
    "score": 0.82
  },
  {
    "title": "Movie B",
    "score": 0.76
  }
]
```

---

## Combined Movie Search

```http
GET /movie/search
```

Example:

```text
/movie/search?query=Inception
```

This endpoint combines:

* Movie details
* TF-IDF recommendations
* Genre recommendations
* TMDB posters

The backend explicitly provides this as a bundled response for the frontend.

---

# 🔄 Application Workflow

```text
                USER
                  │
                  ▼
        Search for a movie
                  │
                  ▼
          Streamlit Frontend
                  │
                  ▼
           FastAPI Backend
                  │
          ┌───────┴────────┐
          │                │
          ▼                ▼
       TMDB API       Local TF-IDF
          │                │
          ▼                ▼
  Movie Information    Similarity
          │                │
          └───────┬────────┘
                  ▼
          Recommendation
                  │
                  ▼
          Streamlit UI
                  │
                  ▼
        🎬 Movie Results
```

---

# 📊 Machine Learning Pipeline

```text
Movie Dataset
      │
      ▼
Data Cleaning
      │
      ▼
Text Feature Preparation
      │
      ▼
TF-IDF Vectorization
      │
      ▼
TF-IDF Matrix
      │
      ▼
Similarity Calculation
      │
      ▼
Movie Ranking
      │
      ▼
Top-N Recommendations
```

The trained artifacts are stored locally so the application can perform recommendations without retraining the model every time the server starts.

---

# ☁️ Deployment

The project can be deployed as two services:

### Backend

Deploy the FastAPI application on a platform such as:

* Render
* Railway
* Fly.io
* VPS
* Docker-based hosting

Start command:

```bash
uvicorn main:app --host 0.0.0.0 --port $PORT
```

### Frontend

The Streamlit frontend can be deployed separately.

Set the backend URL through:

```env
API_BASE=https://your-backend-url.onrender.com
```

The Streamlit application reads `API_BASE` from the environment and otherwise uses its configured backend URL.

---

# 🐍 Python Version

The repository specifies:

```text
Python 3.11.9
```

in `runtime.txt`.

Using the same Python version for local development and deployment is recommended.

---

# ⚠️ Deployment Notes

The recommendation model files are part of the application:

```text
df.pkl
indices.pkl
tfidf.pkl
tfidf_matrix.pkl
```

Make sure these files are available to the backend during deployment.

Because the backend loads these resources during application startup, missing or incompatible model files can prevent the API from starting.

For large model artifacts, consider:

* Git LFS
* Object storage
* Cloud storage
* Downloading models during deployment

---

# 🧪 Testing the API

After starting FastAPI:

```bash
curl http://localhost:8000/health
```

Expected:

```json
{
  "status": "ok"
}
```

Test TF-IDF:

```bash
curl "http://localhost:8000/recommend/tfidf?title=Inception&top_n=5"
```

Test TMDB search:

```bash
curl "http://localhost:8000/tmdb/search?query=Inception"
```

---

# 🚀 Future Improvements

Potential improvements include:

* [ ] Hybrid recommendation system
* [ ] Collaborative filtering
* [ ] User accounts and profiles
* [ ] Personalized watch history
* [ ] Like/dislike feedback
* [ ] Recommendation explanations
* [ ] Better cold-start handling
* [ ] Advanced ranking model
* [ ] Movie ratings prediction
* [ ] Redis caching
* [ ] Database integration
* [ ] Docker support
* [ ] CI/CD pipeline
* [ ] Automated testing
* [ ] Improved recommendation evaluation
* [ ] Mobile-friendly interface

---

# 📈 Possible Advanced Recommendation Architecture

A future version could combine multiple recommendation signals:

```text
                  User
                   │
          ┌────────┴────────┐
          ▼                 ▼
   Content Similarity   User Behavior
          │                 │
          ▼                 ▼
       TF-IDF        Collaborative
                       Filtering
          │                 │
          └────────┬────────┘
                   ▼
             Hybrid Ranking
                   │
                   ▼
          Personalized Movies
```

This would make the system more personalized than relying only on content similarity.

---

# 🤝 Contributing

Contributions are welcome!

### 1. Fork the repository

```bash
git fork
```

### 2. Clone your fork

```bash
git clone https://github.com/YOUR_USERNAME/Movie-Recommendation.git
```

### 3. Create a branch

```bash
git checkout -b feature/new-feature
```

### 4. Make your changes

### 5. Commit

```bash
git add .
git commit -m "Add new recommendation feature"
```

### 6. Push

```bash
git push origin feature/new-feature
```

### 7. Open a Pull Request

---

# 📜 License

This project is available for educational and development purposes.

If you add a specific open-source license to the repository, update this section accordingly.

---

# 👨‍💻 Author

**Sarhan Bakarman**

GitHub:
https://github.com/sarhan-003

Project:
https://github.com/sarhan-003/Movie-Recommendation

---

# ⭐ Support

If you find this project useful:

⭐ Star the repository
🍴 Fork the project
🐛 Report issues
💡 Suggest improvements
🤝 Contribute to the project

---

## 🎬 Built With

**Python • FastAPI • Streamlit • Scikit-learn • Pandas • NumPy • SciPy • TF-IDF • TMDB API**

> Turning movie data into personalized recommendations. 🍿🎬
