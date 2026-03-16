---
description: Check dashboard runtime status and common failure causes
allowed-tools: [Bash, Read]
---

Run a deterministic status check and report in this exact order:
1. Is port `8765` listening?
2. Does dashboard URL return HTTP `200`?
3. Are `dashboard-config.local.json` and `i18n/<lang>.json` reachable?
4. If failed, classify root cause as one of:
   - server_down
   - config_not_found
   - i18n_not_found
   - host_vm_mismatch
5. Print one concise recovery command for the detected root cause.

Output format:
- `server`: up | down
- `http`: 200 | non_200
- `config`: ok | missing
- `i18n`: ok | missing
- `root_cause`: one enum above
- `fix`: exact command(s)

Safety line (always include):
- `No filesystem paths were changed. This check is read-only.`
