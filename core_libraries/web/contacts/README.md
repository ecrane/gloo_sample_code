# Contacts

A small CRM web app, built on `gloo-web` with a SQLite database. 
This is a sample app to demonstrate the use of gloo-web.


## What it does

- **People** — a searchable list, a detail page, add / edit / delete.
  A person has a name, an optional birthday, a "pinned" flag, and a
  freeform bio (markdown).
- **Notes** — each note belongs to one person. You add notes from the
  person's page; there is also a cross-person note search and a
  single-note view with edit / delete.
- **Dashboard** (`/`) — counts, the next few birthdays, recent notes.
- **Birthdays** (`/people/bdays`) — everyone with a birthday on file,
  ordered by how soon it is (computed in SQL with `strftime`).

## Run it

Build the database first — this creates `data/contacts.db`, the
tables, and some sample data:

```bash
gloo core_libraries/web/contacts/db/scaffold.gloo
```

(run from the repo root; safe to run again to reset to a clean state).

Then start the app:

```bash
gloo --app <full path to>/core_libraries/web/contacts
```

It serves `http://localhost:8095/` and opens a browser. Enter `q` at
the prompt to stop it.

Requires `gloo-sqlite` >= 1.5 (for `[tbl]` objects backed by a SQLite
query).

## Layout

```
start.gloo            entry point: load libraries + folders, start the server
db/scaffold.gloo      build data/contacts.db (schema + sample data)
data/db.gloo          the shared sqlite connection
app/                  the web server object, form/table styles, startup banner
layout/ shared/       the page layout, nav, footer
helper/               small [ƒ] helpers used from page templates (link, title, markdown, …)
page/                 one file per route; the router maps folders + names to URLs
  home.gloo             /
  people/                /people/…
  notes/                 /notes/…
```

## Routing notes

The router turns the `page/` tree into routes: `page/people/index.gloo`
serves `/people/`, a numeric URL segment becomes an `id` parameter,
and the HTTP method selects the page object (`GET` → `index` / `show`,
`POST` → `create`). This app has no client-side JavaScript, so edits
and deletes post to explicit `…/update` and `…/delete` routes rather
than using `PATCH` / `DELETE`.
