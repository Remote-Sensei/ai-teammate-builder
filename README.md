# ai-teammate-builder

An agent skill for designing, building, testing and fixing Asana AI Teammates from outside
Asana, in Claude Code, ChatGPT.

It walks your agent through the same steps a good manager uses to onboard a new hire. It reads
your Asana data first, then interviews you and audits whether the workspace is ready. It writes
the behavior guidance and Asana-format Skill files (ready for *Create skill → Upload Markdown*),
plans access and triggers, and writes test tasks with pass bars. You paste the result into
Asana and switch triggers on last.

Want a starting point? Browse ready-made teammates in the
[AI Teammates Directory](https://aiteammates.directory).

Three paths, picked from your request:

| You say | You get |
|---|---|
| "Build / set up a teammate for X" | A paste-ready kit: guidance, Skills, attachments, test tasks, setup order |
| "My teammate keeps doing X wrong" | One reply: diagnosis, replacement guidance, permission changes, before/after test prompts |
| "Review our teammate" | A short scored review with the top fixes |

## Install

**Claude Code**

```bash
git clone https://github.com/Remote-Sensei/ai-teammate-builder.git
cp -r ai-teammate-builder/ai-teammate-builder ~/.claude/skills/
```

**Codex CLI**

```bash
cp -r ai-teammate-builder/ai-teammate-builder ~/.agents/skills/
```

**Claude.ai:** zip the inner `ai-teammate-builder/` folder and upload it under
*Customize → Skills*.

Then ask: *"Help me build an Asana AI Teammate that triages our intake project."*

## Works best with

- An Asana **connector** or MCP, so the agent reads your projects, fields and tasks instead
  of asking you. Without one it asks you to paste what it needs.
- A **browser** the agent can drive (optional). The API doesn't show a teammate's access,
  Skills or memory, so without a browser you paste or screenshot the *Customize* tab.

The skill never changes your workspace without asking. It hands you paste-ready text and asks
before saving anything in Asana.

## What's inside

```
ai-teammate-builder/
  SKILL.md                 the process: paths, three lanes of work, ten build phases, fix path
  references/              platform facts, interview bank, readiness audit, evals, publishing
  assets/                  templates: behavior guidance, Asana Skill, working spec
  examples/
    convention-keeper/     Build path on a public teammate: guidance, two Skills, seed tests
    overdue-organizer-fix.md   Fix path for a teammate that invents data it can't see
```

## Platform facts age

Asana changes AI Teammates often. Platform claims in `references/asana-platform.md` are dated
("documented as of <month year>"). Check anything your design depends on against the current
Asana Help Center, and open an issue when something has changed.

## License

MIT. Built and used by [Remote Sensei](https://remotesensei.org) on our own teammates and in
client Asana implementations.
