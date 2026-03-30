# Claude Design Runbook

A portable harness for running an AI-powered generator/evaluator redesign
loop on any website repo, using Claude Code in your terminal.

Based on Anthropic's [generator/evaluator pattern](https://www.anthropic.com/engineering/harness-design-long-running-apps)
for frontend design improvement.

---

## What This Is

Most AI-assisted design work produces safe, generic output — technically
functional but visually unremarkable. This runbook sets up a structured
loop where Claude Code acts as two agents:

- **Generator** — implements design changes based on a brief and prior feedback
- **Evaluator** — navigates the live site via Playwright, scores the result
  against defined criteria, and produces a written critique

Each iteration either refines the current direction or pivots to a new
aesthetic. The loop runs 5–15 rounds. The scoring threshold enforces real
creative decisions, not just tweaks.

---

## Prerequisites

These must be installed on your machine before using this runbook:

- [Claude Code](https://claude.ai/code) — `claude --version` to confirm
- Node.js — `node --version` to confirm
- Playwright — `npm install -g playwright && npx playwright install chromium`

Your site's local dev server must be runnable before starting a session.

---

## Repo Contents

```
claude-design-runbook/
├── README.md                      ← you are here
├── DESIGN-HARNESS-RUNBOOK.md      ← step-by-step process guide
├── design-criteria-template.md    ← copy this into your target repo and fill in
├── CHANGELOG.md                   ← version history of this process
└── examples/
    └── (design-log examples added after real runs)
```

---

## How To Use This On A New Project

1. Copy `DESIGN-HARNESS-RUNBOOK.md` into your site's project root
2. Copy `design-criteria-template.md` into your site's project root,
   rename it `design-criteria.md`, and fill in the Site Context section
3. Follow the steps in `DESIGN-HARNESS-RUNBOOK.md`

That's it. The runbook is self-contained from that point.

---

## How This Repo Evolves

After each real-world run, update this repo:

- Add the resulting `design-log.md` to `examples/` (scrubbed of any
  client details if needed)
- Update `CHANGELOG.md` with anything you learned about the process
- Refine the criteria template or runbook if a run exposed a gap

The process improves with use. Treat it as a living document.

---

## Background

This harness is based on Anthropic's engineering post
[Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
(March 2026), which describes using a GAN-inspired generator/evaluator
structure to push Claude past the generic defaults it gravitates toward
when working on frontend design.

The four scoring criteria (Design Quality, Originality, Craft, Functionality)
are adapted from that post. The Playwright-based live evaluation approach
is taken directly from it — scoring from code alone misses what scoring
from a running browser catches.
