# SplitIt

SplitIt is a tiny Splitwise-style app for flatmates and trips: a group has members, members pay for things, and the app works out who owes whom. It is also your starter repo for this course — you will read it, ask an AI about it, fix its bugs and build its missing features.

## Run it

```
git clone <this repo>
cd splitit
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
streamlit run app.py
```

Your browser opens on the groups list. Click **Open** on a group, add an expense, then look at `data/expenses.csv` in VS Code: a new line appeared. That folder *is* the database.

## Reset the data

Broke something? Deleted the wrong member? Run

```
python seed.py
```

It copies the pristine CSVs from `seed/` over `data/` and tells you what it restored.

## Run the tests

```
pytest
```

Some tests fail on purpose. They describe features not built yet and bugs not fixed yet. That's your job.

## What is where

```
app.py              the Streamlit screens (this is what "streamlit run app.py" starts)
db.py               reads and writes the CSV files: load_table, save_table, append_row, next_id
logic.py            the rules: members, expenses, shares, balances, settle up (unfinished)
seed.py             python seed.py -> puts data/ back to how it was on day one
data/               the live database: groups.csv, members.csv, expenses.csv
seed/               pristine copies of those three files
tests/conftest.py       test helpers: every test gets its own throwaway copy of the data
tests/test_smoke.py     always green: the app renders, the tables load, seed works
tests/test_bugs.py      red on purpose: what the app SHOULD do once bugs 000-003 are fixed
tests/test_feature_*.py red on purpose: what the app SHOULD do once features 1-3 are built
specs/              one spec per feature, written by the product manager
issues/             one bug report per planted bug, written by users
ONBOARDING.md       the week-1 question sheet: answer it in this file
requirements.txt    the two libraries we use, with their versions
```

Good to know: everything that comes out of a CSV file is text. Ids are `"3"`, not `3`; amounts are `"30.00"`, not `30.0`. Convert with `int()` or `float()` when you need numbers.
