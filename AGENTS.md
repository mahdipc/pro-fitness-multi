# AGENTS.md

## Repository Purpose

This repository is a Codex-ready package for a professional multi-agent fitness
planner. It converts a free-text `user_description` into two Persian Markdown
deliverables:

- `WorkoutPlan.fa.md`
- `DecisionReport.fa.md`

Use the local agent prompts, deterministic rules, schemas, templates, and
approved exercise library as the source of truth.

## Codex Entry Points

- Use `.agents/skills/pro-fitness-planner/SKILL.md` for plan generation,
  domain review, and implementation work related to this planner.
- Treat `agents/*.md` as the product's domain-agent prompt assets.
- Treat `.codex/agents/*.toml` as optional Codex custom subagents. They are
  available only when the user explicitly asks for parallel/subagent work.
- Do not assume that files under `agents/` are automatically spawned by Codex.
  They must be loaded by the skill, the orchestrator, or a custom agent wrapper.

## Domain Safety

- Do not diagnose medical conditions.
- Do not invent medical facts, injuries, equipment, age, height, weight, or
  training history.
- If serious red flags are present, recommend medical evaluation before intense
  exercise and keep programming conservative.
- Use only approved exercise-library entries for exercise selection.
- Label missing data and assumptions clearly in the decision report.
- Do not expose hidden chain-of-thought. Use concise decision summaries,
  assumptions, conflicts, and arbitration outcomes.

## Planning Workflow

When generating a fitness plan:

1. Read `codex_master_prompt.md`, `architecture.md`, and
   `orchestrator/orchestrator_prompt.md`.
2. Read all relevant files in `rules/`.
3. Read the needed schemas in `schemas/`.
4. Read every relevant `agents/*.md` file for the requested workflow.
5. Use `examples/example_exercise_library.seed.json` only when no approved
   library is provided, and disclose that fallback in `DecisionReport.fa.md`.
6. Produce structured intermediate summaries compatible with
   `schemas/AgentRunResult.schema.json`.
7. Resolve conflicts using `orchestrator/arbitration_policy.md`.
8. Render final outputs using the templates in `templates/`.

## Output Requirements

- The user-facing plan must be simple, practical Persian.
- Every final exercise must include sets, reps or duration, rest, intensity,
  target muscles, and an alternative.
- Every final plan must include warm-up, main workout, optional cardio,
  cooldown, progression rules, and safety notes.
- The decision report must include extracted facts, missing data, assumptions,
  risks, conflicts, applied rules, arbitration decisions, and validation notes.

