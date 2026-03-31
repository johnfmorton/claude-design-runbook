---
name: design-harness
description: Run a generator/evaluator design improvement loop on any website. Screenshots the live site, scores against design criteria, and iterates 5-15 rounds toward museum-quality design.
argument-hint: "[site-url] [local-dev-command] [local-url]"
disable-model-invocation: true
allowed-tools: Read, Write, Edit, Bash, Glob, Grep
---

# Design Improvement Harness

Run a structured generator/evaluator loop to push a website's visual design
past generic defaults toward something with real identity.

Based on Anthropic's [generator/evaluator pattern](https://www.anthropic.com/engineering/harness-design-long-running-apps).

## Environment Check

- Playwright installed: !`npx playwright --version 2>&1 || echo "NOT INSTALLED"`
- design-criteria.md exists: !`test -f design-criteria.md && echo "YES" || echo "NO"`
- design-log.md exists: !`test -f design-log.md && echo "YES" || echo "NO"`
- CLAUDE.md exists: !`test -f CLAUDE.md && echo "YES" || echo "NO"`
- CLAUDE.md has Design Mode: !`grep -c "Design Improvement Mode" CLAUDE.md 2>/dev/null || echo "0"`

## Arguments

If the user provided arguments: $ARGUMENTS

- `$0` = site URL (e.g., https://mysite.com)
- `$1` = local dev command (e.g., `npm run dev`)
- `$2` = local URL (e.g., http://localhost:3000)

If no arguments were provided, ask the user for:
1. The site URL or name
2. The stack (e.g., Next.js, Craft CMS + Twig, Laravel + Blade)
3. The local dev command and URL
4. Where templates and CSS live
5. What needs the most design work (top 2-3 concerns)

## Step 1 — Check Prerequisites

If Playwright is NOT INSTALLED (see environment check above):
- Stop and tell the user to install it:
  ```
  npm install -g playwright && npx playwright install chromium
  ```
- Do not proceed until Playwright is available.

## Step 2 — Scaffold Files

### design-criteria.md

If `design-criteria.md` does not exist:
1. Read the template at [design-criteria-template.md](design-criteria-template.md)
2. Create `design-criteria.md` in the project root using the template
3. If the user provided a site URL or context in their arguments, fill in
   what you can in the Site Context section
4. Ask the user to review and complete the Site Context section before
   continuing. The scoring criteria must not be changed.

If `design-criteria.md` already exists, read it and confirm the Site Context
section is filled in. If it has unfilled bracketed placeholders, ask the user
to complete them.

### design-log.md

If `design-log.md` does not exist, create it:

```markdown
# Design Log

Iteration history for the design improvement harness.
Each entry records the strategy, scores, and next move.
```

If it already exists, read it. You will resume from the last iteration.

### CLAUDE.md — Design Improvement Mode

Check if CLAUDE.md contains a "Design Improvement Mode" section.

If it does not, append the following to CLAUDE.md (create the file if it
does not exist). Use a horizontal rule to separate it from existing content:

```markdown

---

## Design Improvement Mode

When working on the visual design of this site, apply the following
process. This mode is activated when the task involves redesigning,
restyling, or improving the visual design of the site.

### Process
1. Read `design-criteria.md` before doing anything else
2. Start the dev server if it is not running
3. Use Playwright to screenshot and navigate the live site on
   localhost before scoring — do not score from code alone
4. Implement design changes
5. Score the result against all four criteria in `design-criteria.md`
6. Append the result to `design-log.md` using the log entry template
7. If Design Quality or Originality score below 7, either refine the
   current direction or make a full aesthetic pivot — do not just tweak
8. Repeat for a minimum of 5 iterations before declaring done

### Design Principles
- Typography first: choose fonts before touching layouts
- Color palette before components: define 3-4 colors and stick to them
- Bold maximalism and refined minimalism both work — the key is
  intentionality, not intensity
- The best designs are museum quality — hold the work to that standard
- Never converge on safe, "technically functional but visually
  unremarkable" outputs
```

## Step 3 — Read Criteria and Assess Current State

1. Read `design-criteria.md` in full
2. Read the scoring rubric at [scoring-rubric.md](scoring-rubric.md) for
   detailed penalty/reward guidance
3. Examine the current templates and CSS to understand the existing design
4. Start the dev server if it is not already running
5. Use Playwright to screenshot the live site so you can see it as a visitor would
6. If resuming (design-log.md has entries), summarize where the redesign
   stands and continue from the last iteration number

## Step 4 — Run the Generator/Evaluator Loop

Execute the following loop for a minimum of 5 iterations:

### Each Iteration

**Generate:**
1. Plan your design changes. Start with typography and color — these
   are the foundation. Then move to layout and component design.
2. Implement the changes in the template and CSS files.

**Evaluate:**
3. Use Playwright to screenshot the live site after changes.
4. Score the result against all four criteria in `design-criteria.md`.
   Use the detailed rubric in [scoring-rubric.md](scoring-rubric.md).
5. Write a candid critique. Be specific about what works and what doesn't.

**Log:**
6. Append the iteration to `design-log.md` using the format in
   [design-log-template.md](design-log-template.md).

**Decide:**
7. Apply the scoring thresholds:
   - Design Quality or Originality below **7/10** → mandatory revision
     or full aesthetic pivot (different fonts, palette, layout logic)
   - Craft below **6/10** → fix fundamentals before continuing
   - Functionality below **6/10** → stop aesthetics, fix usability first
   - **Do not just tweak.** If below threshold, make a real strategic change.
8. Record your next move (refine or pivot, and specifically why).

### Loop Control

- Do not ask for confirmation before each iteration. Work continuously.
- After iteration 5, report your current scores and ask the user whether
  to continue or stop.
- If all four scores are 8+ for two consecutive iterations, you may
  suggest stopping (but let the user decide).
- Maximum 15 iterations before stopping to check in.

## Tips for the User

If Claude gets stuck in small tweaks: say "the Originality score is stuck —
make a full aesthetic pivot, different fonts, different color palette,
different layout logic."

If the evaluator is too lenient: say "you are scoring too generously.
Re-read the Originality criteria and penalize anything that a Tailwind
template would produce by default."

If you want to lock in a direction and refine: say "the direction from
iteration N is the right one — stop pivoting and refine craft only."
