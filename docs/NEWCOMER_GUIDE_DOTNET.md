# Newcomer Guide (C#/.NET)

## High-level architecture

For this project, think in terms of **typing engine + lesson content + progress tracking**.

- `Domain`: pure typing logic (accuracy, WPM, error categories).
- `Application`: orchestrates use-cases (start lesson, submit keystroke, finish session).
- `Infrastructure`: persistence and adapters (EF Core repositories, external services).
- `API/UI`: exposes functionality to web clients (Blazor + ASP.NET Core).

## Important implementation details

### 1) Keep typing logic framework-agnostic

Accuracy/WPM/error calculations should live in `Domain` so they are easy to test and reuse.

### 2) Treat Hindi support as first-class

Design lesson and keystroke models to be Unicode-safe from day one.
Avoid assumptions that one key = one ASCII char.

### 3) Build for feedback latency

Typing tutor UX depends on fast visual response. Keep per-keystroke processing lightweight.

Practical guidance:

- Run scoring incrementally instead of recalculating the whole string each keypress.
- Avoid heavy allocations in hot paths (prefer spans/pooled buffers where appropriate).
- Use async APIs for persistence; keep typing loop CPU-only and local.
- Batch non-critical telemetry writes so they do not block the typing experience.

### 4) Persist useful telemetry

Store enough session data to support future analytics:

- error hotspots,
- frequent substitutions,
- progress over time,
- language-specific performance.

### 5) Set explicit performance budgets

Define and enforce targets so “smooth and fast” is testable:

- Input feedback loop: target under 16 ms average.
- Scoring service: target under 100 ms per completed lesson.
- API persistence endpoints: target p95 under 200 ms.

Add lightweight performance checks in CI once the first vertical slice is complete.

## Recommended learning path

1. Scaffold solution and projects (`dotnet new sln`, `dotnet new webapi`, `dotnet new blazorwasm`).
2. Implement scoring engine in Domain with unit tests first.
3. Build one lesson page in Blazor with real-time highlighting.
4. Add API endpoints for session persistence.
5. Add migration + DB.
6. Introduce adaptive difficulty and more lesson types.

## Practical next tasks

- Add `TypingSession` aggregate and scoring service.
- Implement a `/api/sessions` POST endpoint.
- Create Blazor typing component that reports per-keystroke state.
- Add tests for tricky Unicode comparison scenarios.
- Add a microbenchmark project for scoring and text-comparison hot paths.
- Add a simple load test script for session APIs.
