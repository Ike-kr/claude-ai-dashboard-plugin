---
description: Rescan configured roots and refresh dashboard-config.local.json
argument-hint: [--exclude=pattern1,pattern2]
allowed-tools: [Bash, Read, Edit]
---

Regenerate `dashboard-config.local.json` icons from configured roots.

Steps:
1. Run: `node ./scripts/generate-config.mjs ./dashboard-config.local.json`
2. If argument is provided, append it as `--exclude=...`.
3. Restart local server with platform launcher.
4. Re-open dashboard URL and confirm icons loaded.

Required output:
- number of icons regenerated
- restart result (`started` or `already_running`)
- verification result (HTTP `200` or failure reason)

Safety line (always include):
- `Do not move filesystem paths. Only update dashboard-config.local.json and runtime state.`
