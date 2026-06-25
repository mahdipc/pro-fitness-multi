# Anti-Hallucination Rules

## Core Rules

- Do not invent user facts.
- Do not invent exercises.
- Do not invent medical clearance.
- Do not invent equipment access.
- Do not invent exact calorie needs without input or calculator.
- Do not promise guaranteed outcomes.
- Do not claim a plan is medically safe for a disease.

## Evidence Tags

Every important finding should have one of these basis types:

```text
user_input
rule_engine
exercise_library
calculation
assumption
agent_inference
```

If the basis is `assumption` or `agent_inference`, the DecisionReport must mention it.

## Missing Data Policy

When data is missing:

- use conservative defaults;
- mark assumptions;
- show what would change if the data became available;
- avoid over-specific prescriptions.

## Final Writer Restriction

The PersianPlanWriterAgent is not allowed to introduce new decisions. It can only render approved structured data.
