# Liquid Co-Pilot — Update Feed

This public repo is the update channel for the Liquid Co-Pilot app.
It holds no source code — only the small files installed copies check:

- `version.json` — the feed. Installed apps read it on launch.
- `brainpack.zip` — Nova's current brain (her system prompt), packaged
  by `make_brainpack.py` in the main (private) repo.

## How updates reach users

- **Brain updates** (prompt improvements): if `brain_version` in
  `version.json` is newer than an installed copy's, the app downloads
  `brainpack.zip`, verifies its sha256 against the feed, and applies
  it automatically. Takes effect at the user's next session start.
- **App updates**: if `app_version` is newer, the app shows a banner
  with a download button pointing at `app_url`.

## Publishing a brain update

1. In the main repo, edit `context-pack/system-prompt.md`.
2. Run: `python make_brainpack.py --brain-version N --app-version X.Y.Z
   --brain-url https://raw.githubusercontent.com/LiquidInsomnia/Liquid-Copilot-Releases/main/brainpack.zip
   --app-url https://github.com/LiquidInsomnia/Liquid-Copilot-Releases/releases
   --out <this repo>`
   (N = previous brain_version + 1)
3. Commit and push the regenerated `brainpack.zip` + `version.json` here.

## Publishing an app update

1. Build the new `LiquidCopilot-Setup.exe` in the main repo.
2. Create a GitHub Release here, attach the Setup.exe, and set
   `app_url` in `version.json` to the release asset's download URL
   (and `app_version` to the new version). Commit `version.json`.
