# Discovery interview — question bank

Principles (why the interview works this way):

- **Data first.** Read the projects and docs before asking anything. Cite what you saw in
  the question. The user's attention is the scarcest resource in the build.
- **One open question at a time.** Multiple open questions in one message get one half-answer
  each. Multiple-choice questions can be batched (2–4) with an options tool.
- **Push once on vague answers.** "The team", "faster", "better visibility" are not answers.
  Ask for a name, a number, a recent example. Then accept what you get and move on.
- **Recommend.** For every multiple-choice question, put your recommended option first with
  a one-line reason. The user is hiring you for judgment, not a menu.
- **Harvest, don't scope-creep.** Good ideas beyond the first job go on the roadmap
  ("future Skills / responsibilities") in the spec. Say so out loud so the user knows they
  were heard.

## Core five (exit gate for Phase 1)

1. **Who** — "Who will assign work to this teammate, and who reads what it produces? Names
   and roles." Push: a team is not a person; get at least one named primary user.
2. **Today** — "Walk me through the last time this job was done. Who did it, how long did
   it take, what got dropped?" Push: ask for a specific recent instance.
3. **Desired** — "If the teammate does this perfectly for a month, what is different?"
   Push: convert adjectives into observable states ("every sprint candidate has an owner and
   an estimate by Tuesday").
4. **Why now** — "What made this worth setting up this month?" (Reveals the real priority
   and the stakes; a teammate with no why-now usually gets abandoned.)
5. **Done** — "How will you know in two weeks that it works?" These become eval bars.

## Shape questions (multiple choice, batch them)

**First job** — "Which single job do we build, test and baseline first?" Offer 3–4 jobs
drawn from the interview and the audit; recommend the one that (a) recurs, (b) has a
measurable before/after, (c) fixes a gap the audit found. All other jobs go to the roadmap.

**Authority** — "How much may it change on its own?"
- Read & recommend (comments and reports only; humans change everything).
- Edit with guardrails (recommended for most): may create subtasks, fill fields, move within
  agreed sections, comment; assigning people, deleting, moving across projects need approval.
- Full PM: assigns, dates, moves to sprints, closes stale items. Only with clean conventions
  and a tested baseline.

**Lanes** — "Is there an agent that works outside Asana (Claude Code, Cowork, n8n, other)?
Which kinds of task should be prepared for it rather than for a person?"

**Data sources** — "Which projects and documents are the source of truth?" Offer the ones
found in Phase 0 (backlog, sprint board, content calendar, process docs) as multi-select.
Ask where process docs live; if it is a wiki the teammate cannot read, plan attachments.

**Conventions** — "Does the team have written Asana conventions (naming, where tasks go,
definition of ready, comment style)?" If no: offer to propose them
(`work-conventions.md`) as part of the build. If yes: they become a Skill attachment.

**Cadence** — "When does the team plan and review?" (sprint length, planning day, recurring
syncs). Triggers and recurring tasks hang off this.

## Deeper probes (use when the answers so far are thin)

- "What does a task look like when it is *not* ready? Show me one." (Gets the definition of
  ready from a concrete example faster than asking for the definition.)
- "Which decisions does only you make?" (Feeds the 👤 lane and the escalation rules.)
- "What should this teammate never do, even if asked?" (Feeds do-not-touch.)
- "Who will be annoyed if the teammate comments on their tasks?" (Feeds sharing, tone and
  whether to start read-only.)
- "If it gets one thing wrong, which wrong thing is expensive?" (Feeds the decoys and the
  heaviest-weighted health-score category.)
- "Which existing rules, forms or templates already handle part of this?" (Avoids redoing
  what Asana already does.)
