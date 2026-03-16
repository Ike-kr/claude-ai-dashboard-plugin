# AI Dashboard Local Plugin Marketplace

![version](https://img.shields.io/badge/version-v0.1.3-blue)
![platform](https://img.shields.io/badge/platform-macOS%20%7C%20Windows-green)
![claude](https://img.shields.io/badge/Claude%20Code-Plugin-purple)

Claude Code plugin marketplace for a cross-platform local AI dashboard workflow.

## Why this exists
- Aggregate scattered work folders into one dashboard.
- Open files/folders fast without path hunting.
- Refresh dashboard icons from real roots on demand.

## Included plugin
- Marketplace: `ike-ai-dashboard-marketplace`
- Plugin: `ai-dashboard-local`
- Commands:
  - `/dashboard-start`
  - `/dashboard-refresh`
  - `/dashboard-status`
  - `/dashboard-stop`
- Skill:
  - `dashboard-ops`

## Install
### From GitHub marketplace repo
```bash
claude plugin marketplace add https://github.com/Ike-kr/claude-ai-dashboard-plugin
claude plugin install ai-dashboard-local@ike-ai-dashboard-marketplace
```

### Local test install
```bash
cd /path/to/ai-dashboard-refactor
claude plugin marketplace add /path/to/ai-dashboard-refactor
claude plugin install ai-dashboard-local@ike-ai-dashboard-marketplace
```

## Runtime quick start
1. Create local config from template.

macOS/Linux:
```bash
cp dashboard-config.template.json dashboard-config.local.json
```

Windows (PowerShell):
```powershell
Copy-Item dashboard-config.template.json dashboard-config.local.json
```

2. Edit `dashboard-config.local.json`:
- set `namespace`
- set `roots`
- optional `excludePatterns`

3. Regenerate icons:
```bash
node scripts/generate-config.mjs dashboard-config.local.json
```

4. Launch dashboard:

macOS:
```bash
./start-dashboard.command
```

Windows:
```bat
start-dashboard.bat
```

`start-dashboard` launchers auto-refresh `dashboard-config.local.json` before starting server (if Node is available).

## Project structure
- `.claude-plugin/marketplace.json`
- `plugins/ai-dashboard-local/.claude-plugin/plugin.json`
- `plugins/ai-dashboard-local/commands/*`
- `plugins/ai-dashboard-local/skills/dashboard-ops/SKILL.md`
- `ai-dashboard.refactor.html`
- `scripts/local_dashboard_server.py`
- `scripts/generate-config.mjs`

## Cross-platform notes
- `/open` supports:
  - macOS: `open`
  - Windows: `os.startfile`
  - Linux: `xdg-open`
- Path tokens support `$HOME`, `{HOME}`, `~` with `/` and `\\` separators.
- If Claude runs inside VM/container, `127.0.0.1` may not be your host browser localhost. In that case, run start command on host shell.

## Safety guarantee
- This plugin does not move or rename your real filesystem paths.
- It only updates dashboard runtime state and `dashboard-config.local.json`.

## Release
- Current tag: `v0.1.3`
- Release title: `v0.1.3 - Version alignment for Claude in-app update`

See publish checklist: [`PUBLISH.md`](./PUBLISH.md)
