# Work conventions to recommend

A teammate enforces conventions; it cannot invent them for a team. When the audit finds
none written down, propose this starter set, let the team edit it, then attach the agreed
version to the Skills that apply it. Frame them as the team's rules, not the teammate's —
people follow conventions they chose.

Organise them by the three Cs (creation, collaboration, communication) plus a fourth set
that only exists once agents join the team.

## Creation — how work enters Asana

- **One home per task type.** Write down which project owns which kind of task (e.g. page
  work in the website backlog, content pieces in the content calendar, committed work on
  the sprint board). Multi-homing is fine; say which project is canonical for *status*.
- **Sections mean one thing per project.** Either pages/areas, or stages, or status — not a
  mix. Two "Done" sections is a smell.
- **Titles: verb + object + where.** `Add proposal CTA to /contact form` beats
  `contact form`. Optional time-box prefix: `[15min]`, `[1h]`.
- **A task has one owner.** Unassigned is a note, not a task. Shared work is split into
  subtasks.
- **Dates or sprint.** Anything committed has a due date or a sprint; ideas live in an
  "Ideas" section with no date, and are reviewed or archived every quarter.
- **Templates for recurring task types** (page request, bug, content piece) so the
  definition of ready is built in.

## Collaboration — how work moves

- **Definition of ready** per lane (see `work-lanes.md`) — written, short, linked from the
  project description.
- **Subtasks for every action** someone else owns; one subtask per action; the parent stays
  open until they are closed.
- **Blocked means blocked by something named.** Use dependencies or a "Blocked" section
  with the blocker linked — never a bare "blocked" status.
- **Custom fields from the library**, not per-project lookalikes (one `Priority`, one
  `Estimated time`), so reports and teammates can read across projects.
- **Archive, don't hoard.** Ideas untouched for a year are archived or re-justified.

## Communication — how people talk about work

- **Comments are for the person who has to act**, read on a phone: what this is → needed
  from @Name (each line linking its subtask) → risks.
- **Decisions are recorded where the work is** (a comment marked `Decision:` or a decision
  log task), not only in meetings or chat.
- **Status lives in Asana**, chat is for quick coordination; link the task when a chat
  thread decides something.
- **Acknowledge with a like**, answer with a comment, never with silence.

## Agent conventions — when AI teammates and agents join

- **Every task has a lane** (Human / Agent / Teammate) — field, tag or title prefix, one
  agreed method.
- **Agents never close a task they cannot verify.** They comment a summary and create
  verification subtasks for the human who can.
- **Teammate edits are visible.** It comments what it changed and why; silent bulk edits
  are not allowed.
- **Approval-required actions stay approval-required** even when it would be faster:
  Asana's own gates (assigning someone without access to the task, deleting tasks it didn't
  create, adding tasks to projects where it isn't an editor, changing collaborators) plus
  whatever your policy adds.
- **One owner for each teammate** who reviews its memory monthly and owns its guidance and
  Skills versions.
- **Feedback goes in the task**, not to the builder in private — so the teammate (and its
  memory) learns from it.

## Rolling them out

Conventions stick when they are a project, not a document: one task per convention in a
"Work conventions" project, an owner who reviews them every 2–3 months, and a teammate Skill
that politely points to the convention when it is broken ("This task has no owner — our
convention is one owner per task. Who should take it?").
