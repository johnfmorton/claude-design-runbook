# Project Context

## What This Repo Is
A portable harness for running a Claude Code generator/evaluator redesign
loop on any website repo. Based on Anthropic's engineering post:
https://www.anthropic.com/engineering/harness-design-long-running-apps

## How This Was Developed
This process was refined through real-world use on a portfolio site for a
developer with a creative director background. The diagnosed problems —
generic typography, no visual identity, AI-assembled look — are common
across developer and small-business sites. The harness was effective at
pushing past those defaults through structured iteration and hard scoring
thresholds.

The four scoring criteria, the Playwright-based live evaluation, and the
pivot-not-tweak threshold logic all came directly from that first run and
the Anthropic engineering post that inspired it.

## Design Decisions
- The criteria template is repo-agnostic by design. Only the Site Context
  section changes per project.
- The CLAUDE.md append approach was chosen so the harness doesn't replace
  a project's existing Claude Code instructions — it layers on top.
- The bootstrap prompt in Step 4 uses bracketed placeholders so it works
  with any stack or framework.
