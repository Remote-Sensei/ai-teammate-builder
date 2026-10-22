# Worked example: Fix path, Overdue Organizer

The Fix path in one reply. The teammate is the public **Overdue Organizer** listing on
[aiteammates.directory](https://aiteammates.directory/agents/overdue-organizer): when a task
is 3 days overdue, it comments with 2–3 realistic rescheduling options for the assignee.

## The request

> Our Overdue Organizer keeps telling people things like "your calendar shows you're free
> Friday morning" and "you finish complex tasks faster before 11am". Nobody connected a
> calendar. Yesterday it also commented on a task that was already done. How do I fix it?

## The reply

**What's causing it**

1. *Invented calendar and productivity data.* The guidance invites it. Three of its example
   options are "Your calendar shows availability [specific time]", "you typically finish
   complex tasks faster before 11am" and "Block 2 hours Friday morning when your calendar is
   typically lighter". The teammate copies the shape of examples, and with no calendar to
   read it fills the slots with plausible guesses. Asana documents Drive and OneDrive files
   as the external sources a teammate can read, and says it can't search workload or capacity
   views (documented as of Jun 2026). You haven't connected a calendar, so any availability
   it mentions is made up, and so is the "calendar block" it offers.
2. *Comment on a finished task.* The guidance says "you activate 3 days after any task
   becomes overdue", but guidance can't schedule anything. Something else starts it: either a
   rule with the *Task is overdue* trigger set to 3 days (rules fire only for incomplete
   tasks), or a recurring daily task where it picks the tasks itself. With the recurring
   task, a list built at the start of the run, or no final check, lets a task completed in
   between still get a comment.

What I couldn't see, and you can check in a minute: which **recurring task or rule** starts
it, who it runs as (open View activity on a recent run), and its **Memory** tab. Delete any memory about
people's "productive hours" or calendars; it would keep the invented details coming back.

**The fix: paste over the current guidance**

```
You are the Overdue Organizer for [team]. When a task has been overdue for 3 days, you
help its assignee pick a realistic new plan. You are supportive: overdue work is normal in a
busy week, and you never imply failure.

What you can use — and only this:
- The overdue task: description, subtasks, comments, due date.
- The assignee's other incomplete tasks you can see in Asana, with their due dates.
- Their completed tasks in the last 30 days, for how many tasks they usually close a week.
No calendar is connected, and you can't see workload views. Never mention free time,
calendar slots, time of day or "your patterns" beyond what the task list above shows. If the
assignee tells you something in a comment ("I'm out Thursday"), you may use it and say it came
from them. If someone asks for calendar-based advice, say you can't see their calendar.

How you run (a daily recurring task "Overdue check" starts you):
1. Find incomplete tasks in [projects] whose due date was exactly 3 days ago.
2. For each, check again right before commenting: still incomplete? still overdue? no
   comment from you on it in the last 7 days? If any answer is no, skip it.
3. Comment once with 2–3 options, each tied to something visible:
   - New date: "[date] — you have [n] other tasks due before then."
   - Break it down: "Split into [2–3 subtasks named from the description]."
   - Swap: "Move [lower-priority task, linked] to [date] to make room."
   - Hand off: "[Name] works on related tasks — worth asking them?" (suggest only)
   End with: "Reply with an option and I'll update the date."
4. When the assignee replies with an option, apply it: change the due date or create the
   subtasks. Never reassign the task or change anyone else's tasks.
5. When the check is done, complete the "Overdue check" task so tomorrow's is created.

Format: "Hi [name] 📅 [task] has been overdue a few days. You have [n] open tasks, [m]
due this week. Options: 1… 2… 3… Which works?"
Keep it under 80 words. [Language].
```

**Hard stops beyond the text**

- If you don't want it changing due dates at all, give it **Commenter** access on those
  projects and drop the last line of step 3 and step 4. Guidance is a soft boundary; the
  project role is the hard one.
- Make the trigger explicit: one recurring daily task, "Overdue check", assigned to the
  teammate (step 5 keeps it recurring). A *Task is overdue* rule is the other option, but the
  documented way for a rule to start a teammate is assigning it the task, which takes the task
  away from its owner. It only sees what both it and the person it runs as can see, so check
  View activity for who that is.

**Test it: in a test project with copied tasks, before the change and after it**

1. @mention it on a task due 3 days ago: "check this overdue task". *Expected after:*
   options cite task counts and dates only; no calendar, time-of-day or "you usually" claims.
   For the "before", the reported comments are enough evidence; you don't need to re-create
   them.
2. Complete a task that was due 3 days ago, then run the daily check. *Expected after:* no
   comment on it.
3. Reply "option 1" on one of its comments. *Expected after:* the due date changes to the
   proposed date and it confirms in one line. (This checks the fix didn't break the useful
   part.)
4. Ask "when am I free this week?" *Expected after:* it says it can't see calendars.

**Next.** Change one thing at a time: guidance first, re-run the four prompts; then memory;
then the trigger. If it still invents availability after all three, tell me and we'll look
at a fuller rebuild with a proper first-job Skill and seed tests.

## Why this is the Fix path, not a build

The person asked "how do I fix it". They get one reply: causes with the quoted lines, a
paste-ready replacement, the access change for the hard stop, and four tests. No spec, no
interview, no health score. The useful behaviour (offering options, updating the date when
asked) is kept, so the fix doesn't swap one complaint for another.
