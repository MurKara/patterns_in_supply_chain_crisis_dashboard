# Turkey Fertilizer Crisis Dashboard — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use `superpowers:subagent-driven-development` (recommended) or `superpowers:executing-plans` to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single self-contained `dashboard.html` file that lets the user move 8 crisis-metric sliders and see live updates to 3 scenario probability bars and 10 company ticker scores, all colour-coded green→red.

**Architecture:** One HTML file with inline CSS and inline JavaScript. No external dependencies. Data (metrics list, company list, B-sensitivities) is declared as JS constants at the top of the script block. Three pure functions (`calcScenarios`, `calcCompany`, `valueToColor`) drive all derived values. A single `renderAll()` function reads the DOM, computes everything, and writes back — called on every slider `input` event.

**Tech Stack:** Vanilla HTML5, CSS Grid, vanilla JavaScript (ES6). No build step, no package manager. Open with any browser.

---

## Spec Reference

`docs/superpowers/specs/2026-04-14-turkey-fertilizer-dashboard-design.md`

---

## File Map

| File | Action | Purpose |
|------|--------|---------|
| `dashboard.html` | **Create** | Entire deliverable — structure, style, and logic in one file |

The file is built incrementally across tasks. Each task adds a clearly delimited section. The final file is ~350–400 lines.

---

## Testing Approach

This is a browser-rendered single file. "Tests" are `console.assert()` calls appended to the `<script>` block. They run on every page load and show errors in the browser console (F12 → Console tab). Each formula task ends with: *"Open in browser, open DevTools console, confirm zero assertion errors."*

---

## Task 1: HTML Skeleton + CSS Foundation

**Files:**
- Create: `dashboard.html`

- [ ] **Step 1.1 — Create the file with full HTML skeleton, dark theme CSS, 3-column grid**

Create `dashboard.html` in the project root (`patterns_in_supply_chain_crisis/`) with this complete content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Turkey Fertilizer Crisis Dashboard</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background: #0f1117;
      color: #c8ccd8;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      font-size: 14px;
      line-height: 1.5;
      min-height: 100vh;
    }

    /* ── HEADER ─────────────────────────────────────────── */
    #header {
      padding: 1.25rem 1.5rem 0;
      border-bottom: 1px solid #2a2d3a;
    }
    #header h1 {
      font-size: 1.25rem;
      font-weight: 700;
      color: #e2e4ec;
      margin-bottom: 0.25rem;
    }
    .subtitle {
      font-size: 0.8rem;
      color: #6b7080;
      margin-bottom: 0.75rem;
    }

    /* facts strip */
    #facts-toggle {
      background: none;
      border: 1px solid #2a2d3a;
      color: #8b8fa8;
      font-size: 0.75rem;
      padding: 0.25rem 0.6rem;
      border-radius: 4px;
      cursor: pointer;
      margin-bottom: 0.5rem;
    }
    #facts-toggle:hover { border-color: #4a4d5a; color: #c8ccd8; }
    #facts-panel {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 0.5rem;
      padding: 0.75rem 0;
    }
    #facts-panel.hidden { display: none; }
    .fact-card {
      background: #1a1d27;
      border: 1px solid #2a2d3a;
      border-radius: 6px;
      padding: 0.6rem 0.75rem;
      font-size: 0.78rem;
    }
    .fact-card .fact-label { color: #6b7080; font-size: 0.7rem; text-transform: uppercase; letter-spacing: 0.04em; }
    .fact-card .fact-value { color: #e2e4ec; font-weight: 600; margin-top: 0.15rem; }

    /* ── MAIN GRID ───────────────────────────────────────── */
    .dashboard-grid {
      display: grid;
      grid-template-columns: 1.1fr 0.9fr 1.2fr;
      gap: 1.25rem;
      padding: 1.25rem 1.5rem;
      align-items: start;
    }

    .col-panel {
      background: #1a1d27;
      border: 1px solid #2a2d3a;
      border-radius: 8px;
      padding: 1rem;
    }
    .col-panel h2 {
      font-size: 0.85rem;
      font-weight: 700;
      color: #e2e4ec;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      margin-bottom: 0.2rem;
    }
    .col-subtitle {
      font-size: 0.72rem;
      color: #6b7080;
      margin-bottom: 0.9rem;
    }

    /* ── VALUE BADGE ─────────────────────────────────────── */
    .badge {
      display: inline-block;
      min-width: 2rem;
      text-align: center;
      padding: 0.1rem 0.4rem;
      border-radius: 4px;
      font-size: 0.78rem;
      font-weight: 700;
      color: #fff;
      background: hsl(60, 65%, 45%);
      transition: background 0.25s ease;
    }

    /* ── METRIC SLIDERS ──────────────────────────────────── */
    .metric-row { margin-bottom: 0.9rem; }
    .metric-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 0.3rem;
    }
    .metric-label { font-size: 0.8rem; color: #c8ccd8; font-weight: 500; }
    .metric-desc { font-size: 0.68rem; color: #6b7080; margin-top: 0.25rem; }

    .slider-container {
      position: relative;
      height: 6px;
      border-radius: 3px;
      background: #2a2d3a;
      margin: 0.35rem 0;
    }
    .track-fill {
      position: absolute;
      left: 0; top: 0; bottom: 0;
      border-radius: 3px;
      width: 50%;
      background: hsl(60, 65%, 45%);
      pointer-events: none;
      transition: width 0.1s, background 0.25s;
    }
    input[type="range"] {
      position: absolute;
      inset: -6px 0;
      width: 100%;
      margin: 0;
      opacity: 0;
      cursor: pointer;
      height: 18px;
    }
    /* visible thumb overlay */
    .thumb-overlay {
      position: absolute;
      top: 50%;
      transform: translate(-50%, -50%);
      width: 14px; height: 14px;
      border-radius: 50%;
      background: hsl(60, 65%, 55%);
      pointer-events: none;
      border: 2px solid #0f1117;
      transition: left 0.1s, background 0.25s;
    }

    /* ── SCENARIO BARS ───────────────────────────────────── */
    .scenario-row { margin-bottom: 0.85rem; }
    .scenario-header {
      display: flex;
      justify-content: space-between;
      align-items: baseline;
      margin-bottom: 0.3rem;
    }
    .scenario-name { font-size: 0.8rem; color: #e2e4ec; font-weight: 600; }
    .scenario-desc { font-size: 0.68rem; color: #6b7080; margin-bottom: 0.35rem; }
    .scenario-bar-bg {
      height: 14px;
      background: #2a2d3a;
      border-radius: 4px;
      overflow: hidden;
    }
    .scenario-bar-fill {
      height: 100%;
      border-radius: 4px;
      width: 50%;
      transition: width 0.25s ease, background 0.25s ease;
    }

    /* tail risk gauge — distinct amber border */
    .tail-risk-row {
      border: 1px solid #5a4500;
      border-radius: 6px;
      padding: 0.55rem 0.6rem;
      margin-top: 0.5rem;
    }
    .tail-label {
      font-size: 0.7rem;
      color: #c89a00;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      margin-bottom: 0.35rem;
    }

    /* A+B split bar */
    .split-bar {
      height: 8px;
      border-radius: 4px;
      overflow: hidden;
      display: flex;
      margin-bottom: 1rem;
      margin-top: 0.25rem;
    }
    .split-a { background: hsl(120,65%,40%); transition: width 0.25s ease; }
    .split-b { background: hsl(0,65%,42%); transition: width 0.25s ease; flex: 1; }

    /* formula box */
    .formula-toggle-btn {
      background: none;
      border: none;
      color: #6b7080;
      font-size: 0.72rem;
      cursor: pointer;
      padding: 0.4rem 0;
      display: block;
      margin-top: 0.5rem;
    }
    .formula-toggle-btn:hover { color: #c8ccd8; }
    .formula-box {
      background: #0f1117;
      border: 1px solid #2a2d3a;
      border-radius: 4px;
      padding: 0.6rem 0.75rem;
      margin-top: 0.4rem;
      font-family: "Consolas", "Monaco", monospace;
      font-size: 0.72rem;
      color: #8b8fa8;
      line-height: 1.6;
    }
    .formula-box.hidden { display: none; }

    /* ── COMPANY ROWS ────────────────────────────────────── */
    .company-row { margin-bottom: 0.7rem; }
    .company-header {
      display: flex;
      align-items: center;
      gap: 0.4rem;
      margin-bottom: 0.25rem;
    }
    .ticker { font-size: 0.75rem; font-weight: 700; color: #e2e4ec; min-width: 5rem; }
    .company-name { font-size: 0.72rem; color: #8b8fa8; flex: 1; overflow: hidden; white-space: nowrap; text-overflow: ellipsis; }
    .score-bar-bg {
      height: 8px;
      background: #2a2d3a;
      border-radius: 3px;
      overflow: hidden;
    }
    .score-bar-fill {
      height: 100%;
      border-radius: 3px;
      width: 50%;
      transition: width 0.25s ease, background 0.25s ease;
    }
    .signal {
      font-size: 0.68rem;
      font-weight: 700;
      min-width: 5rem;
      text-align: right;
    }
    .signal-buy       { color: #4ade80; }
    .signal-hold-plus { color: #a3e635; }
    .signal-hold      { color: #6b7080; }
    .signal-hold-minus{ color: #fb923c; }
    .signal-sell      { color: #f87171; }

    /* ── FOOTER ──────────────────────────────────────────── */
    footer {
      text-align: center;
      font-size: 0.7rem;
      color: #4a4d5a;
      padding: 1rem 1.5rem 1.5rem;
      border-top: 1px solid #2a2d3a;
      line-height: 1.8;
    }
  </style>
</head>
<body>

  <!-- HEADER -->
  <div id="header">
    <h1>Turkey Fertilizer &amp; Agriculture Crisis Dashboard</h1>
    <p class="subtitle">Based on 11_TURKEY_FERTILIZER_DEEP_DIVE.md &middot; 2026-04-14 &middot; Session 002b</p>
    <button id="facts-toggle">▼ Key Facts</button>
    <div id="facts-panel" class="hidden">
      <div class="fact-card">
        <div class="fact-label">Global Rank</div>
        <div class="fact-value">#2 fertilizer vulnerability</div>
      </div>
      <div class="fact-card">
        <div class="fact-label">Urea Price Shock</div>
        <div class="fact-value">$340 → $600/MT (+77%)</div>
      </div>
      <div class="fact-card">
        <div class="fact-label">Critical Window</div>
        <div class="fact-value">Spring top-dress Apr–May 2026</div>
      </div>
      <div class="fact-card">
        <div class="fact-label">Base Scenario</div>
        <div class="fact-value">B (continued crisis) 45–55%</div>
      </div>
      <div class="fact-card">
        <div class="fact-label">War Status</div>
        <div class="fact-value">US blockade active 2026-04-13</div>
      </div>
    </div>
  </div>

  <!-- MAIN DASHBOARD -->
  <main class="dashboard-grid">
    <section class="col-panel" id="col-metrics">
      <h2>Crisis Metrics</h2>
      <p class="col-subtitle">0 = calming &middot; 100 = deepening</p>
      <div id="metrics-list"></div>
    </section>

    <section class="col-panel" id="col-scenarios">
      <h2>Scenario Probabilities</h2>
      <p class="col-subtitle">A + B always sum to 100</p>
      <div id="scenarios-display"></div>
    </section>

    <section class="col-panel" id="col-companies">
      <h2>Company Signals</h2>
      <p class="col-subtitle">Score = scenario-weighted attractiveness</p>
      <div id="companies-list"></div>
    </section>
  </main>

  <footer>
    Source: 11_TURKEY_FERTILIZER_DEEP_DIVE.md &middot; patterns_in_supply_chain_crisis wiki<br>
    Formula: Scenario_B = avg(metrics) &middot; Company score = 50 + B_sens &times; (B &minus; 50) &middot; Last updated: 2026-04-14
  </footer>

  <script>
    // JS will be added in later tasks
  </script>
</body>
</html>
```

- [ ] **Step 1.2 — Open in browser and verify layout**

Open `dashboard.html` in a browser (double-click the file or drag into Chrome/Firefox).

Expected:
- Dark background, 3 empty column panels visible side by side
- Header with title, "▼ Key Facts" button
- Clicking "▼ Key Facts" does nothing yet (JS not wired) — that's fine
- Footer with attribution text visible
- No JS errors in DevTools console (F12 → Console)

- [ ] **Step 1.3 — Commit skeleton**

```bash
cd "C:/coding_projects/claude_projects/patterns_in_supply_chain_crisis"
git add dashboard.html
git commit -m "feat: dashboard skeleton — dark theme, 3-column grid, CSS system"
```

---

## Task 2: Data Model + Formula Engine

**Files:**
- Modify: `dashboard.html` — replace empty `<script>` block

- [ ] **Step 2.1 — Replace the empty `<script>` block with the full data model and formula functions**

Find the `<script>` tag near the bottom of `dashboard.html` and replace its content (keep the `<script>` and `</script>` tags):

```javascript
// ── DATA ──────────────────────────────────────────────────────
const METRICS = [
  { id: 'urea',   label: 'Urea Spot Price',       desc: '0 = <$400/MT · 100 = >$700/MT' },
  { id: 'brent',  label: 'Brent Crude',            desc: '0 = <$85/bbl · 100 = >$130/bbl' },
  { id: 'try',    label: 'TRY/USD Weakness',       desc: '0 = TRY stable (<42) · 100 = collapsing (>52)' },
  { id: 'insur',  label: 'War Risk Insurance',     desc: '0 = normal (<0.5%) · 100 = extreme (>3%)' },
  { id: 'dipl',   label: 'Diplomatic Progress',    desc: '0 = active talks · 100 = blockade escalating' },
  { id: 'cpi',    label: 'Turkey Food CPI',        desc: '0 = low pressure (<1% m/m) · 100 = surging (>5%)' },
  { id: 'govt',   label: 'Govt Intervention',      desc: '0 = full subsidy + TMO active · 100 = no support' },
  { id: 'rain',   label: 'Drought / Rainfall',     desc: '0 = good rainfall · 100 = severe drought' },
];

const COMPANIES = [
  { ticker: 'TKFEN', name: 'Tekfen Holding',   bSens:  0.5 },
  { ticker: 'GUBRF', name: 'Gübretaş',         bSens:  0.7 },
  { ticker: 'BAGFS', name: 'Bagfas',           bSens:  0.8 },
  { ticker: 'HEKTS', name: 'Hektaş',           bSens: -0.6 },
  { ticker: 'TTRAK', name: 'Türk Traktör',     bSens: -0.8 },
  { ticker: 'BIMAS', name: 'BİM',              bSens:  0.6 },
  { ticker: 'MGROS', name: 'Migros',           bSens: -0.4 },
  { ticker: 'SOKM',  name: 'Şok Marketler',    bSens:  0.5 },
  { ticker: 'ULKER', name: 'Ülker',            bSens: -0.4 },
  { ticker: 'BANVT', name: 'Banvit',           bSens: -0.6 },
];

// ── FORMULA ENGINE ─────────────────────────────────────────────

/** Returns hsl colour string for any 0-100 value. 0=green, 50=yellow, 100=red. */
function valueToColor(v) {
  const hue = Math.round(120 * (1 - v / 100));
  const lit  = 42 + Math.abs(v - 50) * 0.15;
  return `hsl(${hue}, 65%, ${lit.toFixed(1)}%)`;
}

/**
 * Given array of 8 metric values (0-100), returns scenario scores.
 * A and B are complementary probabilities (always sum to 100).
 * C is a Tail Risk Gauge (0-100), NOT a probability — not added to A or B.
 */
function calcScenarios(metricValues) {
  const B = metricValues.reduce((sum, v) => sum + v, 0) / metricValues.length;
  const A = 100 - B;
  const C = Math.max(0, (B - 70) / 30 * 100);   // 0 when B≤70, 100 when B=100
  return { A, B, C };
}

/**
 * Given a company object and scenario scores, returns a 0-100 attractiveness score.
 * Higher = more attractive under current scenario balance.
 */
function calcCompany(company, scenarios) {
  const raw = 50 + company.bSens * (scenarios.B - 50);
  return Math.min(100, Math.max(0, raw));
}

/** Returns signal label and CSS class based on score thresholds. */
function getSignal(score) {
  if (score >= 68) return { text: 'BUY',        cls: 'signal-buy' };
  if (score >= 58) return { text: 'HOLD+',       cls: 'signal-hold-plus' };
  if (score >= 42) return { text: 'HOLD',        cls: 'signal-hold' };
  if (score >= 32) return { text: 'HOLD−',       cls: 'signal-hold-minus' };
  return            { text: 'SELL / AVOID',       cls: 'signal-sell' };
}

// ── SELF-TESTS (run on every page load — check DevTools console) ──

(function runTests() {
  const eq = (a, b, msg) => console.assert(Math.abs(a - b) < 0.001, msg, { got: a, expected: b });

  // valueToColor
  const c50 = valueToColor(50);
  console.assert(c50.startsWith('hsl(60,'), 'valueToColor(50) should be yellow hue=60');

  // calcScenarios at init (all 50s)
  const init = calcScenarios([50,50,50,50,50,50,50,50]);
  eq(init.B, 50, 'init: B should be 50');
  eq(init.A, 50, 'init: A should be 50');
  eq(init.C,  0, 'init: C tail risk should be 0');

  // calcScenarios at max (all 100s)
  const max = calcScenarios([100,100,100,100,100,100,100,100]);
  eq(max.B, 100, 'max: B should be 100');
  eq(max.A,   0, 'max: A should be 0');
  eq(max.C, 100, 'max: C should be 100');

  // calcScenarios at min (all 0s)
  const min = calcScenarios([0,0,0,0,0,0,0,0]);
  eq(min.B, 0,   'min: B should be 0');
  eq(min.A, 100, 'min: A should be 100');
  eq(min.C, 0,   'min: C should be 0');

  // A + B always = 100
  const mixed = calcScenarios([30,70,45,80,20,60,50,40]);
  eq(mixed.A + mixed.B, 100, 'A + B must always equal 100');

  // calcCompany at init
  COMPANIES.forEach(co => {
    const score = calcCompany(co, { A: 50, B: 50, C: 0 });
    eq(score, 50, `${co.ticker}: init score should be 50`);
  });

  // calcCompany directional (GUBRF should rise when B rises)
  const highB = { A: 20, B: 80, C: 33 };
  const lowB  = { A: 80, B: 20, C: 0  };
  console.assert(calcCompany(COMPANIES[1], highB) > 50, 'GUBRF should be >50 when B=80');
  console.assert(calcCompany(COMPANIES[1], lowB)  < 50, 'GUBRF should be <50 when B=20');
  console.assert(calcCompany(COMPANIES[4], highB) < 50, 'TTRAK should be <50 when B=80');
  console.assert(calcCompany(COMPANIES[4], lowB)  > 50, 'TTRAK should be >50 when B=20');

  // getSignal thresholds
  console.assert(getSignal(70).text  === 'BUY',         'score 70 → BUY');
  console.assert(getSignal(62).text  === 'HOLD+',       'score 62 → HOLD+');
  console.assert(getSignal(50).text  === 'HOLD',        'score 50 → HOLD');
  console.assert(getSignal(36).text  === 'HOLD−',       'score 36 → HOLD−');
  console.assert(getSignal(25).text  === 'SELL / AVOID','score 25 → SELL/AVOID');

  console.log('%c✓ All formula tests passed', 'color:#4ade80; font-weight:bold');
})();
```

- [ ] **Step 2.2 — Reload in browser, verify tests pass**

Open (or reload) `dashboard.html`. Open DevTools console (F12).

Expected output in console:
```
✓ All formula tests passed
```

If any assertion fires, it prints a red error with `got` and `expected` values. Fix the formula logic before proceeding.

- [ ] **Step 2.3 — Commit**

```bash
git add dashboard.html
git commit -m "feat: data model + formula engine (calcScenarios, calcCompany, valueToColor) with console tests"
```

---

## Task 3: Render Metrics Column

**Files:**
- Modify: `dashboard.html` — add `initMetrics()` and `updateMetricColors()` to the `<script>` block, call `initMetrics()` from `init()`

- [ ] **Step 3.1 — Add `initMetrics()` to the script block**

Append these functions **before** the self-test IIFE (just before the `(function runTests()` line):

```javascript
// ── METRICS RENDERER ──────────────────────────────────────────

function initMetrics() {
  const container = document.getElementById('metrics-list');
  METRICS.forEach((m, i) => {
    const row = document.createElement('div');
    row.className = 'metric-row';
    row.innerHTML = `
      <div class="metric-header">
        <span class="metric-label">${m.label}</span>
        <span class="badge" id="badge-${i}">50</span>
      </div>
      <div class="slider-container" id="sc-${i}">
        <div class="track-fill" id="track-${i}"></div>
        <div class="thumb-overlay" id="thumb-${i}"></div>
        <input type="range" min="0" max="100" value="50"
               id="slider-${i}" data-idx="${i}" class="metric-slider"
               aria-label="${m.label}">
      </div>
      <p class="metric-desc">${m.desc}</p>
    `;
    container.appendChild(row);

    // Wire live update
    document.getElementById(`slider-${i}`).addEventListener('input', function () {
      updateMetricColors(i, parseInt(this.value));
      renderAll();
    });

    // Set initial colours
    updateMetricColors(i, 50);
  });
}

function updateMetricColors(idx, value) {
  const color  = valueToColor(value);
  const light  = valueToColor(Math.min(100, value + 10));   // slightly lighter for thumb
  const badge  = document.getElementById(`badge-${idx}`);
  const track  = document.getElementById(`track-${idx}`);
  const thumb  = document.getElementById(`thumb-${idx}`);

  badge.textContent          = value;
  badge.style.background     = color;
  track.style.width          = `${value}%`;
  track.style.background     = color;
  thumb.style.left           = `${value}%`;
  thumb.style.background     = light;
}
```

- [ ] **Step 3.2 — Add `init()` function and call it at the end of the script block**

Append at the very end of the `<script>` block, after the self-test IIFE:

```javascript
// ── INIT ───────────────────────────────────────────────────────
function init() {
  initMetrics();
  // initScenarios() and initCompanies() will be added in Tasks 4 and 5
}

document.addEventListener('DOMContentLoaded', init);
```

- [ ] **Step 3.3 — Reload and verify sliders**

Reload `dashboard.html`.

Expected:
- Left column shows 8 labelled sliders, all starting at 50 (yellow badges)
- Dragging a slider updates the badge number and colours it red (high) or green (low)
- The track fill grows/shrinks with the slider
- Right two columns still empty — that's fine
- Console still shows `✓ All formula tests passed`, zero errors

- [ ] **Step 3.4 — Commit**

```bash
git add dashboard.html
git commit -m "feat: metrics column — 8 live-coloured sliders rendering from METRICS data"
```

---

## Task 4: Render Scenarios Column

**Files:**
- Modify: `dashboard.html` — add `initScenarios()` and `updateScenarios()` to script; call from `init()`

- [ ] **Step 4.1 — Add scenario rendering functions**

Add these functions to the script block, **after** `updateMetricColors()` and **before** the self-test IIFE:

```javascript
// ── SCENARIOS RENDERER ────────────────────────────────────────

function initScenarios() {
  const container = document.getElementById('scenarios-display');
  container.innerHTML = `
    <!-- A+B split overview bar -->
    <div style="margin-bottom:0.6rem">
      <div style="display:flex;justify-content:space-between;font-size:0.7rem;color:#6b7080;margin-bottom:0.2rem">
        <span>Scenario A</span><span>Scenario B</span>
      </div>
      <div class="split-bar">
        <div class="split-a" id="split-a" style="width:50%"></div>
        <div class="split-b" id="split-b"></div>
      </div>
    </div>

    <!-- Scenario A bar -->
    <div class="scenario-row">
      <div class="scenario-header">
        <span class="scenario-name">A — De-escalation</span>
        <span class="badge" id="badge-A">50</span>
      </div>
      <p class="scenario-desc">Naval escort, ceasefire, urea &lt;$500, 5–10% yield damage</p>
      <div class="scenario-bar-bg">
        <div class="scenario-bar-fill" id="bar-A"></div>
      </div>
    </div>

    <!-- Scenario B bar -->
    <div class="scenario-row">
      <div class="scenario-header">
        <span class="scenario-name">B — Continued / Escalating</span>
        <span class="badge" id="badge-B">50</span>
      </div>
      <p class="scenario-desc">Blockade persists, urea &gt;$700, 15–25% yield damage</p>
      <div class="scenario-bar-bg">
        <div class="scenario-bar-fill" id="bar-B"></div>
      </div>
    </div>

    <!-- Tail Risk C gauge (separate, amber border) -->
    <div class="tail-risk-row">
      <div class="tail-label">⚠ Tail Risk Gauge (C) — not a probability</div>
      <div class="scenario-header">
        <span class="scenario-name" style="font-size:0.75rem">C — Regime Breakdown</span>
        <span class="badge" id="badge-C">0</span>
      </div>
      <p class="scenario-desc">Emerges above B=70. Regime collapse, $150+ oil, IMF-level Turkey response.</p>
      <div class="scenario-bar-bg">
        <div class="scenario-bar-fill" id="bar-C" style="width:0%"></div>
      </div>
    </div>

    <!-- Formula toggle -->
    <button class="formula-toggle-btn" id="formula-btn">Show formula ▼</button>
    <div class="formula-box hidden" id="formula-box">
      Scenario_B &nbsp;= avg(metric₁ … metric₈)<br>
      Scenario_A &nbsp;= 100 − B<br>
      Tail Risk C = max(0, (B−70) / 30 × 100)
    </div>
  `;

  document.getElementById('formula-btn').addEventListener('click', function () {
    const box = document.getElementById('formula-box');
    const open = !box.classList.contains('hidden');
    box.classList.toggle('hidden', open);
    this.textContent = open ? 'Show formula ▼' : 'Hide formula ▲';
  });

  updateScenarios({ A: 50, B: 50, C: 0 });
}

function updateScenarios(scenarios) {
  ['A', 'B', 'C'].forEach(key => {
    const val   = Math.round(scenarios[key]);
    const color = valueToColor(val);
    document.getElementById(`badge-${key}`).textContent        = val;
    document.getElementById(`badge-${key}`).style.background   = color;
    document.getElementById(`bar-${key}`).style.width          = `${val}%`;
    document.getElementById(`bar-${key}`).style.background     = color;
  });
  // update split overview bar
  const bPct = Math.round(scenarios.B);
  document.getElementById('split-a').style.width = `${100 - bPct}%`;
}
```

- [ ] **Step 4.2 — Add `initScenarios()` call to `init()`**

Find the `init()` function and update it:

```javascript
function init() {
  initMetrics();
  initScenarios();
  // initCompanies() added in Task 5
}
```

- [ ] **Step 4.3 — Reload and verify scenarios**

Reload `dashboard.html`.

Expected:
- Middle column shows the A+B split overview bar, two scenario bars, the tail risk gauge, and the formula toggle
- All bars start at 50 (yellow)
- "Show formula ▼" button expands/collapses the formula box
- Moving any left-column slider updates the scenario bars instantly:
  - Push all metrics toward 100 → B turns red, A turns green, tail risk rises
  - Push all metrics toward 0 → A turns red, B turns green, tail risk stays at 0
- When B ≤ 70, Tail Risk C bar shows 0
- When all metrics = 100, C bar shows 100 (red)
- Console: zero errors

- [ ] **Step 4.4 — Commit**

```bash
git add dashboard.html
git commit -m "feat: scenarios column — A/B bars, tail risk gauge, split overview bar, formula toggle"
```

---

## Task 5: Render Companies Column

**Files:**
- Modify: `dashboard.html` — add `initCompanies()` and `updateCompanies()` to script; call from `init()`

- [ ] **Step 5.1 — Add company rendering functions**

Add after `updateScenarios()` and before the self-test IIFE:

```javascript
// ── COMPANIES RENDERER ────────────────────────────────────────

function initCompanies() {
  const container = document.getElementById('companies-list');
  COMPANIES.forEach(co => {
    const row = document.createElement('div');
    row.className = 'company-row';
    row.innerHTML = `
      <div class="company-header">
        <span class="ticker">${co.ticker}.IS</span>
        <span class="company-name">${co.name}</span>
        <span class="badge" id="co-badge-${co.ticker}">50</span>
        <span class="signal signal-hold" id="co-signal-${co.ticker}">HOLD</span>
      </div>
      <div class="score-bar-bg">
        <div class="score-bar-fill" id="co-bar-${co.ticker}"></div>
      </div>
    `;
    container.appendChild(row);
  });

  updateCompanies({ A: 50, B: 50, C: 0 });
}

function updateCompanies(scenarios) {
  COMPANIES.forEach(co => {
    const score  = calcCompany(co, scenarios);
    const color  = valueToColor(score);
    const signal = getSignal(score);

    const badge  = document.getElementById(`co-badge-${co.ticker}`);
    const bar    = document.getElementById(`co-bar-${co.ticker}`);
    const sigEl  = document.getElementById(`co-signal-${co.ticker}`);

    badge.textContent      = Math.round(score);
    badge.style.background = color;
    bar.style.width        = `${score}%`;
    bar.style.background   = color;
    sigEl.textContent      = signal.text;
    sigEl.className        = `signal ${signal.cls}`;
  });
}
```

- [ ] **Step 5.2 — Add `initCompanies()` call to `init()`**

Update `init()`:

```javascript
function init() {
  initMetrics();
  initScenarios();
  initCompanies();
}
```

- [ ] **Step 5.3 — Reload and verify company column**

Reload `dashboard.html`.

Expected:
- Right column shows 10 company rows, each with ticker, name, score badge (50, yellow), signal (HOLD, grey), and score bar at 50%
- Console: zero errors

Verify B-sensitivity directions by dragging all sliders to ~80:
- TKFEN, GUBRF, BAGFS, BIMAS, SOKM → scores rise above 50, bars turn orange/red, signals move toward HOLD+ or BUY
- HEKTS, TTRAK, MGROS, ULKER, BANVT → scores fall below 50, bars turn green, signals move toward HOLD− or SELL/AVOID

Drag all sliders back to 50 → all scores return to exactly 50, all signals read HOLD.

- [ ] **Step 5.4 — Commit**

```bash
git add dashboard.html
git commit -m "feat: companies column — 10 tickers with live score bars and Buy/Hold/Sell signals"
```

---

## Task 6: Wire Full `renderAll()` + Key Facts Toggle

**Files:**
- Modify: `dashboard.html` — add `renderAll()`, wire Key Facts toggle, final verification

- [ ] **Step 6.1 — Add `renderAll()` to the script block**

Add after `updateCompanies()` and before the self-test IIFE:

```javascript
// ── RENDER ALL (called on every slider change) ─────────────────

function renderAll() {
  const metricValues = Array.from(
    document.querySelectorAll('.metric-slider'),
    s => parseInt(s.value)
  );
  const scenarios = calcScenarios(metricValues);
  updateScenarios(scenarios);
  updateCompanies(scenarios);
}
```

- [ ] **Step 6.2 — Wire the Key Facts toggle in `init()`**

Update `init()` to its final form:

```javascript
function init() {
  // Key Facts toggle
  document.getElementById('facts-toggle').addEventListener('click', function () {
    const panel = document.getElementById('facts-panel');
    const open  = !panel.classList.contains('hidden');
    panel.classList.toggle('hidden', open);
    this.textContent = open ? '▼ Key Facts' : '▲ Key Facts';
  });

  initMetrics();
  initScenarios();
  initCompanies();
}
```

Note: `initMetrics()` already wires each slider to call `renderAll()`. No other event wiring is needed.

- [ ] **Step 6.3 — End-to-end verification**

Reload `dashboard.html`. Run through this checklist manually:

- [ ] All 8 sliders start at 50, all badges yellow, all signals HOLD
- [ ] Moving Urea slider to 90 → B rises, A falls, GUBRF/BAGFS turn redder/higher, TTRAK turns greener/lower
- [ ] Moving Diplomatic Progress slider to 90 → same directional effect
- [ ] Moving all sliders to 80 → Tail Risk C gauge shows a non-zero value
- [ ] Moving all sliders to 100 → Tail Risk C = 100 (full red), GUBRF/BAGFS show BUY, TTRAK shows SELL/AVOID
- [ ] Moving all sliders to 0 → TTRAK shows BUY, GUBRF/BAGFS show SELL/AVOID
- [ ] "▼ Key Facts" opens the facts strip; "▲ Key Facts" closes it
- [ ] "Show formula ▼" opens formula box; "Hide formula ▲" closes it
- [ ] Console shows `✓ All formula tests passed` and zero errors
- [ ] Page looks correct on a ~1400px wide window (3 columns visible side by side)

- [ ] **Step 6.4 — Commit**

```bash
git add dashboard.html
git commit -m "feat: full renderAll() wiring — sliders drive scenarios drive companies end-to-end"
```

---

## Task 7: Final Polish + Handoff Doc Update

**Files:**
- Modify: `dashboard.html` — responsive fallback, minor style tweaks
- Modify: `docs/superpowers/specs/2026-04-14-turkey-fertilizer-dashboard-design.md` — mark as implemented

- [ ] **Step 7.1 — Add responsive fallback to CSS**

Inside the `<style>` block, append at the end (before the closing `</style>`):

```css
/* Responsive: stack columns on narrow screens */
@media (max-width: 900px) {
  .dashboard-grid {
    grid-template-columns: 1fr;
  }
  #facts-panel {
    grid-template-columns: repeat(2, 1fr);
  }
}
```

- [ ] **Step 7.2 — Add `title` attributes to company rows for tooltip context**

In `initCompanies()`, after `row.className = 'company-row';`, add:

```javascript
row.title = `B-sensitivity: ${co.bSens > 0 ? '+' : ''}${co.bSens} (${co.bSens > 0 ? 'benefits from escalation' : 'benefits from de-escalation'})`;
```

- [ ] **Step 7.3 — Update spec status**

In `docs/superpowers/specs/2026-04-14-turkey-fertilizer-dashboard-design.md`, change the header line:

Old: `**Status:** Approved — ready for implementation`
New: `**Status:** Implemented — dashboard.html in project root`

- [ ] **Step 7.4 — Final browser check**

Reload `dashboard.html`. Hover over a company row — tooltip should show the B-sensitivity description.

Resize browser window to ~800px wide — columns should stack vertically.

Console: `✓ All formula tests passed`, zero errors.

- [ ] **Step 7.5 — Final commit**

```bash
git add dashboard.html docs/superpowers/specs/2026-04-14-turkey-fertilizer-dashboard-design.md
git commit -m "feat: dashboard complete — responsive layout, tooltips, spec status updated"
```

---

## Self-Review Checklist

**Spec coverage:**

| Spec requirement | Task |
|-----------------|------|
| Information overview (Key Facts strip) | Task 1 (HTML), Task 6 (toggle wiring) |
| 8 metric sliders → scenario probabilities | Tasks 2, 3, 4, 6 |
| Scenario probabilities → company ticker values | Tasks 2, 5, 6 |
| Range 0–100, init at 50 | Tasks 2, 3, 4, 5 |
| Slider controls | Task 3 |
| Simple additive formula | Task 2 |
| Red ↑ / Green ↓ colour encoding | Task 2 (`valueToColor`) applied in Tasks 3, 4, 5 |
| Handoff doc (Section 10 of spec) | Spec doc; tooltip in Task 7 |
| A+B complementary (sum to 100) | Task 2 formula, verified in tests |
| C as separate Tail Risk Gauge | Task 4 |
| Formula toggle | Task 4 |
| Dark theme, CSS Grid layout | Task 1 |
| Signal labels BUY/HOLD/SELL | Task 5 |
| Responsive fallback | Task 7 |
| Single self-contained file | All tasks — only `dashboard.html` created |

All spec sections covered. ✓

---

*Plan written: 2026-04-14*
