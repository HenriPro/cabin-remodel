# Cabin remodel

Task map for the cabin remodel: dependencies, scope notes, and progress tracking.

**Live site:** [henripro.github.io/cabin-remodel](https://henripro.github.io/cabin-remodel/)

## What's in the repo

| File | Purpose |
|------|---------|
| [`index.html`](index.html) | Interactive flowchart, Gantt, task list, and status UI |
| [`cabin-remodel.md`](cabin-remodel.md) | Mermaid source (for editors that render Mermaid in preview) |
| [`status.json`](status.json) | Task progress, synced via git |

## Local preview

The site loads `status.json` over the network, so use a local server instead of opening the file directly:

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

## Tracking progress

Each task can be **to do**, **in progress**, or **done**.

### On the website

- Tap the **status pill** on a task row to cycle: to do → in progress → done.
- Or open a task and use the **status picker** in the detail sheet.
- Filter the task list with **All / To do / In progress / Done**.
- Progress counts appear in the header.

Changes save in your browser automatically (`localStorage`).

### Sync to git (and the live site)

1. Click **Copy status.json** in the task list section.
2. Paste into [`status.json`](status.json) and save.
3. Commit and push — GitHub Pages picks up the update.

### Edit the file directly

Only list tasks that are not *to do* — omitted keys default to to do:

```json
{
  "W1": "done",
  "W2": "in_progress"
}
```

Valid values: `"todo"`, `"in_progress"`, `"done"`.

On load, the site merges `status.json` with any browser overrides in `localStorage` (browser wins on conflict).
