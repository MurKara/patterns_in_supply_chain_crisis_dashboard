---
topic: index
type: navigation
date: 2026-04-13
status: active
tags: [index, navigation, master]
---

# Oil Crisis Knowledge Base — Master Index

> **Purpose:** This is the entry point for every session. Any LLM agent should read this file FIRST before doing anything else. It maps the entire wiki, tracks what exists, what's missing, and where to go next.

---

## How to Use This Wiki

1. **Start here.** Read this INDEX.md fully.
2. **Read [[SESSION_GUIDE]]** for protocols on how to work in this wiki.
3. **Check [[LOG]]** for the latest session entries and what was done last.
4. **Navigate by domain** using the map below.
5. **After every session**, update this index and append to the log.

---

## Wiki Architecture

```
oilCrisis/
├── INDEX.md                          ← YOU ARE HERE (master navigation)
├── SESSION_GUIDE.md                  ← Protocol for any LLM to pick up work
├── LOG.md                            ← Chronological session log
├── CLAUDE.md                         ← Personal operating manual (do not modify)
├── claude_Wiki_Guide.md              ← Wiki pattern reference (read for methodology)
│
├── CRISIS_PATTERN_FRAMEWORK.md       ← Reusable template for analyzing any crisis
│
├── 00_OVERVIEW.md                    ← Satellite view: the 2026 Hormuz crisis
├── 01_OIL_AND_ENERGY.md              ← Oil, LNG, energy markets
├── 02_FERTILIZER_AND_AGRICULTURE.md  ← Fertilizer supply → food production chain
├── 03_FOOD_SECURITY.md               ← Hunger, food prices, vulnerable countries
├── 04_SEMICONDUCTORS.md              ← Helium, neon, chip fabrication
├── 05_TEXTILES.md                    ← Polyester, synthetic fibers, apparel
├── 06_ALUMINUM_AND_METALS.md         ← Aluminum, metals, industrial materials
├── 07_PETROCHEMICALS_AND_PLASTICS.md ← Feedstocks, plastics, packaging
├── 08_SHIPPING_AND_TRADE.md          ← Freight, insurance, trade routes
├── 09_HISTORICAL_PATTERNS.md         ← 1973, 1979, 2022, 2026 comparison
│
├── ENTITIES.md                       ← Key actors: countries, orgs, companies
├── OPEN_QUESTIONS.md                 ← Parked questions for future sessions
└── raw/                              ← (future) clipped articles, PDFs, source docs
```

---

## Page Catalog

| # | Page | Summary | Status | Links To |
|---|------|---------|--------|----------|
| — | [[SESSION_GUIDE]] | Protocol for any LLM to continue work | active | INDEX, LOG |
| — | [[LOG]] | Chronological session history | active | all pages |
| — | [[CRISIS_PATTERN_FRAMEWORK]] | Reusable crisis analysis template | active | all domain pages |
| 00 | [[00_OVERVIEW]] | Satellite view of the 2026 Hormuz crisis | active | all domain pages |
| 01 | [[01_OIL_AND_ENERGY]] | Crude oil, LNG, energy rationing | active | 02, 04, 05, 07, 08 |
| 02 | [[02_FERTILIZER_AND_AGRICULTURE]] | Fertilizer disruption → crop impact | active | 01, 03, 07 |
| 03 | [[03_FOOD_SECURITY]] | Global hunger risk, vulnerable nations | active | 02, 08 |
| 04 | [[04_SEMICONDUCTORS]] | Helium/neon shortage → chip fabs | active | 01, 06, 07 |
| 05 | [[05_TEXTILES]] | Polyester/synthetic fiber price shock | active | 01, 07 |
| 06 | [[06_ALUMINUM_AND_METALS]] | Aluminum smelter disruption | active | 01, 04, 08 |
| 07 | [[07_PETROCHEMICALS_AND_PLASTICS]] | Feedstocks, naphtha, methanol, PE | active | 01, 02, 04, 05 |
| 08 | [[08_SHIPPING_AND_TRADE]] | Freight, insurance, trade rerouting | active | all domain pages |
| 09 | [[09_HISTORICAL_PATTERNS]] | Crisis comparison: 1973, 1979, 2026 | active | 00, CRISIS_PATTERN_FRAMEWORK |
| 10 | [[10_TURKEY_EXPOSURE]] | Turkey compound exposure — 7 sectors, 16 companies, probabilities | active | 01, 02, 05, 06, 07, 08, ENTITIES |
| 11 | [[11_TURKEY_FERTILIZER_DEEP_DIVE]] | **Street-level deep dive**: scenarios, company Buy/Sell/Hold signals, watchlist | active | 02, 03, 10, ENTITIES |
| 12 | [[12_RARE_EARTH_MATERIALS]] | Rare earths, critical minerals, China dominance, Iran reserves, sulfur shock | active | 01, 04, 06, 08, ENTITIES |
| — | [[ENTITIES]] | Countries, orgs, companies (incl. Turkish companies table) | active | all domain pages |
| — | [[OPEN_QUESTIONS]] | Parked research questions | active | — |

---

## Cascade Map (How Domains Connect)

```
STRAIT OF HORMUZ CLOSURE (chokepoint event)
    │
    ├─→ [[01_OIL_AND_ENERGY]]         Crude oil + LNG blocked
    │       │
    │       ├─→ [[07_PETROCHEMICALS_AND_PLASTICS]]   Feedstock shortage
    │       │       ├─→ [[05_TEXTILES]]               Polyester/nylon costs
    │       │       ├─→ [[02_FERTILIZER_AND_AGRICULTURE]]  Nitrogen/urea shortage
    │       │       │       └─→ [[03_FOOD_SECURITY]]       Hunger + food prices
    │       │       └─→ [[04_SEMICONDUCTORS]]          Neon for lithography
    │       │
    │       ├─→ [[06_ALUMINUM_AND_METALS]]   Energy-intensive smelting
    │       │       └─→ Aerospace, automotive, construction
    │       │
    │       ├─→ [[04_SEMICONDUCTORS]]        Helium for chip cooling
    │       │       └─→ AI hardware, consumer electronics, defense
    │       │
    │       └─→ [[12_RARE_EARTH_MATERIALS]]  Sulfur supply (refining byproduct)
    │               ├─→ Nickel/cobalt refining halted (battery supply)
    │               └─→ Iran REE reserves inaccessible (supply diversification blocked)
    │
    └─→ [[08_SHIPPING_AND_TRADE]]      Insurance, freight, rerouting
            └─→ ALL sectors (cost multiplier)

TURKEY-SPECIFIC CASCADE:
    [[10_TURKEY_EXPOSURE]] synthesizes all of the above for Turkey:
    TÜPRAŞ (refining) → TRY depreciation → fertilizer/food crisis
    Kirkuk–Ceyhan pipeline → partial mitigation → corridor opportunity
```

---

## Research Zoom Level Tracker

| Domain | Current Level | Next Target |
|--------|--------------|-------------|
| Oil & Energy | Level 1 (Region) | Level 2 — specific supply/demand data |
| Fertilizer & Agriculture | Level 1 (Region) | Level 2 — country-specific planting seasons |
| Food Security | Level 1 (Region) | Level 2 — WFP/FAO scenario modeling |
| Semiconductors | Level 1 (Region) | Level 2 — fab-level helium dependency |
| Textiles | Level 1 (Region) | Level 2 — brand/retailer exposure |
| Aluminum & Metals | Level 1 (Region) | Level 2 — smelter recovery timelines |
| Petrochemicals | Level 1 (Region) | Level 2 — substitution pathways |
| Shipping & Trade | Level 1 (Region) | Level 2 — alternative route analysis |
| Historical Patterns | Level 1 (Region) | Level 2 — quantitative comparison |
| **Rare Earth Materials** | **Level 1 (Region)** | **Level 2 — China monopoly timeline, alternative sourcing rates** |
| **Turkey Exposure** | **Level 2 (City)** | **Level 3 — company-level monitoring, CBRT response** |
| **Turkey Fertilizer (Street)** | **Level 3 (Street)** | Weekly watchlist dashboard, scenario re-scoring |

---

*Last updated: 2026-04-30 — Session 004*
