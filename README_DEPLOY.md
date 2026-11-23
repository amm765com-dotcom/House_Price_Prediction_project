# Lahore House Price Predictor — Vercel deployment

## Included
- `public/index.html`: supplied responsive frontend, configured to call `/api`
- `api/index.py`: Vercel serverless entry point
- `app.py`: supplied FastAPI + scikit-learn model
- `house_prices.db`: supplied SQLite database
- `requirements.txt`, `vercel.json`: deployment configuration

## Deploy
1. Extract this ZIP.
2. Upload all files and folders inside it to a new GitHub repository (the
   `api`, `public`, `app.py`, `house_prices.db`, `requirements.txt`, and
   `vercel.json` must be at repository root).
3. In Vercel, choose **Add New → Project**, import that GitHub repository,
   and click **Deploy**. Keep the Root Directory as `./`.
4. Open the deployed domain. The frontend is `/`; API endpoints are
   `/api/health`, `/api/meta`, `/api/metrics`, and `/api/predict`.

## Local run
Install requirements, then run:
    uvicorn app:app --reload --port 8000
The deployed frontend is configured for Vercel's `/api` routes. For local
testing, change `API_BASE` in `public/index.html` to `http://127.0.0.1:8000`.

## Important model-data note
The supplied SQLite database contains only 2 property rows. The backend's
own training logic therefore supplements these with generated placeholder
rows until at least 50 real rows are available. The website labels this
limitation in the model performance section. Predictions are estimates,
not verified market valuations.

## Serverless storage note
SQLite is bundled as a read-only deployment asset on Vercel. Do not rely on
writing new property records to this database at runtime; use a hosted
database if you later add data-entry functionality.
