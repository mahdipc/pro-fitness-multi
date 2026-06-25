# Codex Usage

This repository is now usable from Codex through three native surfaces:

1. `AGENTS.md` for repository-wide guidance that Codex loads automatically.
2. `.agents/skills/pro-fitness-planner/SKILL.md` for the reusable workflow.
3. `.codex/agents/*.toml` for optional custom subagents.

After adding or changing skills or custom agents, start a new Codex session from
the repository root. If a new skill does not appear immediately, restart Codex.

## Normal Use

From the repository root, ask Codex:

```text
Use $pro-fitness-planner.
user_description:
...

Create WorkoutPlan.fa.md and DecisionReport.fa.md in the repo root.
```

The skill loads the local prompts, rules, schemas, templates, and exercise
library seed as needed.

## Implicit Use

The skill also has implicit invocation enabled. A prompt like this should match:

```text
Generate a Persian workout plan and decision report for this user:
...
```

For best reliability, explicit `$pro-fitness-planner` invocation is preferred.

## Parallel/Subagent Use

Codex only starts subagents when you explicitly ask for them. Example:

```text
Use $pro-fitness-planner with parallel subagents.
Spawn one group-level subagent for each planner group, wait for all results,
then arbitrate conflicts and write the two Persian Markdown files.
```

Group-level custom agents:

- `fitness-profile-safety`
- `fitness-goals-style`
- `fitness-program-exercises`
- `fitness-progression-nutrition`
- `fitness-adherence-review`
- `fitness-persian-writer`

Single-role custom agents are also available under `.codex/agents/` when a run
needs one Codex subagent per domain agent.

## Output Contract

Final plan files:

- `WorkoutPlan.fa.md`
- `DecisionReport.fa.md`

The workout plan must be practical Persian. The decision report must include
extracted facts, missing data, assumptions, risks, conflicts, arbitration
decisions, applied rules, and validation notes.

## Safety Contract

- No medical diagnosis.
- No invented user facts.
- No guaranteed results.
- No exercises outside the approved exercise library.
- Red flags require medical evaluation before intense exercise.
- Final Persian rendering cannot introduce new decisions.
