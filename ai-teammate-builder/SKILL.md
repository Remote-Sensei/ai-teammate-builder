---
name: ai-teammate-builder
description: Design, build, test and tune an Asana AI Teammate from a company's own data — interview, workspace readiness audit, behavior guidance, Asana-format Skill files (.md for "Create skill → Upload Markdown"), access and triggers, seed-task evals with a health score, and iteration. Also diagnoses and fixes a teammate that misbehaves. Use this whenever someone wants to create, set up, configure, improve, audit or troubleshoot an Asana AI Teammate or its Skills/behavior guidance/instructions, wants "an AI project manager / PM agent / coordinator in Asana", asks which Asana Skills to add to a teammate, wants to turn their process docs or an Asana project into an agent, or says their Asana teammate "does the wrong thing", even if they never say "AI Teammate". Also use it to decide which work an Asana teammate should do versus Claude Code (or another agent working outside Asana) versus a human. Not for Asana AI Studio rules/Smart workflows alone, and not for general Asana project setup with no agent involved.
---

# AI Teammate Builder

Build an Asana AI Teammate the way a good manager onboards a new hire: learn the job and the
data first, agree on the boundaries, write the playbook, give it the right access, test it on
real work, and coach it. The result should be a teammate people trust — not a paragraph of
instructions that sounds right and quietly does the wrong thing.

Two worked examples, both public teammates from aiteammates.directory (our directory). Use them as patterns,
not templates: the point of this process is that the teammate is built on *this* company's
data.
- `examples/convention-keeper/`: Build path. A good design taken through the process,
  showing the few changes that matter in real use (access as the hard limit, checks that live
  in Asana data rather than memory, propose mode, two Skills, seed tests).
- `examples/overdue-organizer-fix.md`: Fix path. One reply for a teammate that invents data
  it can't see.

## Pick the path first

Match the effort to the request. A person asking "how do I fix this?" wants a fix in one
reply, not a ten-phase project.

| Request | Path | What the user gets |
|---|---|---|
| "Build / set up / design a teammate", new or freshly created from Asana's wizard | **Build** — the ten phases below | the paste-ready kit (see Outputs) |
| "It does X wrong", "how do I fix", "why does it…" | **Fix** — see *Fix path* | one reply: diagnosis, paste-ready fix, 3–6 test prompts, what to check next |
| "Review / audit our teammate", "is this setup good?" | **Audit** — Phases 0, 2 and the Phase 5 rubric | a short scored review with the top fixes |

If a fix reveals the design is wrong at the root (no clear job, wrong access, no
conventions), say so and offer the Build path — don't silently switch.

## The core idea: three lanes of work

An Asana AI Teammate is strong inside Asana (reading the work graph, creating and editing
tasks, commenting) and in connected Google Drive / OneDrive files (reading them, drafting
Docs, Sheets and Office files). It cannot act anywhere else, and even inside Asana it can't
create goals, dashboards or custom fields, or send messages or status updates. Many
organisations also run an agent with wider reach — Claude Code, Cowork, an n8n agent — that
can edit code, a CMS, files and analytics. And some calls only a human can make.

So the teammate's most valuable job is usually **not doing the work itself**; it is getting
each task *ready* for whoever does it, routing it to the right lane, and closing the loop on
feedback:

| Lane | Who | Typical work |
|---|---|---|
| Teammate | the AI Teammate, inside Asana | triage, backlog hygiene, task specs, subtasks, sprint prep, briefs, meeting follow-ups, status digests |
| Agent | Claude Code / another agent with system access | code, CMS/website edits, file and data work, analytics pulls, anything outside Asana |
| Human | a named person | decisions, approvals, taste/design judgment, client contact, anything needing credentials or accountability |

Ask early whether the organisation has an outside-Asana agent. If not, the Agent lane
collapses into Human and the teammate prepares tasks for people only. Read
`references/work-lanes.md` before writing behavior guidance — it defines "ready" per lane
and the feedback loop.

## Before you start

- Read `references/asana-platform.md` once per session: what a teammate can and cannot do,
  its anatomy, triggers, access control and the Asana Skill format. Platform behaviour
  changes between releases, so when you rely on a platform fact in an output, word it as
  "documented as of <month year>" and, where it matters, add a test that would catch it being
  wrong. Never present an unverified platform claim as the basis of a diagnosis.
- Find out what tools you have. With an Asana connector/API you can read projects, sections,
  custom fields, tasks and the teammate's current guidance. The API does **not** expose which
  projects a teammate can access, its Skills or its memory — read those from the teammate's
  **Customize** tab if you have a browser, otherwise ask the user to paste or screenshot
  them. Never guess the data.
- Guidance, Skills, access and sharing are edited in the Asana UI. Hand the user paste-ready
  text, or fill the UI yourself if you drive a browser — and confirm before saving anything
  in their workspace.
- A teammate freshly created with Asana's wizard usually comes with generic, auto-written
  guidance (often over-fitted to whatever task was open at creation), no Skills and empty
  memory. Check what it actually has; then treat wizard guidance as a placeholder to replace,
  not as a design to critique line by line.

## Build path — the ten phases

Work through them in order. Each phase ends at a gate; when the user is in a hurry, offer
the short path inside a phase instead of skipping its gate. Track progress:

```
Teammate build progress:
- [ ] 0 Context & tools
- [ ] 1 Discovery interview          (gate: five answers concrete; core inputs in hand)
- [ ] 2 Readiness audit              (gate: blockers fixed or accepted)
- [ ] 3 Premises & alternatives      (gate: user picks a shape)
- [ ] 4 Design & write               (gate: user confirms "what did I get wrong?")
- [ ] 5 Quality review               (gate: ≥ 7/10 on every artifact; a failure ships as draft only)
- [ ] 6 Build in Asana               (gate: one batched setup approval; triggers stay off)
- [ ] 7 Evals                        (gate: preregistered; bars met before triggers go on)
- [ ] 8 Health score & baseline
- [ ] 9 Iterate, version, hand over
```

### 0 — Context & tools

Establish: workspace, the teammate (new or existing — get its URL), the projects and docs it
will draw on, who will use it, and which outside-Asana agent exists (if any). For an existing
teammate, read its name, description, guidance, Skills, access and memory, and say plainly
what you found ("six generic lines, no skills, access to one project, empty memory").

### 1 — Discovery interview

**Read the data before asking.** Pull the project(s): sections, custom fields, open tasks with
assignee/due/section, the project description and anything it links to. Then ask questions
that cite what you saw ("62 of 90 open tasks have no owner — who triages new work today?").
A question the data could answer wastes the user's attention.

Ask **one open question at a time**; batch multiple-choice ones (2–4 per round) when you have
an options tool, with your recommendation first. Push back once on vague answers. Full
question bank and reasoning: `references/interview.md`. The minimum set:

1. **Who** does this teammate serve? Named people and roles.
2. **Today** — what happens now, and what does it cost them?
3. **Desired** — what should be different, concretely?
4. **Why now** — what made this worth doing this month?
5. **Done** — how will we know it works? (becomes the eval bars)
6. **Lanes** — is there an outside-Asana agent? What may the teammate change on its own?
7. **Data** — which projects, docs and conventions are the source of truth?
8. **First job** — the single narrowest job to build, test and baseline first.

**Core inputs.** Most jobs depend on one company artifact the teammate must follow: the
onboarding checklist, the definition of ready, the routing table, the brand rules. Ask for it
explicitly. If it does not exist, say so and offer to draft one *with* the user. If you must
proceed without the user, draft it, label it `DRAFT — replace with yours` at the top, and make
"send me your real <artifact>" the first open question. Never present an invented company
process as theirs.

Gate: 1–5 concrete and core inputs in hand (or explicitly drafted). Record every other good
idea as a *future Skill or responsibility* on the roadmap, and say so — the user should hear
that it was kept.

### 2 — Workspace readiness audit

A teammate inherits the mess it is pointed at. Score each data source with the honesty rule:
what you could not check is UNVERIFIABLE with the reason, never "probably fine" — and if a
check is something the user can answer in ten seconds (e.g. what the Access tab shows), ask
instead of leaving it unverifiable. Checks, thresholds, API calls and report template:
`references/readiness-audit.md`.

Also check **what already exists**: rules, forms, templates and library Skills that already do
part of the job. Look for contradictions in the workspace itself — project descriptions or
process docs that point at an old board, two boards claiming the same role — because the
teammate will follow them.

For every trigger, find out **who it runs as** (assigner, rule owner, form creator or
submitter) and check that *that person* can also reach the projects and docs the job needs:
the teammate only sees what both of them can see.

Gate: READY / NEEDS WORK / BLOCKER per source. Data-quality blockers get fixed, become the
teammate's first job, or are explicitly accepted. Missing access, a missing required field or
a conflicting rule can't be accepted, only fixed; until then the kit is a draft. Missing
conventions are a finding; propose them from
`references/work-conventions.md`.

### 3 — Premises & alternatives

State 4–7 premises the design rests on and ask the user to agree or disagree with each ("the
sprint board is the source of truth for status"; "the teammate never assigns a person without
approval"). A disagreement loops back.

Offer 2–3 genuinely different shapes, always including a **minimal** and an **ideal** one,
with your recommendation and why:

- *Minimal*: one Skill (the first job), @mention + one recurring task, read-and-comment only.
- *Recommended*: the first-job Skill (plus one supporting Skill only if the job can't work
  without it), edit with guardrails, one recurring or rule trigger. Library Skills come after
  the baseline, one at a time.
- *Ideal*: the full role as Skills, form/rule intake, cross-project access, outside-agent
  handoff loop.

Every addition beyond the chosen shape is asked separately: Add now / Defer / Skip. A
recommendation is not an approval.

For any bulk change the teammate could make (cleanup, re-dating, re-sectioning), build in a
**propose / apply switch**: a single line in the guidance, `CHANGE MODE: propose`, under which
it lists the bulk changes it would make and makes none of them. The user flips it to `apply`
after reviewing a couple of runs. `apply` never widens authority: ask-first and never rules
still hold. It costs one line and makes the first week safe.

### 4 — Design & write

Keep the design decisions (purpose, users, lanes and authority, access, responsibilities →
Skills, triggers, escalation, out-of-scope, acceptance criteria, roadmap, decision log) in a
working spec — `assets/teammate-spec-template.md`. It is your source of truth so every
instruction traces to a decision; it is a working note, not something the user has to read.

**Split deterministic from judgment work.** Anything that must happen identically every time
— creating a fixed checklist, moving a task when a field changes, assigning by a fixed rule —
belongs in an Asana rule, form or task template where your plan supports it: it behaves the
same every run and costs no AI usage.
Give the teammate the parts a template can't do: choosing items by context, filling owners
and dates, checking for gaps and contradictions, drafting, chasing, summarising. Say this
split out loud in the README; some users will find a template alone solves half their problem.

Then write the deliverables:

- **Behavior guidance** (`assets/behavior-guidance-template.md`): always-on operating rules —
  who it works for, how it speaks, how it picks a lane, what it may change, when it stops and
  asks. Job procedures stay *out*; they belong in Skills, which load only when needed.
- **Skills** (`assets/asana-skill-template.md`), one per responsibility. Prefer an adapted
  library Skill when one fits; write custom Skills where company procedure matters.
- **Domain material the job needs.** A Skill is only as good as the artifacts it can use: the
  checklist itself, an access-request table per tool, message or agenda templates, a
  definition of ready, a routing table. Put them in attachments and reference them from the
  Skill. Process scaffolding without domain substance produces a teammate that is tidy and
  useless.

**Consistency pass.** Before review, check that authority rules agree across guidance, every
Skill and the README — who may be assigned, which fields it may set, what needs approval. A
Skill that permits what the guidance forbids is the most common defect.

Gate: show the guidance and the first-job Skill, and ask "What did I get wrong?".

### 5 — Quality review

Review every artifact as an outside reader who has never seen the company — ideally one
subagent with no conversation context reviewing all artifacts in a single pass; otherwise a
fresh pass of your own. Rubric: `references/quality-and-evals.md`. ≥ 7/10 on every criterion
passes.

Keep it to **one full review plus one targeted re-check**: fix everything the review found,
then re-score *only the criteria that failed*, on the changed passages. A second full review
mostly re-discovers wording nits and costs as much as the build. Most defects should never
reach the review: the consistency pass in Phase 4 catches the expensive class (a Skill
permitting what the guidance forbids).

If a criterion still fails after the re-check, the gate has **failed** for that artifact. Put
it at the very top of the README under **Before you use this**: `NOT READY — <artifact>:
<criterion>, <why>, <what fixes it>` (often a core input only the user has). Don't ship it as
ready, and don't keep looping. A failure on authority, access, platform capability or
consistency blocks Phase 6: the kit ships as a draft and nothing is installed or switched on.
If a fix changed who may do what, re-run the consistency pass, not only the failed line.
If everything passed, say so in one line at the top of the README ("All artifacts
passed review on <date>") so the reader knows the gate ran.

Mechanical fixes apply directly; anything that changes authority, access or what the teammate
does to real tasks goes back to the user.

### 6 — Build in Asana

Order matters:

1. **Conventions & fields first.** The teammate cannot create custom fields; a human creates
   any field the design needs (e.g. `Lane`) before the first run.
2. **Access.** Lowest role that works (Commenter before Editor). Access is the hard boundary;
   guidance is a soft one — anything that must never happen should be prevented by
   permissions where possible, and by guidance plus a test where not.
3. **Behavior guidance** → Customize → Behavior → Instructions.
4. **Skills.** Library: *Add skill → template → Use template*, then edit. Custom: *Create skill
   → Upload Markdown* or blank + paste. Attachments per Skill.
5. **Apps** only if a Skill reads or writes Drive/Microsoft files.
6. **Sharing.**
7. **Triggers last, and off.** Write them down (recurring tasks, rules, form default
   assignee, whose permissions each runs under) but switch on only after Phase 7's dry run
   passes. Pause existing triggers while you replace guidance or access. A recurring task
   only re-creates itself when completed, so the guidance must let the teammate complete
   its own trigger task.

Batch every setup action that touches real work into **one** approval question, a line per
item. That approval covers setup only; it is not standing approval for the teammate's later
bulk changes.

### 7 — Evals (preregistered)

Write before the first live run (`references/quality-and-evals.md`): 6–10 seed tasks from the
real backlog with expected outcomes; 2–6 decoys the teammate must decline or route
(including one per thing that must never happen); numeric bars; a stop rule. When the first
job reads existing data (a backlog sweep, a status digest), also write the **expected first
run**: what it should find today, from your audit numbers — the answer key the user checks the
teammate's first real output against. Run the tests in a separate test project with copied
tasks (a section of a live project is not a sandbox: searches and weekly sweeps still reach
the live tasks). Dry-run 2–3, read **View activity**, fix, then run the full set.

### 8 — Health score & baseline

Score with the weighted rubric, save scores + versions as the baseline, re-score every later
edit against it.

### 9 — Iterate, version, hand over

One change per iteration. Version guidance and Skills in files with a "supersedes" line. After
a week, review **Memory**: delete wrong memories, promote stable lessons into Skills. Add
roadmap responsibilities one Skill at a time, each with its own seed tasks.

## Fix path

For "it does X wrong". One reply the user can act on today — aim for well under 800 words
plus the replacement guidance (example: `examples/overdue-organizer-fix.md`). In this order:

1. **Diagnosis** — map each bad behaviour to its cause. Look in four places, not just the
   guidance: (a) instruction lines that invite it (quote them); (b) Skills whose description
   or output format pulls it that way; (c) **memory** that learned it; (d) **rules, forms or
   recurring tasks** that hand it work or run it under someone else's permissions. Say which
   you could see and which the user must check.
2. **Fix** — paste-ready replacement guidance in the reply itself (not only in a file), plus
   the specific Skill edits, memory deletions and access changes. Keep explicit user requests
   workable (e.g. "assign this to [person]" from a named requester is fine) while removing the
   behaviour nobody asked for — an over-correction annoys users in a new way.
3. **Hard stops** — the behaviours that must never happen get a permission change where
   possible, not only an instruction.
4. **Test it** — 3 test prompts by default (one per reported problem, plus one that checks an
   explicit request still works if you tightened a permission), with the expected new
   behaviour. Run them before and after the change, in a test project with copied tasks. For
   a harmful behaviour (reassigning, re-dating), don't reproduce it: use View activity from
   the reported incident as the "before".
5. **Next** — change one thing at a time and re-run the same prompts; if the problems come
   back, offer the Build path.

Leave out what they didn't ask for: no spec, no health score, no Skill rewrites unless a
Skill is a cause. End with a one-line offer of the fuller follow-up (more tests, a Skill
rewrite, a full rebuild).

## Outputs (Build path)

The user gets a small, paste-ready kit. Working notes live in a separate folder so the kit
stays readable:

```
<teammate-slug>/
  README.md               starts with "Before you use this" (NOT READY items, blockers, the
                          one or two inputs only the user can give); then setup steps in paste
                          order, what it does / never does, open questions, audit summary
  behavior-guidance.md    paste-ready, versioned
  skills/<skill>.md       one Asana-format Skill per file — upload as-is
  attachments/<file>.md   domain material and conventions the Skills reference
  evals/seed-tasks.md     test set, decoys, bars (baseline scores appended after the run)
  evals/expected-first-run.md   answer key for the first live run (when the job reads data)
  _working/               spec.md (incl. premises, decisions and review notes) and
                          readiness-audit.md — two files, for the builder, not required reading
```

If you could not ask the user anything, put the questions with your defaults at the top of
the README, most consequential first, and mark the kit `UNAPPROVED: don't switch on triggers
until these are answered`.

## Publishing a teammate kit for others

To share the result (a community forum, a client, a template library), follow
`references/publishing.md`: strip names, IDs, URLs and internal jargon, turn specifics into
`[placeholders]` with a one-line hint, keep the readiness checklist and evals, and say what was
tested and what was not.

