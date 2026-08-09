# litecrew-workspace

> Clone this into a project, open it in your AI coding CLI, and the directory takes over from there.

`litecrew-workspace` is **not an application** — it is a directory of plain-Markdown
conventions. When you point an AI CLI at it (Claude Code, Codex, Cursor, …), the CLI
picks up [`AGENTS.md`](./AGENTS.md) and starts operating as **Eve**: a supervisor who
plans your request, splits it into Goals and Tasks, hires the right subagent for each
piece, and captures the results as durable knowledge.

You never touch the file structure by hand. You just talk to your CLI the way you
always do — describe what you want, redirect when needed, read the results. Eve handles
the bookkeeping and writes everything down as files you can grep, diff, and review.

## Quick start

```bash
git clone <this-repo> my-workspace
cd my-workspace

# Open this directory in your AI CLI of choice.
claude         # Claude Code
# codex        # Codex
# cursor .     # Cursor
```

Then describe what you want in plain language. For example:

> *"I want to build a small landing page for my SaaS and ship it to Netlify."*

Eve will read the operating contract, draft a Goal capturing the outcome, split off the
single most urgent Task, dispatch a subagent to do the work, and write progress into the
workspace as it goes. When the work is done, Eve captures any reusable lessons and
reports back. You can interrupt, redirect, or ask for status at any time.

## How it works (the 1-minute version)

- **You** set direction and approve decisions. You don't manage files.
- **Eve** is the supervisor. She plans, dispatches, and maintains the workspace. She
  never writes code or runs commands herself — that's what subagents are for.
- **Subagents** are specialist workers (an engineer, a researcher, an archivist, …).
  Each one is a short Markdown spec under `agents/`. Eve dispatches one per Task.
- **Files are the contract.** Goals, Tasks, Knowledge, Handbooks, Sessions — all plain
  Markdown. Eve and the subagents read and write them; you can read along any time.

The full operating model is in [`AGENTS.md`](./AGENTS.md). You do **not** need to read
it to use the workspace — Eve loads it automatically. It's there if you ever want to
know exactly how the gears turn, or if you want to fork the paradigm and tweak it.

## What ships in the box

```
litecrew-workspace/
├── AGENTS.md            # Eve's operating contract (auto-loaded by your AI CLI)
├── workflows/           # Lifecycle protocols Eve follows (Goal, Task, Subagent, Knowledge, …)
├── templates/           # File templates Eve instantiates when creating new Goals / Tasks / agents
├── agents/              # Subagent definitions. Ships with one example (workspace-archivist).
├── skills/              # Two meta-skills: find-skills + skill-creator
├── goals/               # Empty — Eve fills this in as you describe what you want
├── tasks/               # Empty — same
├── knowledge/           # Empty — durable lessons captured across Tasks
├── handbooks/           # Empty — domain playbooks Eve writes when patterns repeat
├── sessions/            # Empty — Eve's session log for cross-conversation memory
└── archive/             # Empty — closed Goals and Tasks retire here
```

Every directory ships with a README explaining its role. The empty directories are
intentional: **you bring the work, Eve brings the discipline**.

## Notes for CLI tools

- **Claude Code**: reads `CLAUDE.md` automatically. This repo symlinks `CLAUDE.md` →
  `AGENTS.md`, so Eve's contract loads with zero configuration.
- **Codex / Cursor / others**: most modern AI CLIs auto-load `AGENTS.md` or an
  equivalent project-level file. If yours doesn't, open `AGENTS.md` in your first
  message and the rest of the conversation will follow the same paradigm.

## License

MIT — see [`LICENSE`](./LICENSE). © litecrew contributors.
