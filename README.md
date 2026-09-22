# NSCake scoop-bucket

Scoop bucket for NSCake packages — the Windows analog of [NSCake/homebrew-tap](https://github.com/NSCake/homebrew-tap).

## Install

```powershell
scoop bucket add nscake https://github.com/NSCake/scoop-bucket
scoop install ttrff
```

Update everything with `scoop update`.

## Packages

| app | what it is |
|---|---|
| [`ttrff`](https://github.com/NSExceptional/ttrff) | tray controller for the ttrff cosmetic Toontown Rewritten animation mods (tracks `main`) |

## How it works

Each manifest installs the app repo's **GitHub branch archive** (`archive/refs/heads/main.zip`)
— the repo IS the payload, exactly like a Homebrew `--HEAD` formula. No CI, no built
artifacts, no hash (a branch archive's bytes change on every push, so a pinned hash would
go stale instantly; Scoop prints the computed SHA256 at install instead). The
[`sync-manifests`](.github/workflows/sync-manifests.yml) workflow's only job is recording
each source repo's latest `main` commit sha as the manifest `version` (every 6h + on push) —
that's what makes `scoop update` see new commits.

## Adding a package

Drop `<app>.json` in the repo root with a `url` pointing at the app repo's branch archive,
an `extract_dir` matching the archive's root folder (`<repo>-main`), and a `source_repo` key.
The sync workflow records its latest commit sha as the version automatically — no per-app
configuration, no secrets.
