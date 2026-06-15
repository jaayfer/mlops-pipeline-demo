# Decisions Log

## 2026-06-15

**Decision**: Version control for the bike-sharing CSV using DVC instead of
committing directly to Git.
**Options considered:** Committing the CSV to Git vs. DVC.
**Why:** Git is unsuitable for large/binary data; DVC commits a small pointer file
(.dvc) and keeps the actual data in the cache/remote.
**Surprise / what went wrong:** Initially thought the CSV itself would go into
Git — in fact, `dvc add` automatically adds it to `.gitignore` inside the
directory that holds the file, and only the `.dvc` file is committed.
**How it was solved:** `.dvc` file + `.gitignore` committed, CSV stays out
of Git; `dvc status` is clean.
**Different under 100x load / in production:** DVC remote (e.g. S3) instead of
just a local cache, so a team can share the data.
