---
name: pro-fitness-planner
description: Generate, review, or implement Persian multi-agent fitness workout plans in this repo using local agents, rules, schemas, templates, and the exercise library. Use when the user asks for a workout plan, fitness-planning agent workflow, Codex conversion, or changes to this planner; do not use for unrelated coding tasks.
---

# Pro Fitness Planner

## Purpose

Use this skill to make the repository's multi-agent fitness planner usable from
Codex. The skill coordinates the local domain assets and produces either:

- two Persian Markdown deliverables, `WorkoutPlan.fa.md` and
  `DecisionReport.fa.md`; or
- implementation/review changes to the planner itself.

## Required Source Files

For plan generation or domain behavior changes, load these files first:

1. `codex_master_prompt.md`
2. `architecture.md`
3. `orchestrator/orchestrator_prompt.md`
4. `orchestrator/arbitration_policy.md`
5. `rules/safety_rules.md`
6. `rules/program_rules.md`
7. `rules/progression_rules.md`
8. `rules/exercise_library_contract.md`
9. `rules/anti_hallucination_rules.md`
10. `schemas/AgentRunResult.schema.json`
11. `schemas/AgentFinding.schema.json`
12. `schemas/UserFitnessProfile.schema.json`
13. `schemas/WorkoutPlan.schema.json`
14. `schemas/DecisionReport.schema.json`
15. `templates/WorkoutPlan.fa.template.md`
16. `templates/DecisionReport.fa.template.md`

For a full plan, also load every file in `agents/` in numeric order.

Use `examples/example_exercise_library.seed.json` as the approved exercise
library only when the user does not provide a library. If you use it, disclose
that fallback in the decision report.

## Modes

### Generate A Fitness Plan

Use this when the user provides a `user_description` and asks for a workout
plan, program, fat-loss plan, hypertrophy plan, or Persian output.

Process:

1. Confirm that `user_description` exists. If it is missing, ask for it.
2. Extract a `UserFitnessProfile` from the description.
3. Run the agent groups in the order defined by
   `orchestrator/orchestrator_prompt.md`.
4. Keep each agent output compatible with `AgentRunResult.schema.json`.
5. Apply deterministic safety, program, progression, and anti-hallucination
   rules before accepting an agent recommendation.
6. Detect conflicts between opposing agents.
7. Resolve conflicts with `orchestrator/arbitration_policy.md`.
8. Build validated `WorkoutPlan` and `DecisionReport` objects.
9. Render `WorkoutPlan.fa.md` and `DecisionReport.fa.md`.

If the user asks for files, write both Markdown files to the requested output
directory, or to the repository root if no output directory is specified.

### Review Or Improve The Planner

Use this when the user asks to improve, validate, or change the planner assets.

Process:

1. Preserve the domain-agent files as the source of truth unless a requested
   change explicitly affects them.
2. Keep Codex-specific configuration in `AGENTS.md`, `.agents/skills/`, or
   `.codex/agents/`.
3. Validate schemas and TOML files after edits.
4. Do not remove safety rules, anti-hallucination rules, or conflict
   arbitration requirements.

### Explicit Parallel/Subagent Work

Codex only spawns subagents when the user explicitly asks for subagents,
parallel agents, or one agent per point. When that happens, use the matching
`.codex/agents/*.toml` custom agents.

For broad plan generation, prefer the six group-level custom agents:

- `fitness-profile-safety`
- `fitness-goals-style`
- `fitness-program-exercises`
- `fitness-progression-nutrition`
- `fitness-adherence-review`
- `fitness-persian-writer`

Use the twenty single-role custom agents only when the user explicitly asks for
one Codex subagent per domain agent.

## Hard Constraints

- Do not diagnose medical conditions.
- Do not invent medical facts or user facts.
- Do not claim guaranteed results.
- Do not create extreme plans for beginners.
- Do not select exercises outside the approved exercise library.
- Do not expose hidden chain-of-thought.
- Do not let the Persian writer introduce new decisions; it can only render
  approved structured data.

## Final Response Shape

When files are written, report only:

- which files were created or updated;
- the validation result;
- any important assumptions or missing data.

When answering inline, keep the Persian user-facing plan concise and practical,
then provide a short decision-summary section.

