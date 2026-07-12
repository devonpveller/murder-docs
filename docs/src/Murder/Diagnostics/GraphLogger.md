# GraphLogger

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class GraphLogger
```

Implement this for plotting graphs into the debug system.

**Intent:** Defines the extension point for time-series performance/debug graphs. Every method here is `virtual` and empty in the base class — `GraphLogger` on its own records nothing and draws nothing; it exists purely so [Game](../../Murder/Game.html)'s `GraphLogger` property has a safe, always-present default in plain game builds. All of the real work happens in a subclass: Murder.Editor's internal `EditorGraphLogger` overrides every method to accumulate per-caller-file `float` samples in a dictionary and expose them for the diagnostics overlay to plot.

**Use-case:** Game code never calls these methods directly — instead call `GameLogger.PlotGraph(value)` (or the `(value, max)` overload) from wherever a per-frame value should be visualized, and `GameLogger` forwards to `Game.Instance.GraphLogger` for you. To customize how graphs are captured or rendered, replace `Game.GraphLogger` (via its `virtual` getter) with your own `GraphLogger` subclass and override `PlotGraph`/`ClearGraph`/`ClearAllGraphs`.

### ⭐ Constructors

```csharp
public GraphLogger()
```

Creates a new graph logger with no active plots. The base constructor does no setup — it exists only because a subclass (or `Game`'s default `= new GraphLogger()` field initializer) needs something to instantiate.

### ⭐ Methods

#### ClearAllGraphs()

```csharp
public virtual void ClearAllGraphs()
```

Removes all plotted graph data across every tracked file. The base implementation is a no-op; overridden by `EditorGraphLogger` to clear its internal graph dictionary. Reached via `GameLogger.ClearAllGraphs()`.

#### ClearGraph(string)

```csharp
public virtual void ClearGraph(string callerFilePath)
```

Clears the graph data recorded for the given source file. The base implementation is a no-op; overridden by `EditorGraphLogger` to remove the entry keyed by the file name derived from `callerFilePath`. Reached via `GameLogger.ClearGraph(string)`, which supplies `callerFilePath` automatically via `[CallerFilePath]`.

**Parameters** \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PlotGraph(float, int, string)

```csharp
public virtual void PlotGraph(float value, int max, string callerFilePath)
```

Records `value` against a maximum of `max` for the graph associated with `callerFilePath`. The base implementation is a no-op; `EditorGraphLogger`'s override resets its sample buffer whenever it grows past `max` samples, effectively giving a fixed-width rolling graph. Reached via `GameLogger.PlotGraph(float, int, string)`.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PlotGraph(float, string)

```csharp
public virtual void PlotGraph(float value, string callerFilePath)
```

Records `value` for the graph associated with `callerFilePath` without an explicit maximum, so the sample buffer grows unbounded. The base implementation is a no-op; reached via `GameLogger.PlotGraph(float, string)`.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

⚡
