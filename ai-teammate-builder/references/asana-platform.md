# Asana AI Teammates — platform facts

Sources: Asana Help Center articles *How to use Asana AI teammates*, *Triggering AI
Teammates*, *Understanding access control for AI Teammates*, *AI Teammate Skills*,
*AI Teammates templates*, *How to create or discover an AI Teammate* (lastmod Jun–Aug 2026),
plus direct inspection of the Customize tab and Skill library (Oct 2026).

**Re-verify before relying on:** the can/can't table, plan availability, whether behavior
guidance is writable via API, and the Skill library contents. These move between releases.

## Contents
1. Anatomy of a teammate
2. Skills
3. Triggers
4. Access control, approvals, memory
5. Can / can't
6. Library Skills useful for PM-type teammates
7. Practical limits found in use

## 1. Anatomy of a teammate

Customize tab layout: **Behavior** (tabs *Instructions* and *Skills*), **Access** (tabs
*Work*, *Attachments*, *Apps*), **Memory**. Plus name, avatar, description, sharing.

- **Name / description** — write the description for colleagues: when and how to use the
  teammate. Put anything the teammate must follow in guidance or Skills, not here.
- **Behavior guidance (Instructions)** — always-on: how it speaks, thinks, delivers. Plain
  text; structure (headings, bullets, short labelled lines) helps it parse priorities.
- **Access → Work** — specific projects and teams, each with a role (e.g. Editor).
- **Access → Attachments** — public URLs or files picked from Google Drive / OneDrive.
- **Access → Apps** — general search/update permission on linked Google Drive and
  OneDrive/SharePoint. Connected from the profile page after creation.
- **Memory** — built automatically from interactions; cannot be written manually; can be
  reviewed and deleted. A user only sees a memory if they can see the source task.
- **Sharing** — creator sets who can use / edit / administer.

API: `GET /agents/{gid}` returns `name, description, behavior_guidance` (read). It does not
return the teammate's access list, Skills or memory — read those in the Customize tab or ask
the user. Treat the UI as the write path for guidance, Skills, access and sharing.

## 2. Skills

A Skill is packaged expertise: **guidance** (instructions + workflow), **trigger
conditions** (when to reach for it instead of another), optional **attachments** (reference
files used only when the Skill runs). Skills load selectively — unrelated Skills add no
noise, so a teammate can hold many.

- Add from the **Skill library** (Asana-authored, ~180 across Essentials, Marketing,
  Strategic operations, IT, Professional Services, Manufacturing, Retail, Healthcare, plus
  *My organization*). Applying one copies it onto the teammate; edits don't affect others.
- Create your own: **Create skill → blank**, or **Upload a Markdown file**.
- Roles: User sees Skills; Editor adds/edits/removes Skills and attachments; Admin manages
  the teammate.
- Naming convention (Asana's own): teammates are job titles ("Supply Coordinator"); Skills
  are action-oriented ("KPI Dashboard Design").

### Asana's Skill format (observed in every library Skill)

```
Description   — what it does + "Use when a user asks to …" trigger phrases
                + "Also use when …" situations + "Do NOT use for … (use <other-skill>)"
Instructions
  <Title>
  One paragraph: what happens when invoked and what the output is for.
  Before <job>  — scan first, surface what's there, then ask only what the data can't answer;
                  confirm delivery format.
  Workflow      — "<Skill> Progress:" checklist of numbered steps
  Output format — a fixed template with [placeholders]
  Gotchas       — the realistic ways the data will be messy, and what to do
  Cadence & Automation — when to run it; offer a recurring task / rule
  Integrations  — which apps add what
  What this Skill does NOT do — explicit non-goals, pointing to other Skills
```

Write custom Skills in this shape (`assets/asana-skill-template.md`). It isn't an Asana
requirement; it's the shape the library Skills use (observed Oct 2026), so users recognise
it. Leave out sections that would be empty.

## 3. Triggers

| Trigger | Runs as | Notes |
|---|---|---|
| Task assigned to teammate | assigning user | the default way to give work |
| @mention in a comment | mentioning user | questions, instructions, interrupts mid-run |
| Update on work it collaborates on | — | completion, key custom field changes *can* re-trigger; not every update does |
| Comment on a task it collaborates on | commenting user | only *may* trigger, and only when the comment is directed at it |
| Rule (e.g. task added to section → assign) | rule owner (unless set otherwise) | intake, triage |
| Form submission (teammate = default assignee) | form creator, or submitter on logged-in forms | intake |
| Recurring task assigned to teammate | not documented; check View activity | weekly reports, backlog reviews. The next occurrence is created only when the current one is **completed**, so the teammate must be allowed to complete it |
| Self-scheduled follow-up ("check back Friday 9am") | — | periodic attention without a fixed recurrence |

Rules also have time-based triggers, e.g. *Task is overdue* N days after the due date, or
*Due date is approaching* (documented Jul 2026). They fire only for incomplete tasks and only
for events after the rule was created.

Activity: **View activity** shows what it is doing; you can interrupt in the task thread.

## 4. Access control, approvals, memory

- Same permission model as a human user; cannot bypass permissions.
- Works only with information **both** the teammate **and** the running user can access.
- External tools use the running user's authentication; the user grants access on the
  profile page or when the request triggers.
- Approval required (documented mid-2026) for: deleting tasks it did not create; assigning a
  user who doesn't already have access to the task; adding a task to a project where it is
  not an editor; adding or removing collaborators. These are Asana's gates. Your company
  policy can be stricter, and that part lives in guidance, not in Asana. The approval is asked of the *running user* — if
  someone keeps approving, the behaviour continues; check View activity to see who.
- Not gated by approval: deleting tasks **it created itself**, assigning people who are
  already on the task, editing fields and descriptions on tasks it can edit. Guidance plus a
  decoy test is the only guard for these; project roles (Commenter vs Editor) are the hard one,
  with two documented holes: a task multi-homed in a project where it is Editor is editable
  everywhere, and a Commenter who is *assigned* a task can complete it, change its assignee
  and due date, and edit its fields. So a Commenter limit holds only if the teammate is never
  the assignee of those tasks and has no Editor role on another project they live in. Test it
  with an edit attempt.

## 5. Can / can't (as documented mid-2026)

Can: read/act on tasks, projects, goals, portfolios; search tasks, subtasks, projects,
milestones, messages, comments, attachments, custom fields, status updates, goals,
dashboards (where it has access); set task name/description, complete tasks, comment;
create tasks, subtasks, projects, sections, milestones, dependencies; edit titles,
descriptions, assignees, due dates; bulk update; set existing custom field values; attach
files; create Google Docs/Sheets and Word/Excel/PowerPoint files; read Drive/OneDrive files,
task images and attachments.

Can't: create goals, custom fields, dashboards/charts; remove a task from a project; send
messages or status updates; add/remove users from objects; search resourcing objects
(capacity plans, workload); generate images, PDFs or Google Slides; see anything the
running user can't.

## 6. Library Skills useful for PM-type teammates

Essentials: Blocker & Dependency Flagging · Brief Writing · Escalation Monitoring · Goal
Tracking · Humanize Output · Intake Classification & Routing · Intake Form Design · Kickoff
Facilitation · Knowledge Curation · Meeting Briefing · Meeting Summary & Action Capture ·
Milestone Tracking · Narrative Report Generation · Priority & SLA Scoring · Project Close &
Retrospective · Project Scoping & Task Breakdown · Review & Approval Tracking · Risk
Detection · Stakeholder Communications · Template Automation · Timeline & Dependency
Planning · Trend & Historical Analysis.

IT / delivery: Sprint Backlog Management · Sprint Retrospective Synthesis · Stand-Up
Facilitation · Velocity & Delivery Tracking · Release Notes Generation · Root Cause Analysis.

Strategic operations: Decision Log Maintenance · Duplicate & Overlap Detection · Process
Standardization · Workflow Optimization · Onboarding Guide Generation.

Marketing (web/content teams): Editorial Calendar Management · Content Brief Writing ·
Content Gap Analysis · Asset Review & Approval · Publishing Readiness · Launch & Event
Readiness.

Pick by responsibility, then read the Skill's full instructions (open it → See more) before
adding — several overlap and explicitly hand off to each other ("Do NOT use … use X").

## 7. Practical limits found in use

- Auto-generated guidance (from the create wizard) tends to be generic and over-fitted to
  whatever task was open at creation. Rewrite it from the spec.
- Process knowledge lives wherever the team keeps it — Google Docs, SharePoint, a wiki
  (Notion, Confluence, …), PDFs, Asana project descriptions, or only in people's heads. The
  teammate reads Drive/OneDrive (when connected) and Asana itself; anything else is
  invisible: export the relevant docs to Markdown/PDF and attach them to the Skill that
  needs them. If nothing is written down (common), the conventions proposal
  (`work-conventions.md`) becomes the attachment.
- Tasks multi-homed across a backlog and a sprint board: decide which project is canonical
  for status, and give the teammate access to both, or it will report half the picture.
- It cannot create the custom field your process needs — humans set up fields first.
