# Arbitration Policy

## Purpose

This document defines how the Orchestrator resolves conflicts between opposing agents.

## Priority Order

1. Safety wins over performance.
2. Medical red flags win over user ambition.
3. Real user constraints win over ideal programming.
4. Recovery capacity wins over high volume.
5. Exercise availability wins over theoretical best exercise.
6. Adherence wins over complex perfection.
7. If two plans are similarly effective, choose the simpler plan.

## Conflict Categories

### Safety Conflict

Example:
- BestExerciseAgent recommends heavy deadlift.
- SafetyFirstAgent flags acute lower-back pain.

Decision:
- Remove heavy deadlift.
- Use safer hinge alternatives only if pain status allows.
- Add safety note.

### Volume Conflict

Example:
- VolumeOptimizerAgent recommends 18 weekly sets.
- RecoveryProtectorAgent recommends 8-10 due to poor sleep.

Decision:
- Start with lower/moderate volume.
- Add progression rule to increase volume later.

### Goal Conflict

Example:
- AmbitiousGoalAgent plans aggressive fat loss.
- RealisticGoalAgent says timeline is unrealistic.

Decision:
- Use realistic timeline.
- Keep ambitious milestones as optional, not guaranteed.

### Exercise Conflict

Example:
- BestExerciseAgent selects pull-up.
- SubstitutionConstraintAgent says user cannot perform pull-ups.

Decision:
- Use lat pulldown or assisted pull-up.

## Output Requirements

For every important conflict, write a short entry in `DecisionReport.fa.md`:

- Conflict
- Agents involved
- Final decision
- Reason
