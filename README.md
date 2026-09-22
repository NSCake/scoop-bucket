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
| [`ttrff`](https://github.com/NSExceptional/ttrff) | tray controller for the ttrff cosmetic Toontown Rewritten animation mods (rolling build of `main`) |

## Adding a package

Drop `<app>.json` in the repo root (a standard Scoop manifest whose `url` points at a
**rolling** artifact, e.g. `releases/latest/download/<app>.zip`). The
[`sync-manifests`](.github/workflows/sync-manifests.yml) workflow downloads each rolling
artifact on a schedule, refreshes the manifest's `hash`, and bumps a monotonic `version`
so `scoop update` picks it up — no per-app configuration, no secrets.
