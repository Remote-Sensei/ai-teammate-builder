# Publishing a teammate kit

Goal: someone at another company can rebuild a comparable teammate on *their* data in an
afternoon, and trusts it because they can see how it was tested.

## What goes in the kit

```
README.md            what it does, who it is for, prerequisites, setup in steps, what it never does
readiness-checklist.md   the audit checks a reader runs on their own workspace first
behavior-guidance.md     with [placeholders]
skills/*.md              Asana-format Skills, ready for "Create skill → Upload Markdown"
conventions.md           the conventions the teammate enforces (editable)
evals.md                 seed-task patterns, decoys, bars, how to score
CHANGELOG.md             versions and what changed
```

Mapping from a Build kit: `attachments/` conventions → `conventions.md`; `evals/` →
`evals.md`; `_working/readiness-audit.md` → `readiness-checklist.md` with your numbers
removed and the checks kept.

## Generalise without gutting it

- Remove: people's names, emails, gids, private URLs, internal project names, client names,
  revenue numbers, anything from a memory or comment thread. Keep links to public sources.
- Replace company specifics with `[placeholders]` and a one-line hint:
  `[Sprint board project — where committed 2-week work lives]`.
- Keep the worked example's *shape* (sections, fields, cadence) as an illustration labelled
  "example — replace with yours". Concrete beats abstract for readers.
- Keep the readiness checklist and evals — they are what separates a kit from a prompt.
- Say what was tested (how many seed tasks, health score, plan tier) and what was not.

## Forum post shape (community forums, e.g. Asana Forum)

Write it as a practitioner sharing a method, not a launch. Structure:

1. The problem in one or two lines, from experience ("our teammate's auto-generated
   instructions were six generic lines…").
2. What you built and the core idea (prepare-and-route across human / agent / teammate).
3. The process in brief (the ten phases as a short list).
4. What worked, what didn't, the numbers you have.
5. The kit (attachment or link) and how to use it in 3 steps.
6. One honest open question to invite replies.

Edit the post into the author's own voice before publishing, and get explicit approval
before posting anywhere public.
