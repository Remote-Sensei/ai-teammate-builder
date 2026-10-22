# Weekly Convention Review

## Description
Checks the open work in the monitored projects against the team's conventions, posts a
capped number of nudges, and writes one summary task for the Convention Setter: adherence,
top gaps, what improved, and patterns worth discussing. Use when the recurring "Weekly
convention review" task is assigned to the teammate, or when the Convention Setter asks "how
are we doing on conventions?", "convention report", "adherence this week" or "which
conventions aren't sticking?". Do NOT use for checking a single task someone asked about
(use Convention Check). Do NOT use for proposing or editing conventions directly; those go in
"Patterns worth discussing" for a human to decide.

## Instructions

### Weekly Convention Review
When invoked, this skill reads the active conventions and the open tasks in the monitored
projects, nudges where it should, writes the summary, and completes its own trigger task.
The summary is read in the weekly ops sync, so it must make sense in two minutes.

### Before the review
1. Read the Work Conventions project (Accepted / On trial).
2. Look for a summary task for this week already (`Weekly convention review — [date]`). If
   one exists, update it instead of creating another.
3. Find last week's summary for the comparison.
4. Pull the open tasks in active sections of [monitored projects], plus what was created or
   completed in the last 7 days. Report the counts before judging anything.

### Workflow
Weekly Convention Review Progress:
- [ ] Step 1: Check each open task against the conventions that apply to it (same checks as
      Convention Check).
- [ ] Step 2: Count adherence per convention: tasks that follow it / tasks it applies to.
- [ ] Step 3: Read your own comments from the past 7 days: repeat gaps (nudged before, still
      open), disputes, unclear conventions.
- [ ] Step 4: Find stale tasks: no update in [14] days in an active section.
- [ ] Step 5: Spot patterns no convention covers (e.g. 8 tasks using different date formats
      in the name).
- [ ] Step 6: Nudges. Skip any task you commented on about the same convention in the last
      7 days. CHANGE MODE propose → post none, list them. Apply → post up to [15], one gap
      per task, most important first; list the rest.
- [ ] Step 7: Create or update the summary task in Work Conventions, assigned to the
      Convention Setter. For each repeat gap, add one subtask assigned to the right Guardian,
      unless an open subtask for that task and convention already exists.
- [ ] Step 8: Complete the "Weekly convention review" trigger task, so next week's occurrence
      is created.

### Output format
Task title: `Weekly convention review — [date]`

```
What improved: [1–3 lines, with numbers vs last week]
Open tasks checked: [N] in [projects] · Adherence: [X]% (last week [Y]%)
This week: [n] created, [n] completed

Top gaps
1. [Convention] — [n] tasks, e.g. [task link], [task link]
2. …
3. …

Repeat gaps (subtasks for Guardians): [task link] — [convention], first nudged [date]
Stale (no update 14+ days): [n] — [links, max 5]
Nudges [posted | I would post]: [n] — [list]; not posted (over the cap): [n]

Patterns worth discussing
- [Observation + count + question for the Setter]
- [Disputes and unclear conventions from this week, with links]
```

### Gotchas
- Very low task volume (< 10 open tasks) → report counts but skip percentages; they mislead.
- Projects the teammate or the person who set up the trigger can't see → say "not visible:
  [project]" rather than counting them as clean.
- The same person behind most gaps → don't name them in the summary; mention the count and
  let the Guardian follow up privately.
- A Guardian isn't a member of Work Conventions → don't assign them (it would need
  approval); name them in the summary instead.

### Cadence & Automation
Weekly, via a recurring task assigned to the teammate in the Work Conventions project. Suggest
moving it to fortnightly once adherence is above [90]% for a month.

### What this Skill does NOT do
- Does not create, edit or retire convention tasks.
- Does not edit tasks in monitored projects.
- Does not add collaborators or message people outside Asana.
