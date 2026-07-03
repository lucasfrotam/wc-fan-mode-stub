# World Cup Fan Mode

**Feature stub for [aitrainingplan.app](https://aitrainingplan.app)** — built during the We The Flywheel *Agentic Engineer* assessment.

**Live demo:** https://lucasfrotam.github.io/wc-fan-mode-stub/

---

## Overview

Endurance athletes who follow the World Cup face a scheduling conflict that neither sports-betting apps nor generic training plans solve: **late kickoffs destroy sleep, spike acute training load (ATL), and push ACWR into injury territory** — right when CTL should stay stable before an A-race.

**World Cup Fan Mode** is a single-page feature stub that:

1. Maps [Tipmaster](https://tipmaster.de/world-cup/) Cup Run schedules to training-load rules
2. Projects CTL / ATL / TSB impact with a 7-day chart
3. Reschedules the athlete's week automatically
4. Exports a **Portable AI Coach Prompt** (mirroring AiTrainingPlan's core workflow)

No backend. No frameworks. One HTML file + SVG favicon.

---

## Product judgement

| Product | Owns | Gap |
|---------|------|-----|
| **tipmaster.de** | Match predictions, Cup Runs, DACH fan leagues | Nothing about physical training |
| **aitrainingplan.app** | CTL/ATL/TSB, ACWR, adaptive AI coaching | Nothing about tournament-month life disruption |

**Overlap audience:** German-speaking football fans who also run marathons, triathlons, or HYROX.

This stub fills the gap **without cloning either UI** — it borrows Tipmaster's Cup Run calendar as input signals and outputs AiTrainingPlan-style coaching artifacts.

---

## Features

- **Cup Run selector** — real WC 2026 windows from Tipmaster (Runs 1, 3, 5, 12)
- **A-race proximity slider** — tightens deload when race is &lt; 6 weeks out
- **Load projection** — CTL Δ, ATL Δ, TSB, injury risk label
- **ACWR gauge** — color-coded bar (green → amber → red at 1.3+)
- **7-day TSB chart** — canvas sparkline with match-night ATL spike
- **Adjusted training plan** — day-by-day sessions with intensity tags
- **Halftime protocol** — 12-min mobility block (counter 90′ seated posture)
- **Portable AI Coach Prompt** — structured prompt for ChatGPT / Claude / Gemini
- **EN / DE toggle** — DACH market localization
- **Comparison table** — Tipmaster vs AiTrainingPlan vs this stub (product judgement)
- **Share link** — URL params + localStorage persist state (`?nation=germany&cupRun=weekday_late&raceWeeks=8`)
- **Copy plan as markdown** — portable output for coaches / Notion
- **Integration roadmap** — 5-phase production path with Tipmaster cross-sell
- **AI Consensus Coaching** — dual coach debate + synthesis (mirrors AiTrainingPlan's two-model workflow)
- **Chart tooltips** — hover TSB values, form labels, match-night ATL spikes

---

## How it works

```
User inputs                Rules engine                 Outputs
─────────────             ─────────────                ───────
Nation          ──┐
Cup Run type    ──┼──▶  Load rules + race proximity  ──▶  Metrics + ACWR bar
Weeks to race   ──┘       Cup Run copy                  7-day plan
                                                          TSB chart
                                                          AI coach prompt
```

### Load rules (simplified)

| Scenario | CTL Δ | ATL Δ | TSB | ACWR | Injury |
|----------|-------|-------|-----|------|--------|
| Early CET weekday | −2 | +8 | −10 | 1.12 | Low |
| Late 22:00 CET | −3 | +14 | −17 | 1.28 | Moderate |
| Weekend block | 0 | +4 | −4 | 0.98 | Low |
| Knockout / 02:00 | −5 | +22 | −27 | 1.42 | High |

If A-race &lt; 6 weeks: extra deload applied (CTL −1, ATL +3, ACWR +0.08).

---

## Tech decisions

| Choice | Why |
|--------|-----|
| **Vanilla HTML/CSS/JS** | 25-minute assessment window — zero build step |
| **Canvas chart** | Lightweight TSB visualization without Chart.js |
| **Clipboard API** | One-click Portable Prompt export |
| **SVG favicon** | Crisp on retina, tiny payload |
| **GitHub Pages** | Free public URL, instant deploy from `main` |
| **i18n object in JS** | DE locale for Tipmaster's primary market without i18n lib |

---

## Local development

```bash
git clone https://github.com/lucasfrotam/wc-fan-mode-stub.git
cd wc-fan-mode-stub

# any static server works
python3 -m http.server 8080
# open http://localhost:8080
```

Or open `index.html` directly in a browser (clipboard API requires HTTPS or localhost).

---

## Deploy (GitHub Pages)

1. Push `main` branch
2. Repo → **Settings** → **Pages**
3. Source: **Deploy from branch** → `main` / `/ (root)`
4. Live at `https://<username>.github.io/wc-fan-mode-stub/`

---

## File structure

```
wc-fan-mode-stub/
├── index.html       # entire app (UI + logic + styles)
├── favicon.svg      # tab icon
├── social-card.svg  # Open Graph preview image
├── manifest.json    # PWA metadata
└── README.md        # this file
```

---

## What I'd ship next (given more time)

- [ ] Pull live kickoff times from Tipmaster's public schedule API
- [ ] Garmin / Strava OAuth to read real CTL/ATL instead of projections
- [ ] Persist adjusted weeks to AiTrainingPlan dashboard via API
- [ ] Push halftime reminder notification at match HT whistle

---

## Links

- **Demo:** https://lucasfrotam.github.io/wc-fan-mode-stub/
- **Target product:** https://aitrainingplan.app
- **Inspiration:** https://tipmaster.de/world-cup/
- **Assessment:** We The Flywheel — Agentic Engineer (Entry-Level)

---

*Built with deliberate product thinking + AI co-creation (Cursor). Assessment work — © The Flywheel Corporation per assessment terms.*
