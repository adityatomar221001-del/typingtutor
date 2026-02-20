# typingtutor

English and Hindi typing tutor focused on smooth, fast performance.

## Recommended stack (C# / .NET)

This repository is currently an early scaffold. If you want to build it using C# and .NET, a practical starting point is:

- **ASP.NET Core** for backend APIs and application hosting.
- **Blazor WebAssembly** (or Blazor Server) for the web UI.
- **Entity Framework Core** for persistence.
- **xUnit** for tests.

## Suggested project structure

```text
typingtutor/
  src/
    TypingTutor.Api/          # ASP.NET Core Web API host
    TypingTutor.App/          # Blazor UI (WASM or Server)
    TypingTutor.Domain/       # Core domain models and rules
    TypingTutor.Application/  # Use cases/services
    TypingTutor.Infrastructure/ # EF Core + external integrations
  tests/
    TypingTutor.Domain.Tests/
    TypingTutor.Application.Tests/
    TypingTutor.Api.Tests/
```

## Core concepts to model first

- **Lesson**: text prompt, language, difficulty.
- **TypingSession**: user attempt metadata (start/end/duration).
- **KeystrokeEvent**: key pressed, expected char, correctness, timestamp.
- **SessionStats**: WPM/CPM, accuracy, error breakdown.

## First milestone (vertical slice)

1. Create one English lesson and one Hindi lesson.
2. Capture keystrokes in the UI and evaluate correctness in real time.
3. Compute basic stats at completion (accuracy + WPM).
4. Save/retrieve completed sessions through API + EF Core.
5. Add tests for scoring logic.

## Performance goals (define early)

To ensure the software feels smooth and fast from the first release, define measurable targets:

- Keystroke-to-UI feedback: **< 16 ms** average on a typical laptop.
- End-of-lesson score computation: **< 100 ms** for standard lesson length.
- API p95 response time for session save/load: **< 200 ms**.
- No UI frame drops while typing at high speed.

Track these in development with simple benchmarks and logs before adding complex features.

## What to learn next

- ASP.NET Core minimal APIs/controllers and dependency injection.
- Blazor component lifecycle and event handling.
- Unicode/text-input handling for Hindi keyboard layouts.
- EF Core migrations and performance basics.
- Clean architecture patterns in .NET (Domain/Application/Infrastructure split).
- .NET performance profiling tools (`dotnet-counters`, `dotnet-trace`, `BenchmarkDotNet`).
