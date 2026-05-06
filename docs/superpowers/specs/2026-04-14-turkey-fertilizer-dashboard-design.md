# Design Spec: Turkey Fertilizer Crisis Dashboard
**Date:** 2026-04-14
**Status:** Implemented — dashboard.html in project root
**Source document:** `11_TURKEY_FERTILIZER_DEEP_DIVE.md`
**Output file:** `dashboard.html` (single file, project root)

---

## 1. Purpose

As a starting point a single-file interactive HTML dashboard that gives an at-a-glance overview of the Turkey fertilizer/agriculture crisis, driven by the analysis in `11_TURKEY_FERTILIZER_DEEP_DIVE.md`. The user moves 8 metric sliders (there should be an option to); those update 3 scenario probability bars; those drive 10 company ticker scores with Buy/Hold/Sell signals. Everything is colour-coded: high values trend red, low values trend green. 

Intended users: the analyst (daily monitoring), or another LLM/person picking up the work.

---

## 2. Deliverable

| Item | Detail |
|------|--------|
| File | `dashboard.html` — one self-contained file, no external dependencies |
| Location | Project root (`patterns_in_supply_chain_crisis/`) |
| Runtime | Open in any modern browser (Chrome, Firefox, Edge, Safari) |
| Dependencies | None — vanilla HTML + CSS + JavaScript only |

---

## 3. Layout

Three-column pipeline layout inside a single scrollable page.

```
┌──────────────────────────────────────────────────────────────┐
│  HEADER                                                       │
│  Title: "Turkey Fertilizer & Agriculture Crisis Dashboard"    │
│  Subtitle + date + [▼ Key Facts — collapsible strip]         │
├──────────────────┬───────────────┬───────────────────────────┤
│  COL 1           │  COL 2        │  COL 3                    │
│  METRICS         │  SCENARIOS    │  COMPANY TICKERS          │
│  (8 sliders)     │  (3 bars)     │  (10 rows)                │
├──────────────────┴───────────────┴───────────────────────────┤
│  FOOTER: source attribution + formula reminder               │
└──────────────────────────────────────────────────────────────┘
```

### 3.1 Header
- `<h1>` title
- `<p>` subtitle: "Based on 11_TURKEY_FERTILIZER_DEEP_DIVE.md · 2026-04-14"
- Collapsible "Key Facts" strip (collapsed by default, toggled by clicking ▼/▲ button):
  - 🌍 Turkey ranked **#2 globally** for fertilizer-trade vulnerability (after Brazil)
  - 📈 Urea price: $340 → >$600/MT (**+77%** since Dec 2025)
  - 🚨 Critical window: **Spring top-dressing April–May 2026** — right now
  - ⚠️ Scenario B (continued crisis) currently base case: **45–55%**
  - 🔴 War status: US naval blockade declared 2026-04-13; ceasefire talks failed

### 3.2 Column 1 — Metrics (8 sliders)
Column header: **"Crisis Metrics"** with subtitle "0 = calming · 100 = deepening"

Each metric row:
```
[Label]                        [value badge]
[━━━━━━━━●━━━━━━━━━━━━━━━━━━━] ← slider (range 0–100, step 1)
[short description line]
```

The value badge and slider track are coloured using the shared colour function.

| # | Label | Short description |
|---|-------|-------------------|
| 1 | Urea Spot Price | 0 = <$400/MT · 100 = >$700/MT |
| 2 | Brent Crude | 0 = <$85/bbl · 100 = >$130/bbl |
| 3 | TRY/USD Weakness | 0 = TRY stable (<42) · 100 = TRY collapsing (>52) |
| 4 | War Risk Insurance | 0 = normal (<0.5%) · 100 = extreme (>3%) |
| 5 | Diplomatic Progress | 0 = active ceasefire talks · 100 = blockade escalating |
| 6 | Turkey Food CPI | 0 = low pressure (<1% m/m) · 100 = surging (>5% m/m) |
| 7 | Govt Intervention | 0 = full subsidy + TMO active · 100 = no support |
| 8 | Drought / Rainfall | 0 = good rainfall · 100 = severe drought confirmed |

All sliders initialise at **50**.

### 3.3 Column 2 — Scenario Probabilities (3 bars)
Column header: **"Scenario Probabilities"**

**Two probability bars** (A and B always sum to 100) plus one **Tail Risk Gauge** (C):

| Element | Type | Description |
|---------|------|-------------|
| **A — De-escalation** | Probability bar (0–100) | Naval escort, ceasefire, urea <$500, 5–10% yield damage |
| **B — Continued / Escalating** | Probability bar (0–100) | Blockade persists, urea >$700, 15–25% yield damage |
| **C — Tail Risk Gauge** | Warning indicator (0–100) | Regime collapse, $150+ oil, IMF-level Turkey response |

Each bar row shows:
- Scenario label + one-line description
- Animated fill bar (width = value as %)
- Numeric value badge (0–100)
- Colour: shared colour function applied to bar fill and badge

A and B are **complementary** (A = 100 − B). They are displayed as a single two-tone bar in addition to separate rows, making the split immediately legible.

C is shown below with a distinct "⚠ Tail Risk" label and amber border to visually separate it from the probability bars.

Below the bars: collapsed formula box (toggled by "Show formula" link):
```
Scenario_B     = average(metric_1 … metric_8)
Scenario_A     = 100 − Scenario_B
Tail_Risk_C    = max(0, (Scenario_B − 70) / 30 × 100)
                 (0 when B ≤ 70; rises linearly to 100 when B = 100)
```

### 3.4 Column 3 — Company Tickers (10 rows)
Column header: **"Company Signals"** with subtitle "Score = scenario-weighted attractiveness"

Each company row:
```
[TICKER]  [Company name]              [score badge] [SIGNAL]
[████████████████░░░░░░░░░░░] ← colour bar
```

Signal label thresholds:

| Score | Signal label | Colour |
|-------|-------------|--------|
| ≥ 68 | **BUY** | bold green text |
| 58–67 | **HOLD+** | normal text |
| 42–57 | **HOLD** | grey text |
| 32–41 | **HOLD−** | normal text |
| ≤ 31 | **SELL / AVOID** | bold red text |

Note: signal label text colour is **independent** of the bar colour — the bar always follows the shared colour function (high = red, low = green). Signal text is its own semantic indicator.

Companies and their B-sensitivities:

| Ticker | Company | B_sens | Deep dive rationale |
|--------|---------|-------:|---------------------|
| TKFEN.IS | Tekfen Holding | +0.5 | E&C pipeline wins (A) + Toros Tarım scarcity pricing (B) |
| GUBRF.IS | Gübretaş | +0.7 | State-linked; scarcity pricing; subsidy conduit |
| BAGFS.IS | Bagfas | +0.8 | Pure-play; high beta to urea price crisis |
| HEKTS.IS | Hektaş | −0.6 | Pre-crisis negative EBITDA; crisis amplifies distress |
| TTRAK.IS | Türk Traktör | −0.8 | Rural income binary; only benefits from Scenario A |
| BIMAS.IS | BİM | +0.6 | Hard discount; proven crisis-alpha (2018/2021/2022) |
| MGROS.IS | Migros | −0.4 | Premium consumer hurt by crisis |
| SOKM.IS | Şok Marketler | +0.5 | Hard discount; defensive; same logic as BİM |
| ULKER.IS | Ülker | −0.4 | Wheat/sugar input cost squeeze in B |
| BANVT.IS | Banvit | −0.6 | Feed grain cost destruction in B |

---

## 4. Formula (Complete Reference)

```javascript
// All metrics initialised at 50
let metrics = [50, 50, 50, 50, 50, 50, 50, 50];

// Layer 1 → Layer 2
// A and B are complementary probabilities (always sum to 100).
// C is a separate Tail Risk Gauge (0–100), NOT a probability — do not add to A or B.
function calcScenarios(metrics) {
  const B = metrics.reduce((a, b) => a + b, 0) / metrics.length; // 0–100
  const A = 100 - B;                                              // 0–100, A+B = 100
  const C = Math.max(0, (B - 70) / 30 * 100);                   // 0–100 tail gauge
  return { A, B, C };
}

// Layer 2 → Layer 3
const B_SENS = {
  'TKFEN': +0.5, 'GUBRF': +0.7, 'BAGFS': +0.8,
  'HEKTS': -0.6, 'TTRAK': -0.8,
  'BIMAS': +0.6, 'MGROS': -0.4, 'SOKM':  +0.5,
  'ULKER': -0.4, 'BANVT': -0.6
};

function calcCompany(ticker, scenarios) {
  const raw = 50 + B_SENS[ticker] * (scenarios.B - 50);
  return Math.min(100, Math.max(0, raw));
}

// Colour function (applies to ALL values — metrics, scenarios, companies)
function valueToColor(v) {
  const hue = Math.round(120 * (1 - v / 100));      // 120 (green) → 0 (red)
  const sat = 65;
  const lit = 42 + Math.abs(v - 50) * 0.15;         // slight brightness boost at extremes
  return `hsl(${hue}, ${sat}%, ${lit}%)`;
}
```

---

## 5. Colour System

Single rule applied to every numeric value across the entire dashboard:

| Value | Hue | Appearance |
|------:|-----|-----------|
| 0 | 120° | 🟢 Green |
| 25 | 90° | Yellow-green |
| 50 | 60° | 🟡 Yellow (neutral) |
| 75 | 30° | Orange |
| 100 | 0° | 🔴 Red |

Applied to:
- Slider thumb and track fill
- Value badges (metrics, scenarios, company scores)
- Scenario bar fill
- Company score bar fill

NOT applied to:
- Signal label text (BUY/HOLD/SELL use their own semantic colours — see §3.4)
- Background and structural chrome (neutral dark theme)

---

## 6. Interactivity

- All sliders trigger immediate live recalculation on `input` event (no submit button)
- All value badges and bars animate smoothly via CSS `transition: all 0.25s ease`
- Collapsible Key Facts strip: click ▼/▲ to toggle, collapsed by default
- "Show formula" toggle under scenario bars: click to expand/collapse the formula box
- No network requests, no external scripts, no localStorage — pure in-memory state

---

## 7. Visual Style

Dark-themed dashboard appropriate for a data monitoring tool.

| Element | Style |
|---------|-------|
| Background | `#0f1117` (near-black) |
| Panel cards | `#1a1d27` with `1px solid #2a2d3a` border |
| Body text | `#c8ccd8` |
| Labels | `#6b7080` (muted) |
| Value badges | `background: valueToColor(v)`, white text, `border-radius: 4px` |
| Column headers | `#e2e4ec` bold |
| Accent / signal BUY | `#4ade80` (green text) |
| Signal SELL/AVOID | `#f87171` (red text) |
| Font | System stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif` |
| Column gap | `1.5rem` |
| Slider track | Custom styled with `accent-color` matching value colour |

---

## 8. Footer

```
Source: 11_TURKEY_FERTILIZER_DEEP_DIVE.md · patterns_in_supply_chain_crisis wiki
Formula: Scenario_B = avg(metrics) · Company = 50 + B_sens × (B − 50)
Last updated: 2026-04-14 · Session 002b
```

---

## 9. File Structure

Everything lives in one file:

```
dashboard.html
├── <style>          — all CSS inline in <head>
├── <body>
│   ├── header
│   ├── .dashboard-grid (3-column CSS grid)
│   │   ├── .col-metrics
│   │   ├── .col-scenarios
│   │   └── .col-companies
│   └── footer
└── <script>         — all JS inline before </body>
    ├── DATA constants (metrics config, company config)
    ├── calcScenarios()
    ├── calcCompany()
    ├── valueToColor()
    ├── renderAll()    — rebuilds badges/bars/signals on every slider change
    └── init()         — builds DOM from DATA, attaches event listeners
```

---

## 10. Handoff Notes (for another person or LLM)

**To update metric definitions:** Edit the `METRICS` array in the `<script>` section. Each entry has `{ id, label, description }`.

**To change B-sensitivities:** Edit the `COMPANIES` array. Each entry has `{ ticker, name, bSens }`. Values should stay in range −1.0 to +1.0.

**To add a new metric:** Add entry to `METRICS` array. Formula automatically includes it in the average.

**To add a new company:** Add entry to `COMPANIES` array. The render loop picks it up automatically.

**To change signal thresholds:** Edit the `getSignal(score)` function. Default thresholds: ≥68 BUY, ≥58 HOLD+, ≥42 HOLD, ≥32 HOLD−, else SELL/AVOID.

**To change the colour curve:** Edit `valueToColor(v)`. Currently: `hue = 120 × (1 − v/100)`. This maps 0→green, 50→yellow, 100→red.

**Source analysis:** All B-sensitivity values and scenario descriptions are derived from `11_TURKEY_FERTILIZER_DEEP_DIVE.md` in this repository. That document contains the full reasoning, probability ranges, and watchlist questions that inform this dashboard.

---

*Spec written: 2026-04-14 — brainstorming session, approved by user*
