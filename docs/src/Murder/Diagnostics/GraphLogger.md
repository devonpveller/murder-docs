# GraphLogger

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class GraphLogger
```

Implement this for plotting graphs into the debug system.

**Intent:** Records time-series performance metrics and renders them as overlay graphs in the debug view.

**Use-case:** Subclass and override plotting methods to capture custom per-frame metrics; the diagnostics overlay will draw them as live graphs.

### ⭐ Constructors
```csharp
public GraphLogger()
```
Creates a new graph logger with no active plots.

### ⭐ Methods
#### ClearAllGraphs()
```csharp
public virtual void ClearAllGraphs()
```
Removes all plotted graph data across every tracked file.

#### ClearGraph(string)
```csharp
public virtual void ClearGraph(string callerFilePath)
```
Clears the graph data recorded for the given source file.

**Parameters** \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PlotGraph(float, int, string)
```csharp
public virtual void PlotGraph(float value, int max, string callerFilePath)
```
Records `value` against a maximum of `max` for the graph associated with `callerFilePath`.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PlotGraph(float, string)
```csharp
public virtual void PlotGraph(float value, string callerFilePath)
```
Records `value` for the graph associated with `callerFilePath` without an explicit maximum.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡