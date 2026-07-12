# PerfTimeRecorder

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class PerfTimeRecorder : IDisposable
```

Disposable timing helper that logs the elapsed wall-clock time of an operation when disposed.

**Intent:** Wraps a named operation in a `using` block to automatically log how many seconds it took when the block exits, without every call site having to manually capture a start timestamp and compute/format the elapsed time itself.

**Use-case:** Write `using var _ = new PerfTimeRecorder("Load assets");` around any performance-sensitive block; when the block (or method) exits and `_` goes out of scope, `Dispose()` fires and reports `Completed 'Load assets' in 0.123 s.` to [GameLogger.LogPerf](../../Murder/Diagnostics/GameLogger.html), which shows up in the debug console with a distinct "📈" marker. This is the standard, low-ceremony way to instrument arbitrary code for perf logging in Murder.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public PerfTimeRecorder(string name)
```

Starts timing an operation named `name`, capturing the current time as the start. The name is included in the log message written when this recorder is disposed.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### Dispose()

```csharp
public void Dispose()
```

Ends the timed operation and reports the elapsed time (in seconds, to millisecond precision) via `GameLogger.LogPerf`. Called automatically at the end of the enclosing `using` block/statement — it is not meant to be called manually.

⚡
