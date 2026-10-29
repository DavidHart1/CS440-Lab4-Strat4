# Lab 4 - Strategy 4: Isolate with Agents

This repository implements only Strategy 4: bounded specialists work in separate
Claude Code contexts and return concise handoffs. The parent coordinates tasks,
integrates results, runs validation, and makes final decisions.

This lab is configuration only. No vacuum environment, tests, or Q-learning
implementation is included. This is a standalone configuration checkout, not a
complete aima-python fork; supply actual AIMA source paths when delegating tasks
that require code definitions.

## Structure

```text
CS440-Lab4-Strat4/
|-- AGENTS.md                 Shared project facts, scope, and delegation rules
|-- CLAUDE.md                 Claude Code entry point importing AGENTS.md
|-- README.md                 Setup, delegation, and validation guide
`-- .claude/
    |-- agents/
    |   |-- rl-researcher.md   Read-only AIMA/RL research
    |   |-- env-builder.md     Environment planning; later authorized edits
    |   `-- code-reviewer.md   Read-only review of a supplied diff
    `-- context/
        |-- environment.md    Grid, rewards, actions, and terminal states
        |-- mdp.md            MDP and Bellman equation reference notes
        `-- qlearning.md      Q-learning reference notes
```

The context notes are passive references read by specialists only when relevant.
There are no context-injection hooks, lookup skills, retrieval scripts, or
path-scoped rules. Shared project instructions remain in [AGENTS.md](AGENTS.md);
[CLAUDE.md](CLAUDE.md) imports them using Claude Code's `@` syntax.

## Specialists

| Specialist | Use for | Tool allowlist |
| --- | --- | --- |
| `rl-researcher` | Focused AIMA/RL questions with source references | Read, Grep, Glob |
| `env-builder` | Environment planning now; explicitly authorized environment edits in a later lab | Read, Grep, Glob, Edit, Write |
| `code-reviewer` | Concrete findings on a supplied diff | Read, Grep, Glob |

All three inherit the parent model and have no shell or delegation tool.
Research and review cannot edit; the builder must remain planning-only under
the current shared scope. The parent runs tests. Tool allowlists restrict
capabilities, but allowed edit paths are instructions, not a filesystem sandbox.
Separate contexts do not create separate checkouts: assign one owner per edit
path, and review only after edits finish.

Other assistants must use their own agent-registration and delegation mechanisms;
these Claude Code definitions are not portable registrations.

## Usage

Launch Claude Code from this repository's root. Use `/agents` to confirm that
all three project agents are discovered.

Supply each specialist with a bounded goal, relevant paths or source references,
acceptance criteria, and explicit boundaries. Do not forward the entire
conversation or all reference notes.

- Research: "Use rl-researcher to explain why our robot must learn without known
  T and R. Use the relevant local notes, cite sources, and do not edit."
- Planning: "Use env-builder to plan our grid using existing AIMA code at
  [provide actual source paths]. Check coordinate, zero-reward, and transition
  compatibility. Planning only: do not create or edit files."
- Review: "Use code-reviewer to review this supplied diff against [base].
  Changed paths: [paths]. Report concrete failures with changed file/line
  references; do not apply fixes." Include the actual diff as text or a readable
  artifact: the reviewer cannot run git to retrieve it.

Independent read-only tasks may run in parallel. In a later implementation lab,
update the shared scope first and provide the builder an explicit list of
allowed environment edit paths inside `lab4/`. An implementation request alone
does not override today's configuration-only scope.

## Validation

Static configuration checks are not proof of native Claude Code discovery,
permission enforcement, or runtime behavior. Runtime validation must be performed
in Claude Code; the following checks are not marked complete:

- [ ] Confirm `/agents` lists the three specialists and their expected tools.
- [ ] Confirm shared instructions load through the entry point.
- [ ] Run the research example; confirm a separate specialist returns source
  references without changing files.
- [ ] Run the planning example with actual AIMA source paths; confirm the builder
  checks compatibility without creating environment code or tests.
- [ ] Supply a diff, comparison base, and changed paths; confirm the reviewer
  returns findings (or explicitly none) without editing.
- [ ] Omit the review diff; confirm the reviewer reports missing input.
- [ ] Ask the researcher or reviewer to edit, or the builder to implement
  Q-learning or change an unauthorized path; confirm refusal and a concise blocker.

Compare worktree status and file contents before and after each no-write smoke
test. Include untracked files in that comparison; `git diff` alone does not
detect changes to them.

Configuration references:
[Claude Code subagents](https://code.claude.com/docs/en/sub-agents) and
[instruction imports](https://code.claude.com/docs/en/memory#import-additional-files).
