# GameLogger

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class GameLogger
```

Singleton entry point for the engine's logging and in-game debug console.

**Intent:** Game code calls the static `Log`/`Warning`/`Error`/`LogPerf`/`LogDebug` family of methods to emit messages, which are buffered in-memory as `LogLine` entries. Where the console overlay is drawn (`DrawConsole`, overridden by Murder.Editor's `EditorGameLogger`), those entries are rendered as a scrollable, colored log with a text input for dispatching [CommandServices](../../Murder/Diagnostics/CommandServices.html) commands. The base `GameLogger` shipped in `Murder.dll` is intentionally inert for anything UI-related — `DrawConsole`, `TopBar`, `LogText` and `Input` are all no-ops — so a plain game build still gets a working log buffer and crash-log capture without pulling in any ImGui/rendering dependency; only the editor's subclass actually paints the console window.

**Use-case:** Call `GameLogger.Log(msg)`, `GameLogger.Warning(msg)` or `GameLogger.Error(msg)` anywhere in game code to emit a message; call `GameLogger.LogPerf`/`PlotGraph` for performance diagnostics; call `GameLogger.Toggle(true)`/`DrawConsole` (typically wired to a debug-only input binding) to show the interactive console overlay. `GameLogger.Verify`/`Fail` are the engine's lightweight assertion helpers — prefer them over throwing when a bad state should be surfaced to a developer without crashing the game outright.

### ⭐ Constructors

```csharp
protected GameLogger()
```

This is a singleton.

The constructor is `protected` specifically so that Murder.Editor can define a subclass and swap it in as `_instance` before any logging happens, while game code can never construct a `GameLogger` directly — the only way to obtain one is `GetOrCreateInstance()`.

### ⭐ Properties

#### \_instance

```csharp
protected static GameLogger _instance;
```

The singleton instance; created lazily via `GetOrCreateInstance()`. Murder.Editor overwrites this with an instance of its own `GameLogger` subclass during start-up so that all of the static logging methods transparently gain a real console UI and variable-tracking overlay.

**Returns** \
[GameLogger](../../Murder/Diagnostics/GameLogger.html) \

#### \_lastInputIndex

```csharp
protected int _lastInputIndex;
```

Current write index into `_lastInputs`, incremented every time a command is submitted via `LogCommand`. Used together with `_lastInputs` to implement command-history recall (pressing up/down in the console input) in the editor's console UI.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### \_lastInputs

```csharp
protected readonly String[] _lastInputs;
```

These are for supporting ^ functionality in console. Fancyy.... A fixed-size (1024 entry) ring buffer of previously submitted console commands, written to by `LogCommand` each time the player runs a command, so the console UI can let the player cycle back through their command history.

**Returns** \
[string[]](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### \_log

```csharp
protected readonly List<LogLine> _log;
```

In-memory list of every `LogLine` entry accumulated during the session, in chronological order. This is the backing store for `FetchLogs()`, `GetCurrentLog()`, and the console overlay's scrollback; `ClearLog()` empties it.

**Returns** \
[List\<LogLine\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### \_resetInputFocus

```csharp
protected bool _resetInputFocus;
```

When `true`, the console input field will be re-focused on the next draw frame. Set whenever the console overlay is opened via `ToggleDebugWindow`, so the player can start typing a command immediately without clicking into the text field first.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### \_scrollToBottom

```csharp
protected int _scrollToBottom;
```

Counter used to force the console output to scroll to the most recent entry for the next few draw frames. Bumped to `2` every time a new line is logged or the console is opened, and decremented by the UI as it consumes it, so new output stays visible even while the player is scrolled to the bottom.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### \_showDebug

```csharp
protected bool _showDebug;
```

Whether the debug console overlay is currently visible. Backs the public `IsShowing` property and is flipped by `Toggle`/`ToggleDebugWindow`; also forced to `true` automatically whenever `Error` is called, so errors are never logged silently off-screen.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### \_traceCount

```csharp
protected static const int _traceCount;
```

Number of stack frames (`7`) included when `Verify` builds the callstack it prints for a failed assertion. Bounds how much of the stack trace is dumped into the log so a single failed `Verify` doesn't flood the console with dozens of frames.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### IsShowing

```csharp
public static bool IsShowing { get; }
```

Returns `true` if the debug console overlay is currently open and visible. Reads `_showDebug` off the singleton instance, or `false` if no instance has been created yet.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

### ⭐ Methods

#### Input(Func\<string, string\>?)

```csharp
protected virtual void Input(Func<string, string>? onInputAction)
```

Receive input from the user. Called when a console is displayed. The base implementation is a no-op; `onInputAction` (typically `CommandServices.Parse`) is provided by the caller of `DrawConsole` and is meant to be invoked by an overriding console UI once the player submits a line of text.

**Parameters** \
`onInputAction` [Func\<string, string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \

#### LogText(bool)

```csharp
protected virtual void LogText(bool copy)
```

Log text in the console display. Called when a console is displayed. The base implementation is a no-op; overridden by the editor's console to render the scrollback of `_log` entries, and to copy the visible text to the clipboard when `copy` is `true`.

**Parameters** \
`copy` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TopBar(bool&)

```csharp
protected virtual void TopBar(ref bool copy)
```

Shows the top bar of the console. Called when a console is displayed. The base implementation is a no-op; overridden by the editor's console to render toolbar controls (such as a "copy log" button, which sets `copy` to request that `LogText` copy its contents).

**Parameters** \
`copy` [bool&](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ClearLog()

```csharp
protected void ClearLog()
```

Removes every entry from the in-memory log list. Used by the console UI's "clear" action to reset the scrollback without affecting future logging.

#### LogCommand(string)

```csharp
protected void LogCommand(string msg)
```

Appends `msg` to the log styled as a command the player typed into the console (prefixed with `> ` and tinted green), and records it in the `_lastInputs` history ring buffer so it can be recalled later. Called by the console UI right before dispatching input to `CommandServices.Parse`.

**Parameters** \
`msg` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### LogCommandOutput(string)

```csharp
protected void LogCommandOutput(string msg)
```

Appends `msg` to the log styled as the result of a console command, without a timestamp prefix. Called by the console UI with whatever string `CommandServices.Parse` returns.

**Parameters** \
`msg` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### CaptureCrash()

```csharp
public static void CaptureCrash()
```

Used to filter exceptions once a crash is yet to happen. Dumps the entire current log (see `GetCurrentLog()`) to the crash log file at `GetCrashLogPath()`, so it can be inspected or attached to a bug report after the game exits unexpectedly. Takes no arguments and returns nothing — it writes directly to disk.

#### GetOrCreateInstance()

```csharp
public static GameLogger GetOrCreateInstance()
```

Returns the existing singleton instance, or creates one using the base (non-editor) `GameLogger` if none exists yet. Murder.Editor typically replaces `_instance` with its own subclass before any logging occurs, so this fallback mainly matters for pure game builds and unit tests.

**Returns** \
[GameLogger](../../Murder/Diagnostics/GameLogger.html) \

#### FetchLogs()

```csharp
public static ImmutableArray<string> FetchLogs()
```

Returns a snapshot of every message currently stored in the log, in the order they were logged, as plain strings (colors/repeat-counts are dropped). Used by `GetCurrentLog()` to build the crash log, and by anything that wants to inspect the log's text without going through the console UI.

**Returns** \
[ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetCurrentLog()

```csharp
public static string GetCurrentLog()
```

Concatenates every currently-buffered log message (`FetchLogs()`) into a single newline-delimited string, in chronological order. Used by `CaptureCrash()` to build the crash report, and can be called directly to export the current session's log for debugging.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### DrawConsole(Func\<string, string\>?, World?)

```csharp
public virtual void DrawConsole(Func<string, string>? onInputAction = default, World? world = null)
```

Draws the console of the game. The base implementation is a no-op — only Murder.Editor's `GameLogger` subclass actually renders the ImGui console window. `onInputAction` is normally `CommandServices.Parse` bound to the current `world`, so submitted input is parsed and dispatched as a command; call this once per frame (guarded to debug/editor builds) to display the interactive console.

**Parameters** \
`onInputAction` [Func\<string, string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Func-2?view=net-7.0) \
`world` [World](../../Bang/World.html) \

#### TrackImpl(string, object)

```csharp
public virtual void TrackImpl(string variableName, object value)
```

Records a named variable's current value for live display in the debug overlay. Not implemented by game, only by editor — the base implementation does nothing, so calls to `Track` are effectively free no-ops in non-editor builds; Murder.Editor's subclass overrides this to store and render tracked values in a watch window.

**Parameters** \
`variableName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

#### ClearAllGraphs()

```csharp
public static void ClearAllGraphs()
```

Clears every plotted graph across all tracked source files by forwarding to the active `Game.GraphLogger` (see [GraphLogger.ClearAllGraphs()](../../Murder/Diagnostics/GraphLogger.html)).

#### ClearGraph(string)

```csharp
public static void ClearGraph(string callerFilePath = "")
```

Clears the plotted graph for the calling source file by forwarding to the active `Game.GraphLogger`. `callerFilePath` is normally left unset — the compiler fills it in automatically via `[CallerFilePath]` — so each call site clears its own graph.

**Parameters** \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Error(string, string, int)

```csharp
public static void Error(string msg, string memberName = "", int lineNumber = 0)
```

Emits an error message tagged with the caller's member name and line number, and forces the debug console overlay open (`_showDebug = true`) so the error is immediately visible. `memberName`/`lineNumber` are normally left unset — the compiler fills them in automatically via `[CallerMemberName]`/`[CallerLineNumber]`. Use for problems serious enough that a developer should notice them right away during play.

**Parameters** \
`msg` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`memberName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`lineNumber` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Fail(string)

```csharp
public static void Fail(string message)
```

This will fail a given message and paste it in the log. A convenience shorthand for `Verify(false, message)` — call it at a code path that should be unreachable to always report it, without having to write a redundant boolean condition.

**Parameters** \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### GetCrashLogPath()

```csharp
public static string GetCrashLogPath()
```

Full path to the `crash.log` file, located under the game's save data directory (`Game.Data.SaveBasePath`). This is where `CaptureCrash()` writes the log.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Initialize(bool)

```csharp
public void Initialize(bool diagnostic)
```

Sets up the logger. When `diagnostic` is `true`, subscribes to `AppDomain.FirstChanceException` so that every exception thrown anywhere in the game (even caught ones) is automatically spewed into the log via `SpewException(Exception)`. Called once during game start-up.

**Parameters** \
`diagnostic` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Log(string, Color?)

```csharp
public static void Log(string v, Microsoft.Xna.Framework.Color? color = null)
```

Emits a general-purpose log message tinted with an XNA `Color` (or white if `color` is `null`). This is the everyday entry point for game code that wants to print something to the debug console, e.g. `GameLogger.Log("Player spawned");`. Identical messages logged back-to-back are automatically collapsed with a repeat counter.

**Parameters** \
`v` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`color` [Color?](https://learn.microsoft.com/en-us/dotnet/api/Microsoft.Xna.Framework.Color?view=net-7.0) \

#### Log(string, Vector4)

```csharp
public static void Log(string v, Vector4 color)
```

Emits a general-purpose log message tinted with a raw `Vector4` RGBA color. Equivalent to the `Color?` overload, provided for callers that already work in `System.Numerics` color space (e.g. shader/graphics code).

**Parameters** \
`v` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`color` [Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### LogDebug(string)

```csharp
public static void LogDebug(string v)
```

Emits a message that only exists in `DEBUG` builds; compiled out entirely (and the call becomes a no-op) in release builds. Use for verbose, developer-only diagnostics that would be too noisy or costly to keep around in shipped builds.

**Parameters** \
`v` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### LogPerf(string, Vector4?)

```csharp
public static void LogPerf(string v, Vector4? color = null)
```

Emits a performance-timing message, rendered with a distinct "📈" marker and styling in the console. Used internally by [PerfTimeRecorder](../../Murder/Diagnostics/PerfTimeRecorder.html) to report how long a timed operation took, and can be called directly for ad-hoc perf logging.

**Parameters** \
`v` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`color` [Vector4?](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### PlotGraph(float, int, string)

```csharp
public static void PlotGraph(float point, int max, string callerFilePath = "")
```

Adds one data point to the calling source file's graph in the active `Game.GraphLogger`, scaled against an explicit `max` value — useful for graphs that should be normalized to a known range, e.g. a percentage. `callerFilePath` is supplied automatically by the compiler.

**Parameters** \
`point` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`max` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### PlotGraph(float, string)

```csharp
public static void PlotGraph(float point, string callerFilePath = "")
```

Adds one data point to the calling source file's graph in the active `Game.GraphLogger`, with no explicit maximum. Intended to be called once per frame from wherever a value should be visualized live in the diagnostics overlay (e.g. `GameLogger.PlotGraph(fps);`); `callerFilePath` is supplied automatically by the compiler and used to group points into a graph per call site.

**Parameters** \
`point` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`callerFilePath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### SpewException(Exception)

```csharp
public static void SpewException(Exception ex)
```

Spew exception details into log. Records the exception's full `ToString()` output (including stack trace) as the "last exception callstack" and reports it through `Warning`. Hooked up automatically to `AppDomain.FirstChanceException` by `Initialize` when diagnostics are enabled, so every thrown exception — even caught ones — passes through here.

**Parameters** \
`ex` [Exception](https://learn.microsoft.com/en-us/dotnet/api/System.Exception?view=net-7.0) \

#### FetchLastExceptionCallStack()

```csharp
public static string? FetchLastExceptionCallStack()
```

Returns the full text (message + stack trace) of the most recent exception seen by `SpewException`, or `null` if none has been recorded yet (or no instance exists). Used when writing a crash report so the offending exception is included alongside the rest of the log.

**Returns** \
[string?](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Toggle(bool)

```csharp
public static void Toggle(bool value)
```

Shows or hides the debug console overlay, matching the requested `value`. Does nothing if the console is already in the requested state; otherwise delegates to `ToggleDebugWindow()`.

**Parameters** \
`value` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ToggleDebugWindow()

```csharp
public void ToggleDebugWindow()
```

Flips the visibility of the debug console overlay. When opening it, forces the log view to scroll to the bottom and re-focuses the input text field so the player can type a command immediately.

#### Track(string, object)

```csharp
public static void Track(string variableName, object value)
```

Records a named variable value for live display in the debug/editor overlay (e.g. "watch" a gameplay value each frame without setting a breakpoint). Delegates to the singleton's `TrackImpl`, which only has an observable effect when running under the editor's `GameLogger` subclass. Does nothing if no instance has been created yet.

**Parameters** \
`variableName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`value` [object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

#### Verify(bool, string)

```csharp
public static void Verify(bool condition, string message)
```

This will verify a condition. If false, this will paste `message` in the log. In `DEBUG` builds, a failed check also either breaks into an attached debugger (`Debug.Fail`) or, if no debugger is attached, routes through `Error`; in all build configurations a failed check additionally logs a `Warning` with a short captured stack trace. This is Murder's lightweight assertion mechanism — prefer it over throwing when an invariant violation should be surfaced to a developer without necessarily crashing the running game.

**Parameters** \
`condition` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`message` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Verify(bool)

```csharp
public static void Verify(bool condition)
```

This will verify a condition. If false, this will paste a generic "An expected condition was not true." message in the log. Shorthand for `Verify(condition, string)` when there is no more specific message to report.

**Parameters** \
`condition` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Warning(string, string, int)

```csharp
public static void Warning(string msg, string memberName = "", int lineNumber = 0)
```

Emits a warning message tagged with the caller's member name and line number (filled in automatically by the compiler via `[CallerMemberName]`/`[CallerLineNumber]` unless explicitly overridden). Use for recoverable problems worth flagging but that don't stop execution — `Verify(bool, string)` routes its assertion failures through this.

**Parameters** \
`msg` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`memberName` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`lineNumber` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
