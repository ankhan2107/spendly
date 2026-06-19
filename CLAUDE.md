# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run the development server (http://localhost:5001)
python app.py

# Run tests
pytest

# Run a single test file
pytest tests/test_auth.py

# Run a specific test
pytest tests/test_auth.py::test_login
```

## Architecture

**Stack**: Python Flask + SQLite + Jinja2 templates. No build pipeline — CSS and JS are served directly as static files.

**Entry point**: `app.py` — defines all routes and runs on port 5001. Routes are currently stub GET handlers that render templates; POST handlers and business logic are not yet implemented.

**Database**: `database/db.py` is a placeholder. It should expose three functions:
- `get_db()` — SQLite connection factory (row_factory set to `sqlite3.Row`, foreign keys enabled)
- `init_db()` — creates tables via `CREATE TABLE IF NOT EXISTS`
- `seed_db()` — inserts sample data for development

The database file (`expense_tracker.db`) is gitignored. Call `init_db()` on app startup to create it if missing.

**Templates**: Jinja2. `base.html` defines the layout (sticky navbar, footer, Google Fonts). All pages extend it using `{% extends "base.html" %}` with blocks `title`, `head`, `content`, and `scripts`.

## CSS Design System

CSS variables are defined in `static/css/style.css`. Use these instead of hardcoded values:

| Variable | Value | Usage |
|---|---|---|
| `--ink` | `#0f0f0f` | Primary text |
| `--accent` | `#1a472a` | Green (primary actions) |
| `--accent-2` | `#c17f24` | Amber (secondary/highlights) |
| `--danger` | `#c0392b` | Destructive actions |
| `--paper` | `#f7f6f3` | Page background |
| `--paper-warm` | `#f0ede6` | Card/section backgrounds |
| `--border` | `#e4e1da` | Borders and dividers |

Typography: DM Serif Display (headings) + DM Sans (body), loaded from Google Fonts in `base.html`.

## Current Implementation State

- **UI complete**: Landing, login, register, privacy, terms pages are fully styled
- **Routes stub**: All routes render templates; auth and expense CRUD are not functional
- **Database empty**: `db.py` contains only comments describing what to implement
- **No tests yet**: pytest is installed but no test files exist

The app is structured for incremental educational implementation — placeholder routes contain comments like "coming in Step X" that guide the build-out order.
