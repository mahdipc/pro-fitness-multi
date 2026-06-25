# .NET Implementation Contracts

This file gives Codex a recommended .NET-friendly structure.

## Suggested Project Structure

```text
src/
├── FitnessPlanner.Api/
├── FitnessPlanner.Application/
│   ├── Agents/
│   ├── Orchestration/
│   ├── Rules/
│   ├── ExerciseLibrary/
│   └── Rendering/
├── FitnessPlanner.Domain/
│   ├── Profiles/
│   ├── Plans/
│   ├── AgentRuns/
│   └── Exercises/
└── FitnessPlanner.Infrastructure/
    ├── Llm/
    ├── Storage/
    └── Markdown/
```

## Recommended Interfaces

```csharp
public interface IFitnessAgent
{
    string Name { get; }
    string GroupName { get; }
    Task<AgentRunResult> RunAsync(AgentContext context, CancellationToken cancellationToken);
}

public interface IAgentOrchestrator
{
    Task<WorkoutPlanningResult> CreatePlanAsync(string userDescription, CancellationToken cancellationToken);
}

public interface ISafetyRuleEngine
{
    SafetyAssessment Evaluate(UserFitnessProfile profile);
}

public interface IProgramRuleEngine
{
    ProgramConstraints BuildConstraints(UserFitnessProfile profile, SafetyAssessment safety);
}

public interface IExerciseLibrary
{
    Task<IReadOnlyList<Exercise>> SearchAsync(ExerciseSearchCriteria criteria, CancellationToken cancellationToken);
    Task<Exercise?> GetByIdAsync(string id, CancellationToken cancellationToken);
}

public interface IProgressionRuleEngine
{
    ProgressionPlan BuildProgression(UserFitnessProfile profile, ProgramArchitecture architecture);
}

public interface IDecisionArbitrator
{
    ArbitrationResult Resolve(IReadOnlyList<AgentRunResult> agentResults, ProgramConstraints constraints);
}

public interface IPersianMarkdownRenderer
{
    string RenderWorkoutPlan(WorkoutPlan plan);
    string RenderDecisionReport(DecisionReport report);
}
```

## Key Records

```csharp
public sealed record AgentRunResult(
    string AgentName,
    string GroupName,
    string Stance,
    IReadOnlyList<AgentFinding> Findings,
    IReadOnlyList<string> Risks,
    IReadOnlyList<string> Recommendations,
    IReadOnlyList<AgentConflict> Conflicts,
    double Confidence,
    bool RequiresHumanReview);

public sealed record AgentFinding(
    string Claim,
    string Basis,
    double Confidence,
    string? Notes);

public sealed record AgentConflict(
    string? WithAgent,
    string Topic,
    string Description,
    string Severity);
```

## Implementation Notes

- Store every `AgentRunResult` for auditability.
- Validate JSON outputs before moving to the next group.
- Retry malformed LLM output once with a repair prompt.
- Never let the Persian renderer introduce new decisions.
- Keep medical red-flag rules deterministic.
- Use cancellation tokens for every agent call.
