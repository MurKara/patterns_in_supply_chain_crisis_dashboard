# Patterns in Supply Chain Crisis

> **Knowledge base** — supply chain crisis patterns under a 2026 Strait of Hormuz blockade scenario.
> Research wiki covering oil, fertilizer, food security, semiconductors, textiles, shipping, and Turkey-specific exposure.
> LLM-assisted research, auto-synced to GitHub.

---

## Quick Start (for any agent picking up this work)

1. Read [`INDEX.md`](INDEX.md) — master navigation map
2. Read [`SESSION_GUIDE.md`](SESSION_GUIDE.md) — protocol for continuing work
3. Read [`LOG.md`](LOG.md) — what was done last session
4. Check [`OPEN_QUESTIONS.md`](OPEN_QUESTIONS.md) — what needs research next

---

## Repository Structure

```
patterns-in-supply-chain-crisis/
├── INDEX.md                        ← Start here — master navigation
├── SESSION_GUIDE.md                ← Protocol for LLM agents to pick up work
├── LOG.md                          ← Chronological session log (append-only)
├── CLAUDE.md                       ← Personal operating manual
├── claude_Wiki_Guide.md            ← Wiki methodology reference
├── CRISIS_PATTERN_FRAMEWORK.md     ← Reusable crisis analysis template
├── ENTITIES.md                     ← Key actors, organizations, countries
├── OPEN_QUESTIONS.md               ← Open research questions
│
├── 00_OVERVIEW.md                  ← Satellite view: the 2026 Hormuz crisis
├── 01_OIL_AND_ENERGY.md
├── 02_FERTILIZER_AND_AGRICULTURE.md
├── 03_FOOD_SECURITY.md
├── 04_SEMICONDUCTORS.md
├── 05_TEXTILES.md
├── 06_ALUMINUM_AND_METALS.md
├── 07_PETROCHEMICALS_AND_PLASTICS.md
├── 08_SHIPPING_AND_TRADE.md
├── 09_HISTORICAL_PATTERNS.md
├── 10_TURKEY_EXPOSURE.md
├── 11_TURKEY_FERTILIZER_DEEP_DIVE.md
│
├── config.yaml                     ← Project config (repo name, metadata)
├── scripts/
│   ├── kb_push.py                  ← Commit + push changes to GitHub
│   └── create_github_repo.py       ← One-time repo creation script
└── docs/
    └── superpowers/                ← Extended reference material
```

---

## Automation: Push Changes to GitHub

After updating any KB file, push the changes with a structured commit:

```bash
# Auto-generate commit message from changed files
python scripts/kb_push.py

# Or provide a custom message
python scripts/kb_push.py "kb: added Turkey fertilizer deep-dive"

# Preview without committing
python scripts/kb_push.py --dry-run
```

### First-time Setup (new machine or new repo)

1. Create a GitHub Personal Access Token with **repo** scope
2. Create `.env` from `.env.example` and add your token
3. Run the repo creation script:
   ```bash
   python scripts/create_github_repo.py
   ```
4. Then push everything:
   ```bash
   python scripts/kb_push.py "kb: initial commit"
   ```

### Reusing in another KB project

Copy `scripts/kb_push.py` and `scripts/create_github_repo.py` into any git-initialized folder.
Update `config.yaml` with the new repo name and description, then follow the steps above.

---

## Research Scope

| Domain | Status | Key Files |
|---|---|---|
| Oil & Energy | Active | `01_OIL_AND_ENERGY.md` |
| Fertilizer & Agriculture | Active | `02_FERTILIZER_AND_AGRICULTURE.md` |
| Food Security | Active | `03_FOOD_SECURITY.md` |
| Semiconductors | Active | `04_SEMICONDUCTORS.md` |
| Textiles | Active | `05_TEXTILES.md` |
| Aluminum & Metals | Active | `06_ALUMINUM_AND_METALS.md` |
| Petrochemicals | Active | `07_PETROCHEMICALS_AND_PLASTICS.md` |
| Shipping & Trade | Active | `08_SHIPPING_AND_TRADE.md` |
| Historical Patterns | Active | `09_HISTORICAL_PATTERNS.md` |
| Turkey Exposure | Active | `10_TURKEY_EXPOSURE.md` |
| Turkey Fertilizer | Active | `11_TURKEY_FERTILIZER_DEEP_DIVE.md` |

---

*Maintained by M (MurKara) — auto-synced via `scripts/kb_push.py`*
