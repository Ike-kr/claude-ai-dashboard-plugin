---
description: Start AI Dashboard local server and open dashboard page
argument-hint: [lang=ko|en]
allowed-tools: [Bash]
---

Start the local AI Dashboard runtime for this project.

Required behavior:
1. Resolve `lang` (`ko` default, `en` optional).
2. Detect OS and shell:
   - macOS/Linux: prefer `zsh ./start-dashboard.command`, fallback to `bash ./start-dashboard.command` if `zsh` is unavailable.
   - Windows: run `start-dashboard.bat`.
3. Verify runtime health:
   - Port `8765` is listening.
   - `GET /ai-dashboard.refactor.html?...` returns HTTP `200`.
4. Output one standard result block:
   - `status`: started | already_running | failed
   - `pid`: process id (if available)
   - `url`: exact URL with lang/config query
   - `log`: log file path
   - `next_action`: exact next command when failed

Connection/VM handling:
- If `ERR_CONNECTION_REFUSED`, automatically attempt one restart and re-check health.
- If running in VM/container/remote shell, clearly warn that `127.0.0.1` may not map to the user's host browser and provide an actionable host-side step.

Safety line (always include):
- `Filesystem paths were not moved. Only dashboard runtime/config state was touched.`
