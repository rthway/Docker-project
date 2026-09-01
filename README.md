# Docker Compose exercises

A set of small, self-contained Docker Compose stacks written while learning
containerisation. They are kept here because they still work and are useful as
references — not as portfolio pieces. For production-shaped work see
[**devops-production-demo**](https://github.com/rthway/devops-production-demo).

## What is here

| Stack | Demonstrates |
|---|---|
| [`Build Local Django Application in a Container`](./Build%20Local%20Django%20Application%20in%20a%20Container) | Dockerfile + Compose for a Django REST app |
| [`Nextcloud Docker compose`](./Nextcloud%20Docker%20compose) | Nextcloud + MariaDB with a healthcheck-gated dependency |
| [`Prometheus and Grafana Docker Compose`](./Prometheus%20and%20Grafana%20Docker%20Compose) | Metrics collection and dashboards |
| [`wordpress with mysql- Fresh`](./wordpress%20with%20mysql-%20Fresh) | WordPress + MySQL with persistent volumes |

## Running any of them

```bash
cp .env.example .env     # then set real values
cd "Nextcloud Docker compose"
docker compose --env-file ../.env up -d
docker compose ps
```

Every stack refuses to start if a required password is unset, rather than
falling back to a default:

```
required variable NEXTCLOUD_DB_PASSWORD is missing a value: set NEXTCLOUD_DB_PASSWORD in .env
```

## Repository history

This repository previously committed an entire Python virtual environment —
**6,807 of 6,848 tracked files** were `env/lib/python3.10/site-packages/...`,
along with `__pycache__` directories and a local SQLite database. The actual
source was 26 files.

That has been purged from the full history with `git-filter-repo`, and
`.gitignore` now makes it impossible to reintroduce.

| | Before | After |
|---|---:|---:|
| Tracked files | 6,848 | 26 |
| `.git` size | 16 MB | 108 KB |

All three original commits are preserved; only the vendored dependencies were
removed. **Commit hashes changed** as a result of the rewrite — if you have an
old clone, re-clone rather than pull.

## Credentials

Passwords were previously hardcoded in the Compose files. They were only ever
local defaults (`wordpress`/`wordpress`, `nextcloud`/`nextcloud`) and Django's
own `django-insecure-` development key, so **no real credential was ever
exposed** — but a committed file containing a literal password is the habit
that eventually leaks a real one.

All of them now come from the environment via `.env`, which is gitignored.
Only `.env.example` is committed.

## Scope and limitations

Stated plainly: these are **local learning stacks**. They bind to localhost,
have no TLS, no backups, no resource limits and no monitoring of their own.
Do not expose them to a network you do not control.
