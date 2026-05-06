---
topic: session-guide
type: protocol
date: 2026-04-13
status: active
tags: [meta, protocol, guide]
---

# Session Guide — How to Work in This Wiki

> **Audience:** Any LLM agent (Claude, GPT, Codex, etc.) picking up work in this knowledge base.
> **Read this after [[INDEX]].**

---

## 1. Session Startup Checklist

Every session begins with these steps, in order:

1. **Read [[INDEX]]** — understand the wiki structure and what exists
2. **Read [[LOG]]** — check what was done in the last session
3. **Read [[OPEN_QUESTIONS]]** — see what's parked and unresolved
4. **Ask the user:** "What would you like to focus on today?" or propose a priority from the open questions
5. **Set the zoom level** — are we at Satellite, Region, City, or Street?

---

## 2. File Conventions

### Frontmatter (required on all wiki pages)
```yaml
---
topic: descriptive-name
zoom_level: satellite | region | city | street
date: YYYY-MM-DD
status: draft | active | stale | archived
tags: [tag1, tag2]
sources_count: N
---
```

### Cross-linking
- Use `[[wiki-link]]` syntax for Obsidian compatibility
- Every page should link to at least 2 other pages
- When mentioning an entity (country, company, org), link to [[ENTITIES]]
- When referencing a cascade chain, link to [[CRISIS_PATTERN_FRAMEWORK]]

### Source Citations
- Inline: `[Source Title](URL)` with brief description
- Each page tracks its own `sources_count` in frontmatter
- When adding a new source, also update the page's source list at the bottom

### Tagging Conventions
Use these standard tags across all pages:
- Domain: `oil`, `lng`, `fertilizer`, `agriculture`, `food-security`, `semiconductors`, `textiles`, `aluminum`, `metals`, `petrochemicals`, `plastics`, `shipping`, `trade`
- Type: `domain-analysis`, `entity`, `pattern`, `framework`, `comparison`, `timeline`
- Status flags: `verify` (unconfirmed claim), `stale` (needs update), `gap` (known missing info)

---

## 3. Operations

### INGEST (adding new information)
1. Read the new source
2. Discuss key takeaways with the user
3. Update relevant wiki pages (often 3-5 pages per source)
4. Update [[INDEX]] page catalog if structure changes
5. Append entry to [[LOG]]
6. Check: does this source answer any [[OPEN_QUESTIONS]]?

### QUERY (answering a question)
1. Read [[INDEX]] to find relevant pages
2. Read those pages
3. Synthesize an answer with `[[wiki-links]]` as citations
4. If the answer is substantial, file it as a new wiki page
5. If the question reveals gaps, add to [[OPEN_QUESTIONS]]

### LINT (health check)
Run periodically (every 3-5 sessions):
- [ ] Any orphan pages (no inbound links)?
- [ ] Any stale claims that newer sources contradict?
- [ ] Any pages missing sources?
- [ ] Any [[OPEN_QUESTIONS]] that can now be answered?
- [ ] Is [[INDEX]] up to date?
- [ ] Does [[ENTITIES]] cover all mentioned actors?
- [ ] Do cascade chains in [[CRISIS_PATTERN_FRAMEWORK]] reflect latest data?

---

## 4. Research Protocol (Satellite-to-Street)

```
Level 0 (Satellite) → What is the crisis? What domains are affected?
Level 1 (Region)    → How does each domain transmit the shock? Key mechanisms.
Level 2 (City)      → Specific data: trade volumes, price changes, timelines, actors.
Level 3 (Street)    → Actionable: monitoring dashboards, datasets, decision tools.
```

- Always label the current zoom level in your session
- Don't jump to Street without passing through Region and City
- When zooming in, note what you're NOT covering (park it)

---

## 5. ADD Support Protocol

The wiki owner has diagnosed ADD. Help them stay focused:

- **One domain per deep-dive.** Don't try to update everything at once.
- **If they drift:** Note `[CONTEXT SHIFT DETECTED]` and ask whether to park or pivot.
- **End every session with:**
  ```
  ## Session State
  - Completed: ...
  - Parked: ...
  - Next priority: ...
  ```
- **Decompose large tasks** into checkbox subtasks (max 5 per batch).
- **Challenge constructively:** "Is this the highest-leverage question right now?"

---

## 6. Pattern Recognition Goal

The ultimate purpose of this wiki is to build a **reusable crisis analysis framework**:

- When a new crisis hits (trade war, pandemic, conflict, natural disaster), the user wants to quickly identify which domains will cascade.
- The [[CRISIS_PATTERN_FRAMEWORK]] should evolve with each session into a checklist/decision tree.
- Cross-links between domain pages reveal the dependency graph.
- The Obsidian graph view visualizes these dependencies.

**Key question to keep asking:** "If [X] is disrupted, what breaks downstream?"

---

## 7. Quality Standards

- **No unsourced claims.** Mark uncertain items with `[VERIFY]`.
- **No walls of text.** Use tables, cascade diagrams, and bullet lists.
- **Every page earns its existence.** If a page has <3 meaningful facts, merge it.
- **Bias check:** Note when sources come from a single perspective (industry, government, NGO).

---

*Last updated: 2026-04-13 — Session 001*
