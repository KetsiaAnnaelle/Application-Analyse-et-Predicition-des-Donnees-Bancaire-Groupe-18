# Banque Analytics Backend (Flask + SQLite + SQLModel)

Small Flask API that serves analytics over the provided `database.db` using the models in `tables__projet.py`. Two endpoints are exposed:
- `/api/transactions/monthly` — monthly income/expense/net totals for charts
- `/api/transactions/category-averages` — average amount per category

## Quick start
1) Install dependencies (inside the project folder):
```
python -m venv .venv
.venv\Scripts\activate
pip install flask sqlmodel
```

2) Make sure the database file exists (provided) and tables are created:
```
python tables__projet.py
```
This seeds sample data only if you run the file directly. Importing it does not reseed.

3) Run the API:
```
flask --app app run --debug
```
or:
```
python app.py
```

## Endpoints
### `/api/transactions/monthly`
- Returns monthly aggregates with fields: `year`, `month`, `income`, `expense` (absolute value of negative amounts), `net`, `label`.
- Optional query params:
  - `start`: `YYYY-MM-DD`
  - `end`: `YYYY-MM-DD`
  - `client_id`: filter by a specific client

### `/api/transactions/category-averages`
- Returns the average transaction amount per category.
- Same optional query params as above: `start`, `end`, `client_id`.

### `/health`
- Simple health check.

## Notes
- Models and engine are defined in `tables__projet.py`; the API reuses that engine.
- If you change column names or add fields, adjust the queries in `app.py`.
- The sample data in `tables__projet.py` includes both positive and negative amounts. The API treats positive amounts as income and negative amounts as expense for the monthly comparison.


