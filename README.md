# Meridian

A monthly notebook. Twelve plates, one year. Private by default.

Once a month, sit with a single plate. Where you are, what changed, what you learned, what worries you, what excites you. Ten minutes. By plate twelve the season completes.

## Run it

It's a single static file. No build, no dependencies, no server.

```bash
# Open directly
open index.html

# Or serve locally
python3 -m http.server 8000
# → http://localhost:8000
```

## Host it on GitHub Pages

1. Push `index.html`, `README.md`, `LICENSE`, and `.nojekyll` to a public repo.
2. **Settings → Pages → Source: `main` / `(root)`**.
3. Wait a minute. Visit `https://<your-user>.github.io/<repo>`.

That's the whole deployment.

## How storage works

Notes live in your browser's `localStorage` — scoped to whatever URL you opened the app from. There is no server and no account.

- ✅ Close the tab and reopen later, same browser, same site — everything persists.
- ✅ Survives closing the browser, restarting your computer, weeks of not visiting.
- ❌ Different browser (Chrome ↔ Safari) → each has its own store.
- ❌ Different device → no sync.
- ❌ Incognito / private window → cleared when the window closes.
- ❌ "Clear browsing data" → wiped.

**Export every few months.** The Atlas page has an `Export · JSON` button. Save the file. If anything goes wrong, `Import · JSON` brings it back. Meridian also surfaces a quiet nudge to export every 3 plates.

## How the reminder works

Click **Remind me next month** on the Begin or Atlas page. A small `.ics` calendar file downloads. Open it; your calendar app (Apple Calendar, Google Calendar, Outlook) offers to add a recurring monthly event. From then on, your own calendar handles the reminder. Tapping the notification opens Meridian to write the next plate.

No push notifications, no server, no permissions to grant.

## Keyboard

- `⌘/Ctrl + S` — seal the current plate (force-save + a soft animation)
- `⌘/Ctrl + K` — jump to the current month's plate
- `Enter` inside a prompt — move to the next prompt
- `Esc` — close the settings drawer

## Settings (the ⚙ icon, top right)

- **Season title** — rename your season (default *Meridian, Vol. I*). Appears on the Atlas heading and the Poster.
- **Start month** — set or change the month your season begins. Past plates re-number themselves.
- **Reminder day** — the day each month your calendar reminder fires (1–28). Default 25.
- **Archive** — quick Export / Import JSON.
- **Reset** — wipe every plate and start over (with confirmation).

## The four pages

- **Begin** — the welcome / first-time view.
- **Plate** — write this month's plate. Pick a hue, fill in the five prompts.
- **Atlas** — see the whole season as a 4×3 grid. Click any plate to open it.
- **Poster** — generate a 24×36 in. poster of all twelve plates. Download as PDF (print) or PNG.

## Privacy & licence

Nothing is sent anywhere. The only network requests are Google Fonts on first load and (when you click "Download PNG") a single, SRI-pinned library from jsDelivr to rasterize the poster.

See `SECURITY.md` for the threat model, the Content-Security-Policy, the import validator, and what the app deliberately does *not* protect against.

**Licence: PolyForm Noncommercial 1.0.0** — see `LICENSE`. Free for personal use, research, hobby projects, and noncommercial organisations (charities, schools, public-research, government). Not for commercial use without a separate licence. Fork it, theme it, make it yours for any noncommercial purpose.
