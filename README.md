# litecrew-workspace

> A file-system-native operating model for an AI steward (Eve) and a fleet of disposable subagents.

`litecrew-workspace` is the open-source release of the workspace paradigm that powers
[litecrew](https://litecrew.com). It is **not** an application — it is a set of
conventions, templates, and workflows that turn a plain directory of Markdown files
into a self-documenting, audit-friendly workspace where a supervisor agent (Eve)
dispatches focused work to specialized subagents and captures the results as durable
knowledge.

## The paradigm in two paragraphs

**Eve is the steward.** Eve plans, dispatches, and maintains the workspace but never
executes production work directly. Every concrete piece of work — development, research,
verification, writing, ops — is delegated to a **subagent**, which is a short Markdown
spec describing a role, its skills, and its boundaries. The workspace itself is the
contract between them: Eve reads `goals/` to decide what to advance, splits off a single
`tasks/<task>.md`, assigns it to a subagent, and supervises until the task closes.

**Goals, Tasks, and Knowledge are first-class files.** A Goal is a multi-week objective
that decomposes into atomic Tasks. Each Task is owned by exactly one subagent, may take
several iterations to close, and must pass explicit "sediment gates" (knowledge capture,
artifact placement, session notes, handbook review) before it is archived. Knowledge and
handbooks accumulate across Tasks so the workspace gets smarter over time. The whole
system is driven by plain Markdown plus a small set of lifecycle protocols under
`workflows/`.

## Getting started

```bash
git clone <this-repo> my-workspace
cd my-workspace
```

Then:

1. **Read `AGENTS.md`** at the root — it is Eve's "operating contract" and the single
   source of truth for the workspace model.
2. **Create your first Goal.** Copy `templates/goal-template.md` into `goals/`, name it
   with kebab-case (e.g. `goals/launch-landing-page.md`), and fill in the success
   criteria. Success criteria are the *only* judge of whether the Goal is done, so make
   them measurable.
3. **Split off the first Task.** Identify the single most urgent piece of work that
   unblocks the Goal, copy `templates/task-template.md` into `tasks/`, and assign an
   `assigned_agent`. If no matching subagent exists yet under `agents/`, create one from
   `templates/agent-template.md`.
4. **Dispatch a subagent.** Point the subagent at the Task file and at
   `workflows/subagent-workflow.md`. The subagent reads relevant `handbooks/` and
   `knowledge/`, executes, and writes progress back into the Task file.
5. **Close the loop.** When the subagent reports completion, walk the gates in
   `workflows/task-lifecycle.md` (knowledge sediment, artifact placement, session notes,
   handbook review). Then archive the Task and pick the next one.

The workspace ships **empty by design**: `goals/`, `tasks/`, `knowledge/`, `handbooks/`,
`sessions/`, and `archive/` contain only READMEs. You bring the content.

## Where to read more

- Source of truth for the model: [`AGENTS.md`](./AGENTS.md)
- Lifecycle protocols: [`workflows/`](./workflows/)
- File templates: [`templates/`](./templates/)
- Example subagent: [`agents/workspace-archivist.md`](./agents/workspace-archivist.md)
- Bundled meta-skills: [`skills/`](./skills/)

Web home:

- Web: <https://litecrew.com>
- Project / source mirror: <https://litecrew.sh>
- Product / hosted: <https://litecrew.ai>

(Domains registered by the litecrew maintainers; replace with your own fork's links if
you fork the project.)

## License

MIT — see [`LICENSE`](./LICENSE). © litecrew contributors.
