# Lab 4 - Vacuum Robot with Reinforcement Learning (CS 440)

## Project overview
Part of our aima-python fork. We are preparing a vacuum-robot agent that
will learn with Q-learning in a later lab. Current work is configuration
only: do not implement the environment or Q-learning in this lab.

## Environment
- 4x4 grid, cells as (row, col); (0,0) top-left is the start
- Wall "X" at (1,1): cannot be entered
- Terminal cells: -1 at (3,1), +10 at (3,3); all other cells 0
- Actions: Up, Down, Left, Right (our assumption, following AIMA's grid world)
- Moving into the wall or off the grid leaves the robot in place (our assumption)
- There are 15 reachable states
- The transition model T and reward function R are UNKNOWN to the agent,
  so value/policy iteration (AIMA ch. 17) cannot be used directly; the agent
  must learn from experience (Q-learning, AIMA ch. 22)

## Coding standards
- Python 3; reuse aima-python's mdp.py and reinforcement_learning.py classes instead of rewriting them
- Configuration changes may update this repository's instructions, documentation,
  and .claude/agents/. Future implementation files must stay inside lab4/,
  after the shared lab scope is explicitly updated.
- Docstrings and type hints on every function and class
- Tests go in lab4/tests/ and use pytest

## Context
- Readings: AIMA ch. 12 (uncertainty), 17 (MDPs), 22 (RL)
- Detailed notes live in .claude/context/ and are loaded on demand; do not copy them here
- Read only the notes and source definitions needed for the assigned task
- Notes are passive references for specialists, not automatically injected context.
- This standalone configuration checkout does not include AIMA source. The parent
  must supply source paths when a task needs definitions; report missing sources
  rather than assuming a sibling checkout exists.

## Delegation - Strategy 4: Isolate
- Claude Code specialists are defined in .claude/agents/; other tools must use
  their own delegation mechanism, not assume these definitions are discovered.
- Use rl-researcher for focused AIMA/RL questions, env-builder for environment
  planning (implementation only in a later lab), and code-reviewer for a supplied diff.
- The parent supplies the goal, relevant paths or source references, acceptance
  criteria, and boundaries. Supply the actual diff and comparison base for reviews;
  for future implementation tasks, supply an explicit list of allowed edit paths.
- Do not forward the entire conversation or all context notes. Each specialist
  reads only task-relevant sources and returns a concise handoff, not raw transcripts.
- Delegate only work that benefits from separate context. Keep small lookups local.
- Run independent read-only work in parallel when useful. Never assign overlapping
  edit ownership; review only after the assigned edits are complete.
- Specialists stop and report missing inputs or out-of-scope requests to the parent.
  They do not expand scope, delegate further, commit, push, or change permissions.
- The parent integrates results, resolves disagreements, runs validation, and makes
  final decisions. A specialist's summary is not evidence that tests passed.
- Tool allowlists restrict capabilities; edit-path and task boundaries are
  instructions, not a filesystem sandbox or a separate checkout.
