# Convention Check

## Description
Checks one task against the team's active work conventions when someone asks, and replies
in that task with what's missing (or that nothing is). Use when someone @mentions the
teammate on a task with "does this task follow our conventions?", "check this task",
"what's missing here?" or "is this ready by our rules?". Do NOT use for "how are we doing on
conventions" or any report across many tasks (use Weekly Convention Review). Do NOT use for
creating or changing conventions; that's the Convention Setter's call.

## Instructions

### Convention Check
When invoked, this skill reads the active conventions and the task, then replies to the
person who asked. The output is one comment they can act on in under a minute.

### Before the check
1. Read the Work Conventions project: which conventions are *Accepted*, which *On trial*.
   Ignore *Old way* and archived ones.
2. Read the task: name, assignee, due date, section, custom fields, project(s), and its
   comment history.
3. Find which conventions apply to this project and task type. If none apply, say so.
4. If the request was a report across tasks rather than this one task, say that's the weekly
   review and offer to add it to the next one.

### Workflow
Convention Check Progress:
- [ ] Step 1: List the gaps: required fields empty, name not matching the pattern, wrong
      section, no assignee past the agreed window.
- [ ] Step 2: No gaps → reply "Checked against [n] conventions: all good." and stop.
- [ ] Step 3: Gaps → reply with the most important one first (missing owner > missing
      required field > wrong section > naming), then the others as one short list.
- [ ] Step 4: If the task was assigned to you, ask the asker to reassign it to its owner.
      Don't complete it or change it.

### Output format
"Checked against [n] conventions.
- [Gap 1]: [what's off]. Accepted convention: [link]. Expected: [value/pattern].
- [Gap 2, if any]: … On-trial convention: [link], worth trying here."

### Gotchas
- A task in several projects → apply only the conventions of the project the asker is
  working in; mention that the other project may have its own rules.
- Subtasks often legitimately skip fields → follow the convention text; if it doesn't
  mention subtasks, don't flag them.
- A convention task is vague ("fill the important fields") → say it's unclear instead of
  guessing, and list it for the weekly summary's "Patterns worth discussing".

### What this Skill does NOT do
- Does not fix the task itself; the owner does.
- Does not post unprompted nudges; those come only from Weekly Convention Review.
- Does not escalate; repeat gaps are handled in Weekly Convention Review.
