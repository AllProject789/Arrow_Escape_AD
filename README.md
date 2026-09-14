# Arrow Escape — level content

Level data for the Arrow Escape Android app. The app ships the first 60 campaign levels
inside the APK and downloads everything else from here on first launch.

| file | what it is |
|---|---|
| `manifest.json` | version + zip URL + SHA-256. The only URL the app hardcodes. |
| `levels_v<N>.zip` | the pack the app downloads: 512 campaign levels + `level_order.json` |
| `level_order.json` | play order, step limits, difficulty |
| `levels/` | every level as its own file, for browsing and editing on github.com |

## Publishing new levels

1. Edit or add levels in the **app** repo under `app/src/main/assets/levels/`, and add them
   to `level_order.json`.
2. `python3 tools/build_levels_release.py --version <N+1> --prune-assets`
3. Copy `build/levels-release/` over this repo and push.

Bump `version` every time — clients only re-download when the manifest names a higher one.
Keep old `levels_v*.zip` files: installs that have not synced yet may still be fetching them.

Nothing here is executable. The app verifies the zip's SHA-256 against the manifest before
unpacking, and rejects entries that try to escape the cache directory.
