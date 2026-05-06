---
topic: semiconductors
zoom_level: region
date: 2026-04-13
status: active
tags: [semiconductors, helium, neon, chips, AI, domain-analysis]
sources_count: 6
---

# Semiconductors

> **Zoom Level:** Region (Level 1)
> **Upstream in cascade:** [[01_OIL_AND_ENERGY]] → THIS (via helium, neon, energy costs)
> **Also connected to:** [[07_PETROCHEMICALS_AND_PLASTICS]] (neon from petrochemical refining), [[06_ALUMINUM_AND_METALS]] (shared energy dependency)

---

## Why Semiconductors Are Hit

This is not an obvious link — semiconductors don't "use oil." But the crisis exposes a **hidden dependency chain** through specialty gases and energy:

```
Hormuz closure
    │
    ├─→ Qatar helium production halted (Ras Laffan struck)
    │       └─→ Helium supply -34% globally
    │               └─→ Chip fab cooling, lithography, plasma processes
    │
    ├─→ Qatar neon exports blocked (~98% of exports)
    │       └─→ Neon for EUV/DUV lithography
    │               └─→ Advanced chip production constrained
    │
    ├─→ LNG shortage → electricity rationing in East Asia
    │       └─→ Power-hungry fabs face curtailment
    │
    └─→ Oil price → South Korea energy crisis (70% Middle East crude)
            └─→ Samsung + SK Hynix operations threatened
```

---

## Critical Input: Helium

- **Qatar produces ~34% of global helium** — all exported via Hormuz
- Helium is used in chip fabrication: lithography cooling, plasma etching, cleanroom environments
- **No viable at-scale substitute** exists for ultra-pure helium in semiconductor processes
- Prices for ultra-pure helium have **doubled** since the crisis began
- Russia (alternative source) unreliable since 2021 facility fire + Ukraine war disruptions

---

## Critical Input: Neon

- Neon is essential for **excimer lasers** used in DUV and EUV lithography
- Qatar dominates neon exports (~98%)
- Previously, Ukraine supplied ~50% of global neon (disrupted in 2022) — industry diversified partly to Qatar
- The 2022 neon scare led to stockpiling, but stockpiles are **finite** (estimated months, not years)

---

## Most Exposed Companies and Regions

| Actor | Exposure | Why |
|-------|----------|-----|
| **South Korea** | Critical | 70% crude from ME; Samsung + SK Hynix = 80% global HBM, 70% DRAM |
| **Taiwan (TSMC)** | High | Energy imports, specialty gas supply |
| **Samsung** | Critical | South Korea energy + helium dependency |
| **SK Hynix** | Critical | HBM for AI — no alternative suppliers at scale |
| **Intel (US fabs)** | Moderate | Less direct ME energy dependency, but helium/neon global |

---

## Downstream Impact

If chip production is curtailed:
- **AI hardware:** HBM and advanced GPUs already supply-constrained → further bottleneck
- **Consumer electronics:** Smartphones, laptops, appliances
- **Automotive:** Modern vehicles require 1,000-3,000+ chips each
- **Defense systems:** Military hardware depends on advanced chips
- **Medical devices:** Imaging, monitoring equipment

---

## The "Previously Invisible" Vulnerability

This crisis revealed what Carnegie called a category of vulnerability **never incorporated into semiconductor supply chain stress tests**: critical, non-substitutable process inputs concentrated in a small number of countries, transiting a single chokepoint.

Before 2026, semiconductor risk planning focused on:
- Geopolitical risk (Taiwan/China)
- Fab concentration
- Equipment bottlenecks (ASML)

It did **not** adequately stress-test:
- Specialty gas supply routes
- Energy supply to fab-hosting countries
- Maritime chokepoint dependencies for process inputs

---

## Open Questions

- `[OPEN QUESTION]` How many months of helium/neon stockpile do major fabs hold?
- `[OPEN QUESTION]` Can US/EU helium production (from natural gas wells) scale to compensate?
- `[OPEN QUESTION]` Are fabs implementing gas recycling/conservation measures?
- `[OPEN QUESTION]` What is the lead time to bring alternative helium sources online?

---

## Sources

1. [Carnegie — The Iran war is also a semiconductor problem](https://carnegieendowment.org/emissary/2026/03/iran-korea-semiconductor-chips-energy-oil-hormuz)
2. [Tom's Hardware — Global chip supply chain under threat](https://www.tomshardware.com/tech-industry/global-chip-supply-chain-under-threat-as-us-iran-conflict-enters-third-week-strait-of-hormuz-blockade-is-days-away-from-crippling-taiwans-semiconductor-industry)
3. [Carra Globe — Semiconductor supply chain disruption 2026](https://carraglobe.com/semiconductor-supply-chain-disruption-2026/)
4. [The Diplomat — The gas inside your AI chip](https://thediplomat.com/2026/04/the-gas-inside-your-ai-chip/)
5. [Al Habtoor Research — Implications for global semiconductor industry](https://www.habtoorresearch.com/programmes/hormuz-closure-global-semiconductor/)
6. [Sourceability — Geopolitics reshaping semiconductor supply chain](https://sourceability.com/post/geopolitics-are-reshaping-semiconductor-supply-chain-risk-in-2026)

---

*Last updated: 2026-04-13 — Session 001*
