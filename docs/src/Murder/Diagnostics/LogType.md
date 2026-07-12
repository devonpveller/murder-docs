# LogType

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public enum LogType : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Nested inside [GameLogger](../../Murder/Diagnostics/GameLogger.html) (`GameLogger.LogType`), this is the category tag stored on every [LogLine](../../Murder/Diagnostics/LogLine.html) entry.

**Intent:** Lets the console overlay tell log lines apart (an ordinary message vs. a warning vs. a command echo, etc.) beyond just their `Color`, so it can style or filter them accordingly. Each `GameLogger` logging method (`Log`, `LogDebug`, `LogPerf`, `Warning`, `Error`, `LogCommand`/`LogCommandOutput`) tags the `LogLine` it produces with the matching `LogType` value.

**Use-case:** Not something game code sets directly — it's assigned internally by whichever `GameLogger` method was used to emit the message. Code that inspects `LogLine.Type` (e.g. a custom console renderer) can use it to decide how to draw or filter a given entry.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Log

```csharp
public static const LogType Log;
```

An ordinary message logged via `GameLogger.Log(string, Color?)`/`GameLogger.Log(string, Vector4)`.

**Returns** \
[LogType](../../Murder/Diagnostics/LogType.html) \

#### Debug

```csharp
public static const LogType Debug;
```

A developer-only message logged via `GameLogger.LogDebug(string)`; only ever produced in `DEBUG` builds, since `LogDebug` compiles to a no-op otherwise.

**Returns** \
[LogType](../../Murder/Diagnostics/LogType.html) \

#### Perf

```csharp
public static const LogType Perf;
```

A performance-timing message logged via `GameLogger.LogPerf(string, Vector4?)`, typically emitted by [PerfTimeRecorder](../../Murder/Diagnostics/PerfTimeRecorder.html) when a timed `using` block completes.

**Returns** \
[LogType](../../Murder/Diagnostics/LogType.html) \

#### Warning

```csharp
public static const LogType Warning;
```

A warning logged via `GameLogger.Warning(string, string, int)`, including assertion failures raised by `GameLogger.Verify(bool, string)`.

**Returns** \
[LogType](../../Murder/Diagnostics/LogType.html) \

#### Error

```csharp
public static const LogType Error;
```

An error logged via `GameLogger.Error(string, string, int)`. Logging an entry of this type also forces the debug console overlay open, so errors are never missed.

**Returns** \
[LogType](../../Murder/Diagnostics/LogType.html) \

#### Command

```csharp
public static const LogType Command;
```

A console command echo or its output, logged via `GameLogger.LogCommand(string)`/`GameLogger.LogCommandOutput(string)` when the player runs a [CommandServices](../../Murder/Diagnostics/CommandServices.html) command.

**Returns** \
[LogType](../../Murder/Diagnostics/LogType.html) \

⚡
