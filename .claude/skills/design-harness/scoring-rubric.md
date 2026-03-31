# Scoring Rubric

Detailed evaluation criteria for the design improvement harness.
These criteria are repo-agnostic and must not be changed per project.

---

## 1. Design Quality (HIGH WEIGHT — score /10)

Does the design feel like a coherent whole with a distinct identity —
not a collection of parts? Colors, typography, layout, and imagery should
combine into a recognizable mood. Ask: would someone screenshot this and
share it as an example of good design?

Generic = automatic fail. Museum quality = the target.

**Score guide:**
- 1-3: No visual identity. Looks like unstyled HTML or a default template.
- 4-5: Has styling but feels assembled, not designed. No distinct mood.
- 6: Competent but unremarkable. Would not stand out in a lineup.
- 7: Clear identity emerging. Cohesive palette and type choices.
- 8: Distinctive. Someone would notice this site in a portfolio review.
- 9: Excellent. Coherent mood across every element. Feels intentional.
- 10: Museum quality. Would be cited as a reference for good design.

---

## 2. Originality (HIGH WEIGHT — score /10)

Evidence of deliberate, custom creative choices. A human designer should
recognize intentional decisions, not defaults.

**Penalize immediately:**
- Purple or blue gradients over white cards
- Neutral gray card grids
- Numbered service lists (01 02 03 04)
- Default Tailwind utility patterns used without customization
- Generic sans-serif fonts: Inter, Roboto, Arial, system-ui
- Hero layout: text left, image right, CTA button below
- Anything a Bootstrap or Tailwind starter theme produces unmodified

**Award points for:**
- Unexpected layout logic: asymmetry, overlap, grid-breaking elements
- A font pairing with genuine personality
- Visual details that reward closer inspection
- A color palette that is limited and intentional, not "whatever works"
- Something that would make a designer stop scrolling

**Score guide:**
- 1-3: Pure defaults. Could be any template. Zero custom decisions.
- 4-5: Some customization but still recognizable as a common pattern.
- 6: Custom choices exist but don't add up to a distinct voice.
- 7: Clearly intentional decisions. Breaks away from template norms.
- 8: Surprising choices that work. A designer would recognize craft.
- 9: Highly original. Distinctive approach that feels owned.
- 10: Would be featured in a design gallery. Unmistakably custom.

---

## 3. Craft (score /10)

Technical execution of the design fundamentals:

- **Typography hierarchy**: clear, intentional type scale with personality
- **Spacing**: consistent rhythm, not arbitrary padding values
- **Color**: limited palette applied with discipline
- **Contrast**: ratios that meet WCAG AA minimums
- **Responsive**: behavior that preserves the aesthetic on mobile

**Score guide:**
- 1-3: Broken fundamentals. Inconsistent spacing, poor contrast, no hierarchy.
- 4-5: Basic competence. Nothing broken but nothing refined.
- 6: Solid fundamentals. Consistent spacing and clear hierarchy.
- 7: Good craft. Typography scale feels intentional, color is disciplined.
- 8: Strong execution. Details are polished, responsive works well.
- 9: Excellent. Every detail feels considered and refined.
- 10: Flawless execution. Production-ready, accessible, polished.

---

## 4. Functionality (score /10)

Can a first-time visitor answer these in under 5 seconds:
- Who is this person or company?
- What do they offer?
- What should I do next?

Can they navigate, find work samples or key content, and contact without
hunting?

**Score guide:**
- 1-3: Confusing. Visitor cannot determine purpose or navigate.
- 4-5: Purpose is unclear or navigation requires hunting.
- 6: Basic clarity. Purpose is stated, navigation works.
- 7: Clear and functional. Visitor knows what to do immediately.
- 8: Smooth experience. Clear hierarchy of actions and content.
- 9: Excellent flow. Visitor guided naturally through key content.
- 10: Effortless. Perfect clarity, zero friction, delightful to use.

---

## Scoring Thresholds

| Criterion | Threshold | Action if below |
|---|---|---|
| Design Quality | 7/10 | Mandatory revision or full aesthetic pivot |
| Originality | 7/10 | Mandatory revision or full aesthetic pivot |
| Craft | 6/10 | Fix fundamentals before continuing |
| Functionality | 6/10 | Stop aesthetics work, fix usability first |

**Do not just tweak.** If Design Quality or Originality fall below threshold,
make a real strategic change — different fonts, different palette, different
layout logic — not a minor adjustment to what is already there.
