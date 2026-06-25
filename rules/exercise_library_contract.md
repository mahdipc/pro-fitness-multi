# Exercise Library Contract

The Exercise Selection Group must use only approved exercises from the ExerciseLibrary.

## Exercise Object

```json
{
  "id": "string",
  "nameFa": "پرس سینه دستگاه",
  "nameEn": "Machine Chest Press",
  "movementPattern": "horizontal_push",
  "primaryMuscles": ["chest"],
  "secondaryMuscles": ["triceps", "front_delts"],
  "equipment": ["machine"],
  "difficulty": "beginner|intermediate|advanced",
  "riskFlags": ["shoulder_pain"],
  "contraindications": ["acute_shoulder_pain"],
  "alternatives": ["push_up", "dumbbell_floor_press"],
  "instructionsFa": "...",
  "commonMistakesFa": ["..."]
}
```

## Mandatory Fields

- id
- Persian name
- English name
- movement pattern
- primary muscles
- equipment
- difficulty
- alternatives

## Movement Patterns

Recommended normalized values:

```text
squat
hinge
horizontal_push
vertical_push
horizontal_pull
vertical_pull
lunge
carry
core_anti_extension
core_anti_rotation
isolation_biceps
isolation_triceps
isolation_delts
calf
cardio_steady
cardio_interval
mobility
```

## Anti-Hallucination Rule

If an exercise is not in the library, the system must not use it in the final plan.
