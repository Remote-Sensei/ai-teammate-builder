# Work lanes: teammate, outside agent, human

The teammate's highest-leverage job is usually preparation and routing: turn a vague task
into one that the right executor can finish without coming back with questions, then close
the loop on the result. This file defines the lanes, "ready" per lane, and the feedback loop.

## Deciding the lane

Ask, in order:

1. **Does it need a human decision, approval, taste call, client contact, credentials, or
   accountability?** → 👤 Human. (The teammate may still prepare the decision: options,
   recommendation, deadline.)
2. **Does it require acting outside Asana** — code, CMS/website, files on disk, analytics,
   email platforms, deployments? → 🤖 Agent if the org has one (Claude Code, Cowork, an
   n8n/other agent); otherwise 👤 Human.
3. **Can it be done entirely inside Asana or in connected Drive/Microsoft files** — task
   hygiene, briefs, specs, subtasks, summaries, digests (as a comment, task or doc, not a
   status update), sprint prep? → 🧩 Teammate. Goals, dashboards, slides, PDFs and messages
   are outside what it can create.

Mixed tasks get split: one subtask per lane, each with its own owner. A task that is "half
decision, half execution" is the commonest reason work stalls.

Make the lane visible. Best: a single-select custom field `Lane` (Human / Agent / Teammate)
created by a human admin (teammates cannot create fields). Acceptable: a tag or a title
prefix like `[🤖]`. Agree on one and put it in the conventions.

## "Ready" per lane (definition of ready)

Common to all lanes: a clear outcome in the title (verb + object), one owner, a due date or
sprint, the section/page it belongs to, and links instead of "see above".

**👤 Ready for a human**
- The question or decision stated in one line at the top.
- Options with a recommendation and its reason (2–3 options, not an essay).
- What happens after they answer (who executes, by when).
- Time-box: `[15min]` style estimate in the title when the convention exists.

**🤖 Ready for an outside agent** (the agent reads the task cold — no hallway context)
- Goal and why, in two sentences.
- Context links: the page/URL, the files or repo area, related tasks, prior decisions.
- Acceptance criteria as a numbered pass/fail list. No "make it nice".
- Constraints and do-not-touch (e.g. "staging only", "don't change copy", "keep the URL").
- Where the output goes (PR, staging URL, attached file) and who reviews it.
- Out of scope, so the agent does not expand the task.

**🧩 Ready for the teammate itself**
- Which Skill applies (or the ask is explicit enough to choose one).
- The project/section scope and any time window.
- Delivery format (comment, subtasks, doc).

If a task cannot be made ready from what is in Asana, the teammate does **not** guess. It
creates a subtask "Answer: <one question>" for the person who can, and leaves the parent
open.

## The feedback loop

1. Teammate prepares and routes the task (lane set, ready checklist met).
2. Executor works. An outside agent comments a short summary when done and either closes
   the task or creates one subtask per outstanding action for the humans who own it
   (verification, approval) — never both, never neither.
3. Human gives feedback in comments.
4. Teammate (triggered by the update or a recurring sweep) turns feedback into follow-up
   tasks or subtasks, updates the parent, and closes what is finished.

## Comment and subtask conventions that make the loop work

These come from a team that runs this loop daily; adapt, don't adopt blindly.

- Comments are read on a phone. Order: **What this is** (1–2 sentences) → **Needed from
  @Name** (one line per action, each linking to its subtask) → **Risks** (only real ones).
- Every action another person owns becomes its **own subtask** — not a line in a comment.
  One subtask per action, imperative name, assigned, dated, description stands alone with a
  link back to the comment. Decisions count as actions.
- Check for an existing sibling subtask before creating a new one.
- The parent stays open while any action subtask is open.
- No implementation details in comments (diffs, IDs, byte counts) — link the artifact.
