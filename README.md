# pi-oneliner

[![npm](https://img.shields.io/npm/v/pi-oneliner?style=flat)](https://www.npmjs.com/package/pi-oneliner)
[![license](https://img.shields.io/npm/l/pi-oneliner?style=flat)](./LICENSE)
[![stars](https://img.shields.io/github/stars/jerryfan/pi-oneliner?style=social)](https://github.com/jerryfan/pi-oneliner)

Sticky **one-line footer** for [pi coding agent](https://github.com/mariozechner/pi-coding-agent).
Optimized for **high-signal**, **zero-wrap** workflows.

What you get:
- always-visible session/repo + git branch (dirty/ahead/behind)
- compact right-side status strip from other extensions (`ctx.ui.setStatus(...)`)
- presets: `full` / `compact` / `ultra` (cycleable)
- optional i18n: re-render on `pi-i18n` locale change

If this helps your daily Pi loop, star the repo → it directly drives maintenance time.

---

## Install

Install with **Pi**, not npm:

```bash
pi install npm:pi-oneliner
```

Then in Pi:

```text
/reload
/oneliner
```

Project-local install (shared via `.pi/settings.json`):

```bash
pi install -l npm:pi-oneliner
```

---

## Quickstart

- picker UI (recommended): `/oneliner`
- show current state: `/oneliner show`
- switch preset: `/oneliner full|compact|ultra`
- toggle preset cycle: `/oneliner toggle`
- toggle status strip: `/oneliner statuses`
- zen mode: `/oneliner zen`
- self-check: `/oneliner doctor`

---

## Commands

- `/oneliner` (opens picker UI)
- `/oneliner show` (or `status`)
- `/oneliner full|compact|ultra`
- `/oneliner toggle`
- `/oneliner statuses`
- `/oneliner zen`
- `/oneliner doctor`
- `/oneliner save` (or `persist`)
- `/oneliner reload`
- `/oneliner help`

---

## Config

Config file:
- `~/.pi/agent/oneliner.json`

Fast path:
- `/oneliner save` writes current preset + toggles
- `/oneliner reload` reloads config

Common keys:
- `preset`: `"full" | "compact" | "ultra"`
- `shortCwd`: show last 2 cwd segments
- `maxSessionLen`, `maxBranchLen`, `maxCwdLen`: truncation controls
- `pollGitMs`: refresh git state without running git every render

Example (status allowlist):

```json
{
  "status": {
    "enabled": true,
    "right": {
      "mode": "allowlist",
      "allow": ["pi-semantic", "govern", "pi-i18n"],
      "priority": ["pi-semantic"],
      "maxVisible": 2
    }
  }
}
```

---

## Files

- config: `~/.pi/agent/oneliner.json`

---

## For extension authors (how to show up in the footer)

Oneliner does **not** hardcode other extension keys.
If your extension calls `ctx.ui.setStatus(key, value)`, oneliner can render it.

Minimal pattern:

```ts
ctx.ui.setStatus("myext", "ok");
// later…
ctx.ui.setStatus("myext", "✕");
```

Recommendations:
- keep values short (`ok`, `sync`, `95%`, `✕`)
- expose a stable key (don’t include versions)

---

## Troubleshooting

- **"Package not found"**
  - use full name: `npm:pi-oneliner`
- **Installed but `/oneliner` is unknown**
  - run `/reload` (or restart Pi)
- **Footer not showing**
  - oneliner only runs when `ctx.hasUI` is true (Pi TUI)

---

## Development

Local dev install:

```bash
pi install -l <path-to-pi-oneliner>
```

Then:

```text
/reload
/oneliner
```

---

## For maintainers

Release checklist:
- update `CHANGELOG.md`
- bump version: `npm version patch` (or minor/major)
- `npm publish`

---

## License

MIT
