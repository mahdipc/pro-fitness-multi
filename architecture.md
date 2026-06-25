# Architecture — Professional Multi-Agent Fitness Planner

## High-Level Flow

```text
User Free Text
   ↓
Profile Understanding Group
   ↓
Safety & Medical Risk Group
   ↓
Goal Reality Group
   ↓
Training Style Group
   ↓
Program Architecture Group
   ↓
Exercise Selection Group
   ↓
Progression Group
   ↓
Nutrition & Body Composition Group
   ↓
Adherence & Lifestyle Group
   ↓
Final QA & Persian Output Group
   ↓
WorkoutPlan.fa.md + DecisionReport.fa.md
```

## Key Principle

The system should not use debate as the only source of truth. Two opposing agents reduce blind spots, but the final decision must be constrained by:

- deterministic safety rules,
- exercise database,
- structured schema validation,
- conflict arbitration,
- conservative defaults when data is missing.

## Recommended Domain Services

```text
IFitnessProfileParser
ISafetyRuleEngine
IProgramRuleEngine
IExerciseLibrary
IProgressionRuleEngine
IAgentRunner
IAgentResultStore
IConflictDetector
IDecisionArbitrator
IPersianMarkdownRenderer
IOutputValidator
```

## Suggested Data Flow Objects

```text
UserFitnessProfile
MissingDataReport
SafetyAssessment
GoalStrategy
TrainingStyleRecommendation
ProgramArchitecture
ExerciseSelectionPlan
ProgressionPlan
NutritionGuidance
AdherencePlan
CriticalReview
FinalWorkoutPlan
DecisionReport
```

## Conflict Handling

Each opposing pair can produce conflicts. Examples:

- AmbitiousGoalAgent wants 5 training days; RealisticGoalAgent wants 3 days.
- VolumeOptimizerAgent wants 16 weekly sets for chest; RecoveryProtectorAgent wants 8-10 due to poor sleep.
- BestExerciseAgent chooses barbell squat; SubstitutionConstraintAgent replaces it due to knee pain.

The DecisionArbitrator must use priority order:

1. Safety
2. Medical red flags
3. User constraints
4. Recovery capacity
5. Training effectiveness
6. User preference
7. Simplicity/adherence

## Final Output Policy

The final user-facing plan should not expose internal debate. It should say what to do.

The decision report should explain:

- what was extracted,
- what was missing,
- what assumptions were made,
- what conflicts happened,
- which decision won and why,
- what would change if missing data becomes available.

