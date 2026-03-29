# Movie Recommender

Public Streamlit app for discovering movies with TMDb and saving personalized ratings in Postgres.

## Features

- Filter recommendations by genre, extra genres, actor, US content rating, streaming service, release year, and language
- Search directly by movie title
- Create user accounts with a username and PIN
- Save, update, and delete movies in a Postgres database
- Personalize recommendation order from a user's saved ratings
- Show a normalized many-to-many schema with `app_users`, `movies`, and `user_movies`

## Tech Stack

- Streamlit
- TMDb API
- PostgreSQL
- `psycopg`

## Database Design

This app uses three main tables:

- `app_users`: one row per user
- `movies`: one row per movie
- `user_movies`: junction table linking users to movies, with user-specific rating and notes

That means the app models a many-to-many relationship:

- one user can save many movies
- one movie can be saved by many users

## Run Locally

```bash
cd /Users/mattbiddle/Documents/Playground/movie_recommender
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
export TMDB_API_KEY='your_tmdb_api_key'
export DATABASE_URL='your_postgres_connection_string'
python -m streamlit run app.py
```

Then open the local URL Streamlit prints, usually `http://localhost:8501`.

## Deploy On Streamlit Community Cloud

1. Push this repo to GitHub.
2. In Streamlit Community Cloud, create a new app from the repo.
3. Set the main file path to `movie_recommender/app.py`.
4. Add these secrets:

```toml
TMDB_API_KEY="your_tmdb_api_key"
DATABASE_URL="your_postgres_connection_string"
```

## Important Notes

- Do not commit API keys or database credentials to GitHub.
- The app reads secrets from Streamlit Cloud or local environment variables.
- The `View Database Tables` section in the app can be used to show the three-table many-to-many structure for class screenshots.
