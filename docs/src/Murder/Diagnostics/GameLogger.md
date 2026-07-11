# GameLogger

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class GameLogger
```

Singleton debug console and logging system for the Murder engine.

**Intent:** Provides the central interface for emitting log messages, performance data, and rendering an in-game debug console that can parse and dispatch `CommandServices` commands.

**Use-case:** Call `GameLogger.Log`, `GameLogger.Warning`, or `GameLogger.Error` to emit messages; call `DrawConsole` each frame (in debug mode) to render the interactive console overlay.

### ⭐ Constructors
```csharp
protected GameLogger()
```

This is a singleton.

### ⭐ Properties
#### _instance
```csharp
protected static GameLogger _instance;
```
The singleton instance; created lazily via `GetOrCreateInstance()`.

**Returns** \
[GameLogger](../../Murder/Diagnostics/GameLogger.html) \
#### _lastInputIndex
```csharp
protected int _lastInputIndex;
```
Current index into `_lastInputs` for navigating command history with the up/down arrows.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### _lastInputs
```csharp
protected readonly String[] _lastInputs;
```

These are for supporting ^ functionality in console. Fancyy....

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
#### _log
```csharp
protected readonly List<T> _log;
```
In-memory list of all `LogLine` entries accumulated during the session.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \
#### _resetInputFocus
```csharp
protected bool _resetInputFocus;
```
When `true`, the console input field will be re-focused on the next draw frame.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### _scrollToBottom
```csharp
protected int _scrollToBottom;
```
Counter used to force the console output to scroll to the most recent entry for the next N frames.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### _showDebug
```csharp
protected bool _showDebug;
```
Whether the debug console overlay is currently visible.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### _traceCount
```csharp
protected static const int _traceCount;
```
Number of stack frames included when logging exception traces.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### IsShowing
```csharp
public static bool IsShowing { get; }
```
Returns `true` if the debug console overlay is currently open and visible.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Methods
#### Input(Func<T, TResult>)
```csharp
protected virtual void Input(Func<T, TResult> onInputAction)
```

Receive input from the user. Called when a console is displayed.

**Parameters** \
`onInputAction` [Func\<T, TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \

#### LogText(bool)
```csharp
protected virtual void LogText(bool copy)
```

Log text in the console display. Called when a console is displayed.

**Parameters** \
`copy` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TopBar(Boolean&)
```csharp
protected virtual void TopBar(Boolean& copy)
```
Renders the top toolbar of the console window; override to customize toolbar content.

**Parameters** \
`copy` [bool&](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ClearLog()
```csharp
protected void ClearLog()
```
Clears all entries from the in-memory log list.

#### LogCommand(string)
```csharp
protected void LogCommand(string msg)
```
Appends `msg` to the log with the command-input styling.

**Parameters** \
`msg` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### LogCommandOutput(string)
```csharp
protected void LogCommandOutput(string msg)
```
Appends `msg` to the log with the command-output styling.

**Parameters** \
`msg` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### CaptureCrash(Exception, string)
```csharp
public bool CaptureCrash(Exception _, string logFile)
```

Used to filter exceptions once a crash is yet to happen.

**Parameters** \
`_` [Exception](https://learn.microsoft.com/en-us/dotnet/api/System.Exception?view=net-7.0) \
`logFile` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetOrCreateInstance()
```csharp
public GameLogger GetOrCreateInstance()
```
Returns the existing singleton instance or creates a new one if none exists.

**Returns** \
[GameLogger](../../Murder/Diagnostics/GameLogger.html) \

#### FetchLogs()
```csharp
public ImmutableArray<T> FetchLogs()
```
Returns an immutable snapshot of all log message strings accumulated so far.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetCurrentLog()
```csharp
public string GetCurrentLog()
```
Returns all log entries concatenated into a single newline-delimited string.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DrawConsole(Func<T, TResult>)
```csharp
public virtual void DrawConsole(Func<T, TResult> onInputAction)
```

Draws the console of the game.

**Parameters** \
`onInputAction` [Func\<T, TResult\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \

#### TrackImpl(string, Object)
```csharp
public virtual void TrackImpl(string variableName, Object value)
```
Records a named variable value for live display in the debug overlay.

**Parameters** \
`variableName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

#### ClearAllGraphs()
```csharp
public void ClearAllGraphs()
```
Removes all tracked graph data from all registered graph loggers.

#### ClearGraph(string)
```csharp
public void ClearGraph(string callerFilePath)
```
Clears the graph data for the file identified by `callerFilePath`.

**Parameters** \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Error(string, string, int)
```csharp
public void Error(string msg, string memberName, int lineNumber)
```
Emits an error message tagged with the caller's member name and line number.

**Parameters** \
`msg` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`memberName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`lineNumber` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Fail(string)
```csharp
public void Fail(string message)
```

This will fail a given message and paste it in the log.

**Parameters** \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Initialize(bool)
```csharp
public void Initialize(bool diagnostic)
```
Sets up the logger; when `diagnostic` is `true`, hooks into `AppDomain.FirstChanceException` to log unhandled exceptions.

**Parameters** \
`diagnostic` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Log(string, Vector4)
```csharp
public void Log(string v, Vector4 color)
```
Emits a log message with the given RGBA color tint.

**Parameters** \
`v` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`color` [Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### Log(string, T?)
```csharp
public void Log(string v, T? color)
```
Emits a log message with an optional color tint.

**Parameters** \
`v` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`color` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### LogPerf(string, T?)
```csharp
public void LogPerf(string v, T? color)
```
Emits a performance-timing message, displayed with a distinct styling in the console.

**Parameters** \
`v` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`color` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### PlotGraph(float, int, string)
```csharp
public void PlotGraph(float point, int max, string callerFilePath)
```
Forwards a data point with an explicit maximum to the registered `GraphLogger` for the calling file.

**Parameters** \
`point` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PlotGraph(float, string)
```csharp
public void PlotGraph(float point, string callerFilePath)
```
Forwards a data point to the registered `GraphLogger` for the calling file.

**Parameters** \
`point` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Toggle(bool)
```csharp
public void Toggle(bool value)
```
Shows or hides the debug console overlay.

**Parameters** \
`value` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ToggleDebugWindow()
```csharp
public void ToggleDebugWindow()
```
Flips the visibility of the debug console overlay and resets focus when opening.

#### Track(string, Object)
```csharp
public void Track(string variableName, Object value)
```
Records a named variable for live display in the debug overlay; delegates to `TrackImpl`.

**Parameters** \
`variableName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

#### Verify(bool, string)
```csharp
public void Verify(bool condition, string message)
```

This will verify a condition. If false, this will paste <paramref name="message" /> in the log.

**Parameters** \
`condition` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Verify(bool)
```csharp
public void Verify(bool condition)
```

This will verify a condition. If false, this will paste in the log.

**Parameters** \
`condition` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Warning(string, string, int)
```csharp
public void Warning(string msg, string memberName, int lineNumber)
```
Emits a warning message tagged with the caller's member name and line number.

**Parameters** \
`msg` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`memberName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`lineNumber` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡