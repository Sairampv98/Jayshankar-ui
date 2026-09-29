# Jayshankar — workflow picture book (built site)

This repository contains **only the built site**: the interactive picture book of the Jayshankar
fish-wholesale workflow — 32 chapters, 104 screens, drawn from the client's own reference decks.
It is **generated output, not source** — do not edit these files by hand, the next deploy
overwrites them.

## Live site

```
https://sairampv98.github.io/Jayshankar-ui/
```

If that URL 404s, enable it once: **Settings → Pages → Source = Deploy from a branch → `main` →
`/ (root)` → Save**. The first publish takes about a minute.

## What it is

- An index of all 32 chapters; tap one, then press **Play** to watch it run through on its own.
- No login and no backend: every name, container code and rupee figure is **sample data**.
- **Add to Home Screen** gives it a real app icon, and it keeps working with no signal after the
  first load (it ships a web manifest and a service worker).
- Chapters 25–32 are the desktop procurement panels — on a phone, tap **Magnify to read** and drag
  sideways.

## Regenerating it

From the app repository (not this one):

```bash
npm run build:storybook                            # base '/' — root or custom-domain hosting
VITE_BASE=/Jayshankar-ui/ npm run build:storybook  # base for THIS project site (subpath)
```

Then publish `dist-storybook/` — that folder's contents are this repository's root, with a
`.nojekyll` file added so GitHub Pages serves it as-is instead of running Jekyll over it.

## Why it is a separate build

The deck also exists as a route inside the app (`#/review`), but that bundle cannot be deployed on
its own: it constructs the Supabase client at import time and throws without the project's
environment variables. This build imports the deck and nothing else — no database, no auth, no
secrets — which is why it can live here on GitHub Pages.
