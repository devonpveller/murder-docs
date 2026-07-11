# LogLine

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
sealed struct LogLine
```

Represents a single entry in the debug console log, with its display color, message text, and a repeat counter.

**Intent:** Stores the data for one console output line so the logger UI can render it with the correct color and collapse repeated identical messages.

**Use-case:** Returned in batches by `GameLogger.FetchLogs()` for display in the in-game console; not typically created by game code directly.

### ⭐ Properties
#### Color
```csharp
public Vector4 Color { get; public set; }
```
RGBA color used to tint this log entry in the console UI (e.g. red for errors, yellow for warnings).

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \
#### Message
```csharp
public string Message { get; public set; }
```
The text content of this log entry.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### Repeats
```csharp
public int Repeats { get; public set; }
```
Number of times this exact message has been logged consecutively; used to collapse duplicate entries.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡