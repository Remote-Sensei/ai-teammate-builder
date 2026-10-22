# Worked example: Convention Keeper

A teammate that keeps a team's agreed work conventions alive: it notices where tasks drift
from what the team decided (empty required fields, wrong names, wrong section, no owner) and
nudges the person with a link to the exact convention. Once a week it summarises adherence
for the people who own the conventions.

The starting point is the public **Convention Keeper** listing on
[aiteammates.directory](https://aiteammates.directory/agents/convention-keeper). It's a good
design, which makes it a useful example: the process below doesn't rewrite it from scratch,
it finds the handful of places where a good-sounding instruction would fail in real use and
fixes those. Replace every `[placeholder]` with yours; the readiness audit decides what your
version needs.

## Situation the build assumes

- A **Work Conventions** project: one task per convention, sections such as *On trial*,
  *Accepted*, *Old way*. Each convention task says what the rule is and why.
- 2–5 **monitored projects** where the conventions apply, with the custom fields the
  conventions refer to (Priority, Status, Team…).
- A **Convention Setter** who owns the rules and one or two **Workflow Guardians** who follow
  up with people.
- No outside-Asana agent is needed for the first job. If one exists, it gets the bulk
  backfills (below).

If your team has no written conventions yet, that's the blocker: start from
`references/work-conventions.md` and agree on 5–8 before building this teammate.

## What changed from the directory version, and why

| Directory version | Problem in real use | This build |
|---|---|---|
| "Re-triggers on every task update" as a project collaborator | Asana documents that updates *can* re-run a teammate on work it collaborates on (completion, key field changes), and that comments *may* trigger it only when directed at it (documented as of Jun 2026). Being a project member isn't the same as collaborating on every task, so the coverage isn't guaranteed, and where it does work, every run is a chance to add a comment. | No unprompted nudges between reviews. People can ask for a check any time with an @mention. The weekly review is the one place unprompted nudges come from, capped and deduplicated. |
| "Cannot do: reassign tasks, complete tasks…" written in the guidance | The platform *can* do these; the list is a policy, not a limit. | **Commenter** on monitored projects, **Editor** only on Work Conventions. Commenter has documented holes: if the teammate is *assigned* a monitored task, or the task is multi-homed in a project where it's Editor, it can edit it. So it is never assigned monitored tasks, and seed test D1 attempts an edit. |
| "Never flag the same task twice in a week" | Relies on memory, which isn't guaranteed to hold that. | Before commenting it reads the task's comment history. The check lives in Asana data, not memory. |
| "Drop an encouraging note on roughly 1 in 10 clean tasks" | Random praise is noise, and "1 in 10" can't be followed reliably. | No comments on clean tasks. Praise goes in the weekly summary ("what improved"). |
| Weekly audit comments on every gap it finds | First run on a messy project = dozens of comments in one morning; the team mutes it. | `CHANGE MODE: propose` for the first two weeks: it lists the nudges it *would* post and posts none. Then at most [15] per week; the rest are listed in the summary. |
| Weekly audit scans tasks updated in the last 7 days | Stale tasks and old gaps are exactly the ones nobody updates, so they never show up. | It checks all open tasks in active sections, and reports last week's activity separately. |
| Weekly summary "@mentions the Setter and Guardians as collaborators" | Adding collaborators asks the running user for approval (documented as of Jun 2026). On a recurring task nobody is watching, the run stalls. | The summary is assigned to the Setter, who is a member of Work Conventions (assigning someone with access needs no approval). Repeat gaps go as subtasks to Guardians who are members too. |
| "Cannot do: complete or close tasks" | A recurring task only creates its next occurrence when it is completed. With this rule the weekly review runs once and never again. | It completes its own weekly trigger task at the end of a run, and nothing else. |
| One block of guidance holding both modes | Every run carries both procedures. | Two Skills (on-request check, weekly review); guidance keeps only the always-on rules. |
| No tests | "Friendly and accurate" can't be checked. | Seed tasks + decoys with bars (`evals/seed-tasks.md`), run in a test project. |

## Lanes

| Lane | Work |
|---|---|
| Teammate | read conventions, check tasks on request, weekly review with capped nudges, summary task, "patterns worth discussing" |
| Agent (optional) | bulk backfills the teammate shouldn't do by comment — e.g. setting Priority on 120 old tasks, renaming a whole section to the new pattern. The teammate prepares the task (scope, list of tasks, the rule, who approves); the agent runs it; a human approves first. Without an agent this lane is Human. |
| Human | Convention Setter: accepts, changes or retires conventions; decides exceptions. Workflow Guardians: follow up on repeat gaps. Task owners: fix their own tasks. |

## Deterministic vs judgement

Some checks don't need a teammate. A pure "field is empty when the task is added" check is
often cheaper as an Asana rule (task added to project → condition: field empty → action),
if your plan's rules support it. Keep the teammate for what a rule can't do: reading the
convention text, judging names and section placement, choosing the one gap worth mentioning,
writing the summary and spotting new patterns.

## Setup in paste order

1. **Fields first.** Make sure every field a convention names exists on the monitored
   projects (the teammate can't create custom fields).
2. **Access.** Work Conventions project: Editor. Monitored projects: Commenter. Check the
   teammate has no Editor role on other projects those tasks are multi-homed in.
3. **Behavior guidance** → `behavior-guidance.md`.
4. **Skills** → *Create skill → Upload Markdown*: `skills/convention-check.md`,
   `skills/weekly-convention-review.md`.
5. Run the **seed tests** in a separate test project with copied tasks and a copy of the
   conventions (`evals/seed-tasks.md`).
6. **Trigger, last.** A recurring task "Weekly convention review" every [Monday], assigned
   to the teammate, in the Work Conventions project, created by someone with access to all
   monitored projects (it can only see what both of them can see; check View activity for
   who it ran as). Start in `propose`; flip to `apply` after two clean weeks.

## Roadmap (one Skill at a time, each with its own seed tasks)

- Live nudges between reviews, once you've confirmed in View activity which updates actually
  re-run it, with a daily cap.
- Onboarding nudge: a new member's first 10 tasks get a single welcome comment with the top
  five conventions.
- Convention trial report: at the end of an *On trial* period, adherence and complaints for
  that convention, so the Setter can accept or drop it.
- Library Skills to consider: *Process Standardization*, *Duplicate & Overlap Detection*.
