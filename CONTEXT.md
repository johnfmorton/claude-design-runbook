# Project Context

## What This Repo Is
A portable harness for running a Claude Code generator/evaluator redesign
loop on any website repo. Based on Anthropic's engineering post:
https://www.anthropic.com/engineering/harness-design-long-running-apps

## First Target Site
johnfmorton.com — portfolio/consulting site for a full-stack developer
with an advertising creative director background (DDB, Bozell, Dentsu).

## Diagnosed Problems
- Typography is generic (likely Tailwind defaults)
- No clear visual identity
- Looks AI-assembled — card grids, numbered service lists, safe palette
- Design doesn't reflect the advertising/creative background

## What We've Built
All files in this repo. The process is documented in DESIGN-HARNESS-RUNBOOK.md.
The design-criteria-template.md should be copied into the target repo and
filled in before starting a session.

## Next Steps
1. Copy DESIGN-HARNESS-RUNBOOK.md into the johnfmorton.com repo
2. Copy design-criteria-template.md → design-criteria.md, fill in Site Context
3. Append Design Improvement Mode section to johnfmorton.com's CLAUDE.md
4. Run the harness bootstrap prompt from Step 4 of the runbook
```

Then in Claude Code:
```
read CONTEXT.md and all other .md files in this directory, then tell me
what you understand about this project and what we should do first.
