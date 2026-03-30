# Claude Design Runbook

Here's what the runbook contains and how to use it:
Drop into any repo and fill in three things before starting:

design-criteria.md — the scoring rubric. The template is inside the runbook. The only part you fill in is the "Site Context" block at the top (URL, audience, differentiator, what to avoid). The four criteria themselves are repo-agnostic.
CLAUDE.md append — a scoped "Design Improvement Mode" section that tells Claude how to run the loop without interfering with your normal dev instructions.
The harness bootstrap prompt — the Step 4 prompt has brackets for stack, local URL, template paths, and CSS location. Fill those in once and paste into Claude Code.

A few design decisions in the runbook worth noting:

The evaluator is explicitly told to use Playwright to navigate the live site before scoring — not just read code. This is what the Anthropic article identifies as the key unlock for catching things that look fine in templates but feel wrong in the browser.
The scoring threshold (7/10 for Design Quality and Originality) forces real pivots, not just tweaks.
The resume prompt at the end of Step 5 makes it easy to pick up across sessions without losing context.
