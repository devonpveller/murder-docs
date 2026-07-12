# LogLine

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
protected readonly struct LogLine
```

Nested inside [GameLogger](../../Murder/Diagnostics/GameLogger.html) (`GameLogger.LogLine`), this is the immutable record for a single entry in the debug console's in-memory log buffer.

**Intent:** Stores everything the console overlay needs to render one line — its text, the color it should be tinted with, which `LogType` bucket it belongs to, and how many consecutive identical messages it represents — without game code having to build this itself.

**Use-case:** Created internally by `GameLogger.OutputToLog` every time `GameLogger.Log`, `Warning`, `Error`, `LogPerf`, `LogDebug`, `LogCommand` or `LogCommandOutput` is called, and appended to `GameLogger`'s private `_log` list. When the exact same message is logged again back-to-back, `GameLogger.CheckRepeat` replaces the last `LogLine` with a copy (`with { Repeats = lastLog.Repeats + 1 }`) instead of appending a new one, so the console can collapse spam into a single "message (x5)"-style line. `GameLogger.FetchLogs()` projects the stored `LogLine`s down to their `Message` strings for consumers that only need the text; the console overlay itself reads the full `LogLine` (including `Color` and `Type`) to draw each line.

### ⭐ Properties

#### Color

```csharp
public Vector4 Color { init; get; }
```

RGBA color used to tint this log entry in the console UI. Each logging method picks its own tint — e.g. warnings use a pale yellow, errors a red/magenta, debug messages a translucent white — so the severity of a line is visible at a glance.

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Message

```csharp
public string Message { init; get; }
```

The text content of this log entry, already formatted (including the `[HH:mm:ss]` timestamp prefix for most log types) and split so that each `LogLine` holds exactly one line of text, even if the original logged string contained embedded newlines.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Repeats

```csharp
public int Repeats { init; get; }
```

Number of times this exact message has been logged consecutively. Starts at `1` when the line is first created and is incremented by `GameLogger.CheckRepeat` each time the same message is logged again immediately afterward, letting the console collapse duplicate spam into one line instead of flooding the log.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Type

```csharp
public GameLogger.LogType Type { init; get; }
```

Which category of message this line is (`Log`, `Debug`, `Perf`, `Warning`, `Error` or `Command`), set by whichever `GameLogger` method produced it. The console overlay uses this alongside `Color` to decide how to render or filter the line.

**Returns** \
[GameLogger.LogType](../../Murder/Diagnostics/GameLogger.html) \

⚡
