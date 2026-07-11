# PerfTimeRecorder

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class PerfTimeRecorder : IDisposable
```

Disposable timing helper that logs the elapsed time of an operation when disposed.

**Intent:** Wraps a named operation in a `using` block to automatically log how many seconds it took when the block exits.

**Use-case:** Use `using var _ = new PerfTimeRecorder("Load assets")` around any performance-sensitive block to emit a timing message to `GameLogger` on completion.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
public PerfTimeRecorder(string name)
```
Creates a new recorder for the named operation and records the current time as the start.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods
#### Dispose()
```csharp
public virtual void Dispose()
```
Logs the elapsed time since construction to `GameLogger.LogPerf`.



⚡