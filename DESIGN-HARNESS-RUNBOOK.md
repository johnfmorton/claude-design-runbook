# Design Harness Runbook
### A portable setup guide for running a Claude Code generator/evaluator redesign loop on any website repo

Drop this file into any site repo. Then follow the steps below to have Claude Code
scaffold the full harness and begin an iterative design improvement process.

---

## What This Does

This runbook sets up a **multi-agent design harness** based on Anthropic's
generator/evaluator pattern. Claude Code acts as both agents:

- **Generator** — implements design changes based on a brief and prior feedback
- **Evaluator** — navigates the live site, scores the result against defined
  criteria, and produces a written critique the generator uses next round

Each iteration either refines the current direction or pivots to a new aesthetic.
The loop runs 5–15 rounds. You end up with a design log, a final critique, and
a site that looks like it was made by someone with taste.

---

## Prerequisites

Before starting, confirm these are available on your machine:

```bash
# Claude Code
claude --version

# Node / npm (for Playwright)
node --version

# Playwright (the evaluator uses this to navigate the live site)
npm install -g playwright
npx playwright install chromium
```

Your site's local dev server must be runnable. Know the command and port before
you begin (e.g. `npm run dev` on port 3000, `php artisan serve` on 8000, etc.).

---

## Step 1 — Drop These Files Into Your Repo

You need three files in your project root:

1. `DESIGN-HARNESS-RUNBOOK.md` — this file (reference only)
2. `design-criteria.md` — the four scoring criteria (created in Step 2)
3. `design-log.md` — auto-maintained iteration log (created by Claude)

Optionally, you will append a section to your existing `CLAUDE.md` (Step 3).

---

## Step 2 — Create `design-criteria.md`

Create this file in your project root. Fill in the bracketed sections with
specifics about this site before starting your Claude Code session.

```markdown
# Design Evaluation Criteria

## Site Context
**Site:** [URL or name]  
**Owner/Brand:** [Who is this for, and what do they do?]  
**Audience:** [Who visits this site and why?]  
**Differentiator:** [What makes this person/brand genuinely different?
  Be specific. This is what the design should express.]  
**What to avoid:** [Any aesthetic directions that would be wrong for
  this brand — e.g., "don't go corporate," "avoid dark/moody," etc.]

---

## Scoring Criteria

### 1. Design Quality (HIGH WEIGHT — score /10)
Does the design feel like a coherent whole with a distinct identity —
not a collection of parts? Colors, typography, layout, and imagery
should combine into a recognizable mood. Ask: would someone screenshot
this and share it as an example of good design? Generic = automatic fail.

### 2. Originality (HIGH WEIGHT — score /10)
Evidence of deliberate, custom creative choices. A human designer
should recognize intentional decisions, not defaults.

**Penalize immediately:**
- Purple or blue gradients over white cards
- Neutral gray card grids
- Numbered service lists (01 02 03 04)
- Default Tailwind utility patterns with no customization
- Generic sans-serif fonts (Inter, Roboto, Arial, system fonts)
- Hero: text left, image right, button below
- Anything a bootstrap theme would produce without modification

**Award points for:**
- Unexpected layout logic (asymmetry, overlap, grid-breaking elements)
- A font pairing with genuine personality
- Visual details that reward closer inspection
- A color palette that is limited and intentional, not "whatever works"
- Something that would make a designer stop scrolling

### 3. Craft (score /10)
Technical execution of the design fundamentals:
- Typography hierarchy: clear, intentional type scale with personality
- Spacing: consistent rhythm, not arbitrary padding
- Color: limited palette, used with discipline
- Contrast ratios that meet accessibility minimums
- Responsive behavior that doesn't break the aesthetic on mobile

### 4. Functionality (score /10)
Can a first-time visitor answer these questions in under 5 seconds:
- Who is this person/company?
- What do they do or offer?
- What should I do next?
Can they navigate, find work samples or services, and contact without hunting?

---

## Scoring Threshold

- Design Quality or Originality below **7/10** = mandatory revision
- Do not just tweak — make a real strategic change or full aesthetic pivot
- Functionality below **6/10** = stop, fix usability before continuing aesthetics
```

---

## Step 3 — Update Your `CLAUDE.md`

**Do not replace your existing `CLAUDE.md`.** Append the following section to
the bottom of it. The horizontal rule and header keep it scoped so Claude only
applies design-critique thinking when explicitly working on design.

```markdown
---

## Design Improvement Mode

When working on the visual design of this site, apply the following
process. This mode is activated when the task involves redesigning,
restyling, or improving the visual design of the site.

### Process
1. Read `design-criteria.md` before doing anything else
2. Start the dev server if it is not running
3. Use Playwright MCP to screenshot and navigate the live site on
   localhost before scoring — do not score from code alone
4. Implement design changes
5. Score the result against all four criteria in `design-criteria.md`
6. Append the result to `design-log.md` using the template below
7. If Design Quality or Originality score below 7, either refine the
   current direction or make a full aesthetic pivot — do not just tweak
8. Repeat for a minimum of 5 iterations before declaring done

### Design Log Entry Template
Append to `design-log.md` after each iteration:

## Iteration N — [date]
**Strategy:** [What you changed and why. What aesthetic direction
  you are pursuing or pivoting to.]
**Design Quality:** X/10
**Originality:** X/10
**Craft:** X/10
**Functionality:** X/10
**Notes:** [Anything notable — what worked, what didn't, what a
  reviewer would likely flag]
**Next move:** [Refine or pivot — and specifically why]

### Design Principles
- Typography first: choose fonts before touching layouts
- Color palette before components: define 3–4 colors and stick to them
- Bold maximalism and refined minimalism both work — the key is
  intentionality, not intensity
- The best designs are museum quality — hold the work to that standard
- Never converge on safe, "technically functional but visually
  unremarkable" outputs
```

---

## Step 4 — Start Your Claude Code Session

Open your terminal in the project root and start Claude Code:

```bash
claude
```

Paste the following as your first message. Fill in the bracketed sections
before sending.

---

### The Harness Bootstrap Prompt

```
Read design-criteria.md in this project root before doing anything else.

I want to run a design improvement harness on this site. Here is the
context you need:

**Site:** [URL]
**Stack:** [e.g., Craft CMS + Twig, Laravel + Blade, Next.js, etc.]
**Local dev command:** [e.g., `ddev start`, `npm run dev`, `php artisan serve`]
**Local URL:** [e.g., http://localhost:3000 or https://mysite.ddev.site]
**Templates live at:** [e.g., `templates/`, `resources/views/`, `src/`]
**CSS lives at:** [e.g., `src/css/`, `resources/css/`]

**What needs the most work:**
[Paste your top 2–3 concerns — e.g., "typography is generic,"
"the services section looks like every other dev site," "no visual identity"]

**What the design should express about this brand:**
[Pull from the Site Context section of design-criteria.md and expand.
Be specific about what makes this person or brand different.]

Now do the following:

1. Examine the current templates and CSS to understand the existing
   design system
2. Use Playwright MCP to screenshot the live site at [LOCAL URL] so
   you can see it as a visitor would
3. Start with typography and color — these are the foundation
4. Work through at least 5 full iterations of the generator/evaluator
   loop, scoring each against design-criteria.md
5. After each iteration, append results to design-log.md
6. If Design Quality or Originality fall below 7, pivot — do not
   just make small adjustments
7. After iteration 5, tell me your current scores and ask whether to
   continue or stop

Do not ask for confirmation before starting each iteration. Work
continuously until you have completed 5 rounds or hit a blocker.
```

---

## Step 5 — After the Session

When Claude Code finishes or you end the session, you'll have:

- `design-log.md` — a full record of every iteration, score, and strategic
  decision. Review this to understand what changed and why.
- Modified templates/CSS reflecting the final design direction
- A clear sense of where to continue in the next session

To resume in a new session, start Claude Code and say:

```
Read design-criteria.md and design-log.md. Summarize where the
redesign stands, then continue from the last iteration.
```

---

## Tips

**If Claude gets stuck in small tweaks:** Say "the Originality score
is stuck — make a full aesthetic pivot, different fonts, different color
palette, different layout logic."

**If the evaluator is too lenient:** Say "you are scoring too generously.
Re-read the Originality criteria and penalize anything that a Tailwind
template would produce by default."

**If you want to lock in a direction and refine:** Say "the direction
from iteration N is the right one — stop pivoting and refine craft only."

**If the site uses a CMS:** Tell Claude which files control global
styles vs. per-template styles so it doesn't hunt. Include this in
your stack description in the harness bootstrap prompt.

**For Craft CMS specifically:** Tell Claude your CSS entry point
(usually a Vite config or a single compiled CSS file) and whether
you are using Tailwind, custom CSS, or both.

---

## File Checklist

Before starting a session, confirm:

- [ ] `design-criteria.md` exists and the Site Context section is filled in
- [ ] `CLAUDE.md` has the Design Improvement Mode section appended
- [ ] Local dev server starts cleanly
- [ ] You know the local URL and port
- [ ] Playwright is installed (`npx playwright --version`)

---

*Based on Anthropic's generator/evaluator harness pattern described in
[Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
and the [frontend-design skill](https://github.com/anthropics/claude-code/blob/main/plugins/frontend-design/skills/frontend-design/SKILL.md).*
