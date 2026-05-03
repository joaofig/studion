# studion
Personal pharma research study tracker

## Database

- The app initializes a local SQLite database at startup.
- Database path is configured via `studion.toml`:

```toml
[database]
path = "studion.db"
```

- By default, the database file is `studion.db` in the project root.
- Initial schema includes a `location` table with sequential identifier `id` and `name` field.
