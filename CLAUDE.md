# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

`studion` is a Python NiceGUI fullstack application for a hospital nurse to manage incoming pharma research projects. It runs standalone locally with SQLite, with future portability to Tauri desktop and Postgres in mind.

## Commands

```bash
# Run the app
uv run studion.py

# Add a dependency
uv add <package>
```

There are no tests yet. When adding non-trivial logic, add tests alongside it.

## Architecture

**Entry point**: `studion.py` — initializes the DB, defines the `/` route, and calls `ui.run()`.

**`db/`** — persistence layer:
- `config.py`: Reads `studion.toml` for the database path; falls back to `studion.db` in the project root.
- `sqlite.py`: `get_connection()` returns a `sqlite3.Connection`; `initialize_database()` creates the schema (`location`, `researcher`, `study` tables) on startup.
- `__init__.py`: Re-exports the public API.

**`views/`** — NiceGUI UI components:
- `main.py`: Top-level layout — vertical splitter with tab navigation (Studies, Researchers, Locations, Reports, Settings).
- `study.py`: Study tab content — table view with an "Add Study" button.

**Configuration**: `studion.toml` controls the database path. Relative paths resolve from the project root.

## Key Conventions

- Keep business/domain logic separate from UI rendering.
- Isolate all DB access through `db/` — do not call `sqlite3` directly from views.
- Avoid SQLite-specific SQL patterns that would block a future Postgres migration (e.g., no `AUTOINCREMENT`, no SQLite-only pragmas in schema queries).
- Treat all study and hospital data as sensitive; avoid logging it.
- Update `README.md` when behavior, setup, or scope changes materially.
