---
topic: crisis-pattern-framework
zoom_level: satellite
date: 2026-04-13
status: active
tags: [framework, pattern, reusable, checklist, decision-tree]
sources_count: 0
---

# Crisis Pattern Framework

> **Purpose:** A reusable checklist and decision tree for analyzing ANY supply chain crisis. Built from patterns observed in the [[09_HISTORICAL_PATTERNS|2026 Hormuz crisis and historical precedents]].
> **Goal:** When a new crisis hits, work through this framework to quickly identify affected domains and cascade paths.

---

## Step 1: Identify the Disruption Type

| Type | Examples | Key Question |
|------|----------|-------------|
| **Chokepoint closure** | Hormuz 2026, Suez 1967/2021, Bab el-Mandeb 2024 | What % of global trade flows through it? |
| **Production shutdown** | Iran revolution 1979, Libya 2011 | What % of global supply is removed? |
| **Sanctions/embargo** | Arab embargo 1973, Russia 2022 | Who is sanctioned? Who enforces? |
| **Infrastructure damage** | Pipeline attacks, refinery strikes | How long to repair? Substitutable? |
| **Financial disruption** | Insurance withdrawal, currency crisis | Can goods flow physically but not financially? |
| **Pandemic/natural disaster** | COVID 2020, Fukushima 2011 | What labor/logistics are disrupted? |

---

## Step 2: Map the Primary Commodity Flows

For the identified chokepoint/disruption, list ALL commodities affected:

```
Disruption: ________________

Commodities blocked/disrupted:
□ Crude oil          — % of global flow: ___
□ LNG/natural gas    — % of global flow: ___
□ Fertilizers        — % of global flow: ___
□ Petrochemicals     — % of global flow: ___
□ Metals (specify)   — % of global flow: ___
□ Specialty gases    — % of global flow: ___
□ Food/grain         — % of global flow: ___
□ Other: ________    — % of global flow: ___
```

**Rule of thumb:** If >10% of global flow is disrupted for any commodity, expect significant price impact within days.

---

## Step 3: Trace the Cascade Chains

For each blocked commodity, trace downstream:

### Energy cascade
```
Oil/gas disruption
├─→ Energy prices (electricity, heating, transport fuel)
│   ├─→ Energy-intensive manufacturing (aluminum, steel, cement, glass)
│   ├─→ Agriculture (diesel, irrigation, drying)
│   ├─→ Cold chain / logistics
│   └─→ Residential (heating, cooling — political pressure)
│
└─→ Feedstock supply (oil/gas as raw material, not fuel)
    ├─→ Petrochemicals → plastics → packaging, medical, textiles
    ├─→ Fertilizers → agriculture → food prices → hunger
    └─→ Specialty chemicals → semiconductors, pharmaceuticals
```

### Shipping cascade
```
Maritime disruption
├─→ Insurance costs spike → financial blockade
├─→ Freight rates spike → all traded goods more expensive
├─→ Vessel rerouting → longer transit → delays
├─→ Port congestion → cascading delays
└─→ Air freight substitution → air rates spike
```

### Financial cascade
```
Price spike / uncertainty
├─→ Currency pressure (import-dependent countries)
├─→ Central bank response (rates, reserves)
├─→ Corporate distress (thin-margin industries)
├─→ Consumer inflation → demand destruction
└─→ Government fiscal pressure (subsidies, bailouts)
```

---

## Step 4: Identify the Amplifiers

Check each amplifier — these make any crisis worse:

| Amplifier | Check | 2026 Hormuz Status |
|-----------|-------|--------------------|
| **Timing:** Does it coincide with a critical season? | □ | YES — spring planting |
| **Concentration:** Is supply concentrated in few sources? | □ | YES — Qatar helium 34% |
| **Substitutability:** Can inputs be replaced? | □ | NO — helium has no substitute |
| **Stockpile:** Are buffers adequate? | □ | PARTIAL — SPR exists for oil, not for helium |
| **Infrastructure damage:** Is capacity physically destroyed? | □ | YES — smelters frozen |
| **Insurance withdrawal:** Is trade financially blocked? | □ | YES — 100x premium increase |
| **Concurrent crises:** Are other disruptions happening? | □ | YES — Guinea bauxite restrictions |
| **Debt stress:** Are affected countries already in fiscal trouble? | □ | YES — several developing nations |

---

## Step 5: Map Regional Vulnerability

For each affected region, assess:

| Region | Energy Import Dependency | Commodity Exposure | Fiscal Buffer | Food Import Dependency | Industrial Exposure |
|--------|------------------------|-------------------|---------------|----------------------|-------------------|
| ______ | High / Medium / Low | List key commodities | Strong / Weak | High / Medium / Low | List key sectors |

**Most vulnerable profile:** High energy import dependency + high food import dependency + weak fiscal buffer + energy-intensive industry.

---

## Step 6: Timeline and Recovery Assessment

| Phase | Duration | What Happens |
|-------|----------|-------------|
| **Acute (0-30 days)** | Weeks | Price spikes, panic buying, insurance withdrawal, stockpile drawdown |
| **Adjustment (1-6 months)** | Months | Rerouting, demand destruction, rationing, government intervention |
| **Structural (6-24 months)** | Quarters | New supply sources, infrastructure investment, policy changes |
| **Post-crisis (2-5 years)** | Years | Diversification, new trade patterns, technology shifts |

**Key question for each phase:** What breaks if the crisis lasts this long?

---

## Step 7: Non-Obvious Connections Checklist

These are the dependencies that are invisible until a crisis reveals them (lessons from 2026):

- [ ] Does the disrupted region supply **specialty gases** (helium, neon, argon)?
- [ ] Are there **energy-intensive industries** in the region (smelting, refining)?
- [ ] Does the disruption affect **fertilizer inputs** (natural gas → ammonia → urea)?
- [ ] Are there **single-exit maritime routes** for key exporters?
- [ ] Do downstream countries have **electricity rationing risk**?
- [ ] Are there **concurrent supply restrictions** in related commodities?
- [ ] Does the disruption coincide with **planting/harvest seasons**?
- [ ] Are **medical supply chains** dependent on affected petrochemicals?
- [ ] Does the disruption affect **AI/tech supply chains** (HBM, GPUs via energy or gases)?
- [ ] What **recycling/secondary production** exists as buffer?

---

## Step 8: Document and Monitor

After completing the framework:

1. Create a domain page for each significantly affected sector
2. Add to [[INDEX]] with cascade links
3. List open questions in [[OPEN_QUESTIONS]]
4. Set review dates — when should we re-assess?
5. Track: Which predictions were correct? Which were wrong? (Feedback loop)

---

## Template: Quick Crisis Assessment Card

```markdown
## Crisis Assessment: [Name]
**Date:** YYYY-MM-DD
**Type:** Chokepoint / Production / Sanctions / Infrastructure / Financial / Natural
**Trigger:** [What happened]

### Supply Impact
- Commodity 1: X% of global flow disrupted
- Commodity 2: Y% of global flow disrupted

### Cascade Chains Identified
1. [Commodity] → [Sector 1] → [Sector 2] → [End impact]
2. ...

### Amplifiers Active
- [ ] Critical timing
- [ ] Supply concentration
- [ ] No substitutes
- [ ] Infrastructure damage
- [ ] Insurance/financial blockade

### Most Vulnerable
- Countries: ...
- Sectors: ...
- Populations: ...

### Timeline Estimate
- Acute: [weeks]
- Recovery: [months/years]

### Open Questions
- ...
```

---

*Last updated: 2026-04-13 — Session 001*
