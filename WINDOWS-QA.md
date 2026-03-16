# Windows QA Checklist (AI Dashboard Local)

Use this checklist before release or when validating a new update on Windows.

## Test Environment
- OS: Windows 10/11
- Browser: Chrome or Edge
- Python installed (`py` or `python`)
- Node installed (recommended for auto refresh)

## Quick Pass Checklist

1. Launch
- [ ] Run `start-dashboard.bat`
- [ ] Browser opens `http://127.0.0.1:8765/ai-dashboard.refactor.html?config=dashboard-config.local.json&lang=ko`
- [ ] Dashboard UI loads without blank screen or error page

2. Core Interaction
- [ ] Icons render on desktop area
- [ ] Search opens and returns results
- [ ] Category/type tabs filter icons correctly

3. Open Behavior
- [ ] Clicking file icon opens the file/app (or browser target)
- [ ] Clicking folder icon opens folder window or target path
- [ ] `/open` behavior works (no `ERR_CONNECTION_REFUSED`)

4. Context Menus
- [ ] Desktop right-click shows `휴지통 비우기` and it works
- [ ] Icon right-click shows `경로 복사`, and copy works
- [ ] Folder right-click shows `경로 복사` only for real filesystem folders
- [ ] Dashboard-created virtual folders do not expose copy-path

5. Clipboard
- [ ] `경로 복사` result pastes correctly in Notepad
- [ ] Copied path is absolute and usable

6. Trash
- [ ] Delete icon/folder moves item to Trash
- [ ] Restore works
- [ ] Empty Trash confirmation appears and clears items

7. Icon Scale / Layout
- [ ] Increasing icon size does not push items permanently out of view
- [ ] If space is insufficient, scale is auto-limited with notice
- [ ] Dragged icon positions are saved and restored after restart

8. Refresh / New Files
- [ ] Add a new file under configured root
- [ ] Refresh/restart shows new file icon
- [ ] Existing icon positions remain stable

## Optional Diagnostics (if issue occurs)

```bat
netstat -ano | findstr :8765
```

```bat
type "%TEMP%\ai-dashboard-server.log"
```

```bat
type "%TEMP%\ai-dashboard-refresh.log"
```

## Pass Criteria
- All items in sections 1-8 are checked.
- No blocker issues in launch/open/trash/copy-path flows.
