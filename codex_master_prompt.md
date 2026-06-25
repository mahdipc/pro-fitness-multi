# Codex Master Prompt — Professional Multi-Agent Fitness Planner

You are Codex. Build a professional multi-agent fitness planning system.

The system receives a free-text user description and generates two Persian Markdown files:

1. `WorkoutPlan.fa.md`
   - User-facing workout plan in Persian.
   - Clear, realistic, practical, safe, and easy to follow.

2. `DecisionReport.fa.md`
   - Technical Persian report explaining the decisions.
   - Includes extracted data, missing data, assumptions, conflicts between agents, arbitration decisions, safety limits, reasoning summary, and validation results.

## Core Design

The system must use 10 agent groups. Each group contains 2 opposing agents.

Do not let a single LLM response create the whole workout plan. Every agent must return structured data. The Orchestrator must merge the findings and apply deterministic rules.

## Agent Groups

1. Profile Understanding Group
   - `ProfileExtractorAgent`
   - `MissingDataChallengerAgent`

2. Safety & Medical Risk Group
   - `SafetyFirstAgent`
   - `PracticalContinuityAgent`

3. Goal Reality Group
   - `AmbitiousGoalAgent`
   - `RealisticGoalAgent`

4. Training Style Group
   - `StrengthHypertrophyAgent`
   - `ConditioningFatLossAgent`

5. Program Architecture Group
   - `VolumeOptimizerAgent`
   - `RecoveryProtectorAgent`

6. Exercise Selection Group
   - `BestExerciseAgent`
   - `SubstitutionConstraintAgent`

7. Progression Group
   - `ProgressiveOverloadAgent`
   - `FatigueControlAgent`

8. Nutrition & Body Composition Group
   - `PerformanceNutritionAgent`
   - `FatLossNutritionAgent`

9. Adherence & Lifestyle Group
   - `DisciplineCoachAgent`
   - `BehaviorDesignAgent`

10. Final QA & Persian Output Group
   - `CriticalReviewerAgent`
   - `PersianPlanWriterAgent`

## Mandatory Non-LLM Components

Implement or design contracts for:

- `SafetyRuleEngine`
- `ProgramRuleEngine`
- `ProgressionRuleEngine`
- `ExerciseLibrary`
- `OutputSchemaValidator`
- `DecisionArbitrator`

## Hard Rules

- Do not diagnose medical conditions.
- Do not invent medical facts.
- Do not claim guaranteed results.
- Do not create extreme plans for beginners.
- If serious red flags exist, recommend medical evaluation before intense training.
- Every final exercise must include: sets, reps or duration, rest, intensity, target muscles, and alternative.
- Every plan must include warm-up, main workout, optional cardio, cooldown, progression rules, and safety notes.
- Persian user-facing output must be simple and practical.
- Decision report must explain decisions without exposing hidden chain-of-thought. Use decision summaries, assumptions, conflicts, and final arbitration.

## Recommended Workflow

1. Receive `user_description`.
2. Extract structured profile.
3. Detect missing data.
4. Run safety checks.
5. Define goal strategy.
6. Decide weekly structure.
7. Select exercises from ExerciseLibrary only.
8. Apply substitutions and constraints.
9. Apply progression and fatigue rules.
10. Generate draft plan JSON.
11. Run critical review.
12. Fix issues.
13. Write `WorkoutPlan.fa.md` and `DecisionReport.fa.md`.

## Required Internal Output Format

Each agent must return `AgentRunResult` compatible JSON:

```json
{
  "agentName": "string",
  "groupName": "string",
  "stance": "string",
  "findings": [],
  "risks": [],
  "recommendations": [],
  "conflicts": [],
  "confidence": 0.0,
  "requiresHumanReview": false
}
```

## Final Deliverables

Create code/prompt assets so the product can:

- Run every agent independently.
- Store each agent result.
- Compare opposing agents.
- Resolve conflicts using arbitration rules.
- Generate Persian final outputs.

