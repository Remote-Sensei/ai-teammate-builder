# Workspace readiness audit

A teammate amplifies the conventions it works in. Pointed at a clean project it multiplies
good habits; pointed at a messy one it produces confident noise. The audit tells the user
which, before they find out from the teammate.

## How to collect (Asana REST / connector)

For each candidate project:

- Project: `GET /projects/{gid}?opt_fields=name,notes,members.name,custom_field_settings.custom_field.name,custom_field_settings.custom_field.enum_options.name`
- Sections: `GET /projects/{gid}/sections`
- Open tasks: `GET /projects/{gid}/tasks?completed_since=<now ISO>&opt_fields=name,assignee.name,due_on,created_at,modified_at,memberships.section.name,memberships.project.name,custom_fields.name,custom_fields.display_value,notes,num_subtasks` (paginate)
- Existing teammate: `GET /agents/{gid}?opt_fields=name,description,behavior_guidance`
- Not in the API: the teammate's **access list, Skills and memory** (Customize tab), and
  rules/forms on a project (project Customize panel). Read them with a browser, or ask the
  user for a screenshot — it takes them seconds and turns an UNVERIFIABLE into a fact.

Read 5–10 task descriptions in full; field stats alone miss whether tasks are *understandable*.

## Checks and thresholds

| # | Check | READY | NEEDS WORK | BLOCKER |
|---|---|---|---|---|
| 1 | Teammate *and* each trigger's running user can access every project and doc the job needs (Customize → Access; ask if you can't see it) | all | — | any missing |
| 2 | Open tasks with an owner | ≥ 80% | 50–79% | < 50% *and* the job relies on owners |
| 3 | Open tasks with a due date or sprint | ≥ 60% | 30–59% | < 30% *and* the job is time-based |
| 4 | Priority / estimate fields exist and are used | field exists, ≥ 50% filled | exists, < 50% | job needs it and it doesn't exist |
| 5 | Sections have a clear meaning (pages, stages, or status — not a mix) | yes | mixed | — |
| 6 | Duplicate / dead sections (two "Done", empty legacy sections) | none | some | — |
| 7 | Stale work: open tasks untouched > 12 months | < 10% | 10–30% | > 30% |
| 8 | Multi-homing has a rule (which project is canonical for status) | written | implicit | contradictory |
| 9 | Task descriptions state outcome + acceptance | most | some | almost none *and* job is execution prep |
| 10 | Process docs / conventions exist and are reachable by the teammate | written + reachable | written, not reachable (attach) | none |
| 11 | Existing automation overlapping the job (rules, forms, templates) | mapped | unknown | conflicting |
| 12 | A definition of ready exists (per lane, see `work-lanes.md`) | yes | partial | no, and job is "make tasks ready" |

Honesty rule: anything you could not check is **UNVERIFIABLE**, with the reason. Never round
up to READY.

A BLOCKER does not mean "stop the project". A data-quality blocker (checks 2–9, 12) can be
fixed first, made the teammate's first job (e.g. a backlog-health Skill whose job is exactly
checks 2–7), or explicitly accepted. Missing access (1) or conflicting automation (11) can't
be accepted, only fixed; until then the kit stays a draft.

## Report template

```markdown
# Readiness audit — <Teammate name> — <date>

**Verdict:** READY / READY WITH FIXES / NOT READY — <one line why>

| Source | Verdict | Key numbers | Fix |
|---|---|---|---|
| <Project A> | NEEDS WORK | 90 open · 38% owned · 6% dated · 2 "Done" sections | assign or archive pre-2024 ideas; merge Done |
| <Process docs> | NEEDS WORK | live in <wiki>, not a supported app | export → attach to <Skill> |

## Blockers (fix or accept before design)
1. …

## What already exists (don't rebuild)
- Rule: … · Form: … · Library Skill that covers part of the job: …

## Missing conventions (propose in Phase 4)
- …

## Unverifiable
- … (reason)
```
