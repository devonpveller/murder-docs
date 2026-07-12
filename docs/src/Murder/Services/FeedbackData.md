# FeedbackData

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public readonly struct FeedbackData
```

The high-level input to [FeedbackServices](../../Murder/Services/FeedbackServices.html)`.SendSaveDataFeedbackAsync` — the player-facing feedback message plus optional screenshots. Declared as a nested type of `FeedbackServices`.

**Intent:** Separates what a *caller* (e.g. an in-game feedback form) needs to supply from the lower-level `RawFeedbackData` that actually gets posted over HTTP; `SendSaveDataFeedbackAsync` is responsible for turning a `FeedbackData` into a fully-populated `RawFeedbackData` (attaching save files, crash log, and session log automatically).

**Use-case:** Construct a `FeedbackData` from a feedback form's message/description text and (optionally) one or more captured `ScreenshotFeedbackData` values from `TryGetGameplayScreenshot`/`TryGetScreenshot`, then pass it to `SendSaveDataFeedbackAsync`.

### ⭐ Constructors

```csharp
public FeedbackData()
```

Creates a `FeedbackData` with all fields at their defaults (empty strings, `MachineId` of `0`, no screenshots). Since every property is `init`-only, use object-initializer syntax (`new FeedbackData { Name = ..., Description = ... }`) to populate it.

### ⭐ Properties

#### Description

```csharp
public readonly string Description { get; init; }
```

The body of the player's feedback message — the detailed explanation of the bug or comment being submitted.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### MachineId

```csharp
public readonly int MachineId { get; init; }
```

A seed used to derive an anonymous, human-readable computer name via `FeedbackServices.GenerateFunnyName`, so the submitted feedback title can identify (without exposing real machine info) which device it came from.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Name

```csharp
public readonly string Name { get; init; }
```

A short title/summary for the feedback, used to build the submission's `Title` field alongside the generated computer name.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Screenshots

```csharp
public readonly ScreenshotFeedbackData?[]? Screenshots { get; init; }
```

Optional array of captured screenshots to attach to the submission (from `TryGetGameplayScreenshot`/`TryGetScreenshot`). Each entry's underlying `Texture` is disposed by `SendSaveDataFeedbackAsync` once the request completes.

**Returns** \
[ScreenshotFeedbackData?[]?](../../Murder/Services/ScreenshotFeedbackData.html) \

#### Version

```csharp
public readonly string Version { get; init; }
```

The game version string to record alongside the feedback submission, useful for triaging reports against a specific build.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
