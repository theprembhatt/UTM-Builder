# UTM-Builder

A simple UTM builder for BimaScore campaign links. Pick a destination, fill source / medium / campaign, and get one clean, consistent tracking link.

Built as a single `index.html` file — no build step, no backend, no login.

## Destinations

- `bimascore.com` — main website
- `clarity.bimascore.com` — Bima Clarity
- `analyze.bimascore.com` — Bima Analyze

## What it does

- Builds `utm_source`, `utm_medium`, `utm_campaign` links, plus optional `utm_term` and `utm_content`
- Optional page path (e.g. `blogs/health-insurance-guide`)
- Live link preview while typing
- Auto-clean values: lowercase, spaces/underscores → hyphens
- Copy link and test link in one click
- Saved links sidebar with **copy**, **edit / update** and **remove**
- Saved links stay in the browser (`localStorage`) — nothing is sent anywhere
- Mobile responsive

## Use it

Open the file directly:

```bash
open index.html        # macOS
xdg-open index.html    # Linux
```

Or serve it locally:

```bash
python3 -m http.server 8931
# http://localhost:8931/index.html
```

## Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl / Cmd + Enter` | Copy the link |
| `Ctrl / Cmd + S` | Save / update the link |

## Example link

```
https://clarity.bimascore.com?utm_source=internal&utm_medium=via-team&utm_campaign=sanitation-testing
```

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole tool (HTML + CSS + JS) |
| `FLOW.md` | How the tool works |
| `MEMORY.md` | Build history and decisions |

## Deploy

Any static host works. On Vercel: import this repo, framework preset **Other**, no build command, output directory `.`.
