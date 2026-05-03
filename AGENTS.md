# AGENTS.md

This file provides guidance for coding agents working in this repository.

## Project Overview

- **Project**: `studion`
- **Type**: Python `nicegui` fullstack application
- **Purpose**: Support a researching nurse in a hospital to manage incoming pharma-related research projects
- **Current runtime target**: Standalone local mode
- **Current database target**: SQLite
- **Possible future targets**:
  - Tauri desktop packaging/support
  - Distributed deployment
  - Postgres as a production/distributed database option

## Current Technical Context

- Main UI/app module currently lives in `studion.py`.
- `nicegui` is the current framework dependency (see `pyproject.toml`).
- The project is in an early stage; architecture and domain model are expected to evolve.

## Development Guidance

When making changes, prioritize:

1. **Clinical workflow clarity**
   - Keep the UI straightforward for hospital users.
   - Minimize clicks and cognitive load for repetitive research intake tasks.

2. **Data integrity**
   - Preserve correctness of project metadata (sponsor, protocol, status, timelines, contacts).
   - Favor explicit validation over implicit assumptions.

3. **Local-first reliability**
   - Ensure features work in standalone local mode without external services.
   - Keep SQLite compatibility as the baseline.

4. **Future portability**
   - Avoid SQLite-specific patterns that block migration to Postgres.
   - Keep persistence boundaries clear to ease future distributed support.

5. **Security and privacy mindset**
   - Treat all hospital and study data as sensitive.
   - Avoid logging sensitive details unless explicitly necessary and sanitized.

## Suggested Conventions for Agents

- Prefer small, incremental changes with clear reasoning.
- Keep business/domain logic separate from UI rendering when practical.
- If introducing storage layers, isolate DB access behind well-defined interfaces.
- Update `README.md` when behavior, setup, or scope changes materially.
- Add or update tests for non-trivial logic.

## Out of Scope (for now)

- Premature optimization for distributed scale.
- Hard-coding assumptions that prevent future Tauri/Postgres adoption.
