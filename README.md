# BMW M4 Competition — Pure Precision

**Live demo:** https://bmwsite-eta.vercel.app/

A dark, cinematic single-page landing site for the BMW M4 Competition, built as a
**frontend-only** project — no backend, no database, just HTML, CSS and vanilla JS.

---

## How it was built

The site was assembled from three AI tools, each owning one part of the pipeline:

| Stage | Tool | What it produced |
| --- | --- | --- |
| 1 | **Stitch** | The **user interface** — layout, glassmorphism panels, dark M-sport theme, typography (Syne / Space Grotesk / JetBrains Mono), the Material 3 color token system and every section/screen of the page. |
| 2 | **Flow** | The **M4 drift animation** — the 300-frame scroll-driven canvas sequence of the car sliding through the corner, preloaded with a progress bar and scrubbed frame-by-frame against scroll position. |
| 3 | **Antigravity** | The **integration** — merged the Stitch UI with the Flow animation, wired up scroll snapping, deck tabs, feature slides, loading screen and all interactive behaviour, then shipped it as one deployable static site. |

In short: **Stitch designed it → Flow animated the drift → Antigravity fused everything together.**

---

## Features

- **Scroll-driven 300-frame drift sequence** on a full-screen `<canvas>`, with device-pixel-ratio-aware scaling, letterboxed cover-fit rendering and inertia-smoothed frame interpolation.
- **Loading screen** with a real preload progress bar (`loaded / 300`).
- **Deck tabs** — `01 ENGINE · 02 AERO · 03 DRIFT · 04 CHASSIS` — that scroll-jump to their quarter of the sequence, plus a live `FRAME 001/300` counter and progress bar.
- **4 feature slides** (S58 TwinPower Turbo, Sculpted Aerodynamics, M xDrive 2WD Drift Mode, Carbon Ceramic Brakes) that cross-fade as the scroll deck advances.
- **Design / Performance / Technology / Gallery** sections, drive-mode switcher (Road · Sport · Track), tachometer readout, drift & damper analytics cards.
- Fully responsive, zero framework, zero build step.

## Tech stack

- HTML5 + Tailwind CSS (CDN) with a custom Material-3 style token config
- Vanilla ES module JavaScript (Vite-style hashed bundle in `assets/`)
- Canvas 2D for the frame sequence
- Hosted on Vercel

## Project structure

```
.
├── index.html                 # the whole page (Stitch UI + Antigravity wiring)
├── assets/
│   ├── index-*.css            # compiled styles / design tokens
│   ├── index-*.js             # scroll engine + canvas frame player
│   └── img/                   # gallery & emblem imagery
└── frames/
    ├── ezgif-frame-001..300.jpg   # the M4 drift animation (Flow)
    └── bmwlogo.jpg
```

## Run it locally

No build step required — any static server works:

```bash
python3 -m http.server 8099
# then open http://localhost:8099
```

## Notes

- This repository contains **only frontend code**.
- Everything ships from the `frames/` folder locally, so the site works offline
  except for the Google Fonts and Tailwind CDN requests.
