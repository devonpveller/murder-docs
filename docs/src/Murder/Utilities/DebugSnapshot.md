# DebugSnapshot

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public class DebugSnapshot
```

A singleton, subclassable profiling facility that measures how long named sections of code take to run (e.g. per-system timings) and exposes the results as a list of `(id, time)` entries. All entry points are guarded by `Game.DIAGNOSTICS_MODE` and are no-ops in a non-diagnostics build, so profiling calls can be left in shipping-adjacent code paths (like `SpriteRenderSystem`) without runtime cost when diagnostics are off.

**Intent:** By itself, `DebugSnapshot`'s protected `*Impl` methods do nothing (they are overridable stubs); the class exists to be subclassed by a concrete implementation that actually records timings — the editor provides `EditorDebugSnapshot`, which averages several consecutive snapshots and is installed via `EditorDebugSnapshot.OverrideInstanceWithEditor()`. This lets gameplay/engine code call the static `DebugSnapshot.*` methods unconditionally, while the editor (or any other host) decides whether/how profiling data is actually collected.

**Use-case:** Wrap a section of code with `StartStopwatch("label")` / `PauseStopwatch()` to time it (see `SpriteRenderSystem`, which times its own render pass), call `TakeSnapShot(samples)` to begin collecting an averaged batch of snapshots, and read `GetTotalTime()` / `GetAllEntries()` to display the results (the editor's `EditorSystem` polls these to draw a bar graph via `ImGuiHelpers.DrawBarsGraph`). Subclass `DebugSnapshot` and override the `*Impl` methods to plug in an actual timing implementation.

### ⭐ Constructors

```csharp
protected DebugSnapshot()
```

Protected constructor — this is a singleton, so instances are only created internally via `GetOrCreateInstance` (or by a subclass's own factory, such as `EditorDebugSnapshot.OverrideInstanceWithEditor`), never directly by consumers.

### ⭐ Methods

#### GetOrCreateInstance()

```csharp
public static DebugSnapshot GetOrCreateInstance()
```

Returns the current singleton instance, lazily constructing a plain `DebugSnapshot` the first time it's called if no subclass has already installed itself (e.g. via `EditorDebugSnapshot.OverrideInstanceWithEditor`). Every other static method on this class routes through this to reach the active instance.

**Returns** \
[DebugSnapshot](../../Murder/Utilities/DebugSnapshot.html) \

#### GetAllEntries()

```csharp
public static ImmutableArray<(string id, float time)> GetAllEntries()
```

Returns every recorded `(id, time)` entry from the active instance, or an empty array if `Game.DIAGNOSTICS_MODE` is disabled. Used by the editor's diagnostics overlay to render a per-section timing breakdown.

**Returns** \
[ImmutableArray\<ValueTuple\<T1, T2\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetAllEntriesImpl()

```csharp
protected virtual ImmutableArray<(string id, float time)> GetAllEntriesImpl()
```

Overridable hook behind `GetAllEntries()`; the base implementation is a no-op stub that always returns an empty array. A subclass (such as `EditorDebugSnapshot`) overrides this to return its own recorded `(id, time)` entries.

**Returns** \
[ImmutableArray\<ValueTuple\<T1, T2\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetTotalTime()

```csharp
public static float GetTotalTime()
```

Returns the total elapsed time recorded across the current/most recent snapshot on the active instance, or `0` if `Game.DIAGNOSTICS_MODE` is disabled.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetTotalTimeImpl()

```csharp
protected virtual float GetTotalTimeImpl()
```

Overridable hook behind `GetTotalTime()`; the base implementation is a no-op stub that always returns `0`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### EndSnapshot()

```csharp
public static void EndSnapshot()
```

Finalizes the current snapshot on the active instance (a no-op unless `Game.DIAGNOSTICS_MODE` is enabled), delegating to `EndSnapshotImpl`.

#### EndSnapshotImpl()

```csharp
protected virtual void EndSnapshotImpl()
```

Overridable hook behind `EndSnapshot()`; the base implementation is a no-op stub. A subclass overrides this to finalize whatever snapshot-recording state it tracks internally.

#### PauseStopwatch()

```csharp
public static void PauseStopwatch()
```

Pauses the currently-running named stopwatch started by `StartStopwatch` on the active instance (a no-op unless `Game.DIAGNOSTICS_MODE` is enabled), delegating to `PauseStopWatchImpl`.

#### PauseStopWatchImpl()

```csharp
protected virtual void PauseStopWatchImpl()
```

Overridable hook behind `PauseStopwatch()`; the base implementation is a no-op stub. A subclass overrides this to pause whatever stopwatch mechanism it uses.

#### StartStopwatch(string)

```csharp
public static void StartStopwatch(string id)
```

Begins (or resumes) timing a named section identified by `id` on the active instance (a no-op unless `Game.DIAGNOSTICS_MODE` is enabled). Pair with `PauseStopwatch()` to bracket the code being measured; `SpriteRenderSystem` uses this to time its own render pass.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### StartStopwatchImpl(string)

```csharp
protected virtual void StartStopwatchImpl(string id)
```

Overridable hook behind `StartStopwatch(string)`; the base implementation is a no-op stub. A subclass overrides this to begin timing the named section `id`.

**Parameters** \
`id` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### TakeSnapShot(int, float)

```csharp
public static void TakeSnapShot(int samples, float divider = 1000f)
```

Begins collecting a new batch of `samples` snapshots on the active instance (a no-op unless `Game.DIAGNOSTICS_MODE` is enabled), delegating to `TakeSnapShotImpl`. `divider` scales the recorded raw time units (e.g. converting microseconds to milliseconds) — the default `1000f` is used by the editor's diagnostics overlay.

**Parameters** \
`samples` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`divider` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TakeSnapShotImpl(int, float)

```csharp
protected virtual void TakeSnapShotImpl(int samples, float divider)
```

Overridable hook behind `TakeSnapShot(int, float)`; the base implementation is a no-op stub. A subclass overrides this to begin collecting `samples` snapshots, scaling recorded values by `divider`.

**Parameters** \
`samples` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`divider` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
