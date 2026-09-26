# Programming notes (Joplin mirror)

This directory is a local, version-controlled copy of the **Private / Programming** notebook from [Joplin](https://joplinapp.org/). The same content lives in two places:

- **Joplin**, for reading, searching and syncing across devices,
- **this Git repository**, for editing in a code editor, reviewing diffs, checking links and keeping history.

The two are kept in sync with [`joplin-sync`](https://github.com/pzborow/joplin-sync), a small CLI that maps a Joplin notebook tree to a directory of Markdown files.

## How the mapping works

| Joplin | This directory |
|---|---|
| notebook | directory |
| sub-notebook | subdirectory |
| note | `.md` file named after the note title |
| link to another note (`:/note_id`) | relative Markdown link |

`.joplin-sync.json` stores which Joplin notebook this directory is bound to and when it was last pulled. Do not edit or delete it.

## What is inside

Most notes are written in Polish, some in English. Top-level notebooks:

| Directory | Contents |
|---|---|
| `Software engineering/` | how to design and change systems, beyond a single language: `Architecture/` (layered, hexagonal, onion, clean, DDD, CQRS), `Microservices/`, `Legacy/` (working with legacy code), `Security/` (application security for developers, with Django and DRF), `Design patterns/` (GoF in Python), `Principles/` (OOP, SOLID, DRY, KISS, YAGNI) |
| `Databases/` | `RDBMS/` (SQL), `NoSQL/MongoDB/`, `Graph/ArangoDB/`, `Graph/RDF Jena Fuseki/`, `Search/Elasticsearch/` |
| `Cloud/` | `AWS/` (S3, RDS, EC2, Lambda, CloudWatch, containers, CI/CD), `Google/` |
| `Python/`, `Django/` | short how-tos and snippets: testing, logging, packaging, DRF, ORM queries |
| `Frontend/`, `Javascript/` | JavaScript, ES6, React, Bootstrap notes |
| `XML/` | data-format notes |
| `Docker and compose/`, `Git/`, `Command line CLI/`, `System trics/`, `VSCode/` | tooling and day-to-day tricks |
| `Test uml/` | PlantUML experiments |
| loose `.md` files at the root | single notes that are not in any sub-notebook |

Most long tutorials have numbered chapters and a glossary. The ones under `Software engineering/Architecture/`, `Software engineering/Legacy/` and `Software engineering/Security/` also link each term's first mention to the glossary and end every chapter with a "Co zapamiętać" summary and interview questions with hidden answers. `Design patterns/` and `Principles/` were converted from Jupyter notebooks, so each code block is followed by its output.

## Workflow

The safe cycle is always **pull → edit → publish**:

```bash
cd jopplin

# 1. get the current state from Joplin (overwrites local files)
joplin-sync pull --force

# 2. edit Markdown files locally, review the diff
git diff

# 3. push local changes back to Joplin
joplin-sync publish

# 4. record the change in Git
git add .
git commit -m "notes: ..."
```

Without `--path`, both commands use the notebook stored in `.joplin-sync.json`.

## Things to keep in mind

- **Local files are the source of truth during `publish`.** Notes missing in Joplin are created, existing ones are updated, and notes deleted locally are deleted in Joplin.
- **There is no conflict detection.** If a note was edited in Joplin and locally, the last operation wins. Pull before you start editing.
- **`pull --force` replaces the whole local directory.** Commit or stash local work first; Git is the safety net here.
- **File names are note titles.** Renaming a file renames the note in Joplin. Keep names readable; spaces and Polish characters are fine.
- **This README is also a note.** After `publish` it appears in Joplin at the root of the Programming notebook.
- **Never commit the Joplin token.** It belongs in `~/.config/joplin-sync/config` or in the `JOPLIN_TOKEN` environment variable.

## Setup on a new machine

```bash
pipx install 'git+ssh://git@github.com/pzborow/joplin-sync.git'

# ~/.config/joplin-sync/config
# JOPLIN_TOKEN=<token from Joplin: Tools > Options > Web Clipper>
# JOPLIN_URL=http://127.0.0.1:41184
```

Joplin must be running with the Web Clipper service enabled. If Joplin runs on another computer, forward its port over SSH:

```bash
ssh -N -R 41184:127.0.0.1:41184 user@machine-running-joplin-sync
```

Check the connection with `joplin-sync list programming`.
