# UpdateTimeTracker

**Namespace:** Murder.Diagnostics \
**Assembly:** Murder.dll

```csharp
public class UpdateTimeTracker
```

Track the latest update times.

**Intent:** A simple fixed-capacity (528-entry) ring buffer of frame-time samples in milliseconds, used to feed the diagnostics overlay's frame-time history graphs. Kept deliberately dependency-free (no `GraphLogger`/`GameLogger` coupling) so `Game` can hold one for update time and another for render time without any overhead when nobody is looking at them.

**Use-case:** [Game](../../Murder/Game.html) owns two static instances — `Game.TimeTrackerDiagnostics` and `Game.RenderTimeTrackerDiagnostics` — and calls `Update(dt)` on each once per frame with the measured update/render duration. Murder.Editor's system code (`EditorSystem`) reads `Sample`/`Length` off both to plot recent update and render time history in the diagnostics window. Game code does not typically create its own `UpdateTimeTracker`; it's an editor-facing profiling utility.

### ⭐ Constructors

```csharp
public UpdateTimeTracker()
```

Default parameterless constructor (no custom initialization beyond the field initializers); allocates the 528-entry `Sample` buffer.

### ⭐ Properties

#### Length

```csharp
public int Length { get; }
```

Number of samples currently considered valid in `Sample` (the write cursor position plus one).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Sample

```csharp
public readonly float[] Sample;
```

Ring buffer of the most recent update delta times, in milliseconds. Only populated in `DEBUG` builds (see `Update(double)`); read by the diagnostics overlay to plot recent frame-time history.

**Returns** \
[float[]](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### Update(double)

```csharp
public void Update(double dt)
```

Appends `dt` (in seconds, converted to milliseconds) to the `Sample` ring buffer, advancing the write index. Once the buffer fills up, older entries are shifted down (dropping the oldest sample) to make room, so `Sample` always holds the most recent up-to-528 update times. Compiled to a no-op outside `DEBUG` builds — this tracker exists purely for editor/diagnostics use and should not affect release-build performance.

**Parameters** \
`dt` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \

⚡
