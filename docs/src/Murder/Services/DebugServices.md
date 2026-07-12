# DebugServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class DebugServices
```

Development utilities for timing code, saving the session log, and drawing short-lived debug shapes/text directly into the world.

**Intent:** Provides low-friction helpers for the kind of ad-hoc instrumentation you reach for while debugging: measuring how long something takes, dumping the log to disk, and visualizing positions, paths, or areas without setting up a dedicated debug-rendering system.

**Use-case:** Wrap a suspect code block in `StopwatchStart`/`StopwatchStop` to log its execution time in milliseconds. Call `SaveLogAsync` from a crash handler or feedback flow to persist the buffered log for a bug report. Call `DrawText`, `DrawLine`, or `DrawRectangle` from gameplay/AI code to visualize a value, path segment, or bounding box for a short duration — these spawn a throwaway entity with a custom draw callback and destroy themselves automatically, and are compiled out entirely in non-`DEBUG` builds.

### ⭐ Properties

#### DebugPreviewImage

```csharp
public static Texture2D? DebugPreviewImage;
```

A texture slot that tooling/editor code can set at runtime to be shown as a debug preview/overlay image; `null` when no preview is active. This is a simple shared "mailbox" rather than a stack, so only one preview can be active at a time.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

### ⭐ Methods

#### StopwatchStart()

```csharp
public static DateTime StopwatchStart()
```

Records `DateTime.Now` as the start of a stopwatch measurement (in a static field shared across all callers) and returns it. Pair with `StopwatchStop` to measure elapsed wall-clock time around a block of code. Because the start time is stored statically, do not use this for overlapping/concurrent measurements.

**Returns** \
[DateTime](https://learn.microsoft.com/en-us/dotnet/api/System.DateTime?view=net-7.0) \

#### StopwatchStop()

```csharp
public static float StopwatchStop()
```

Computes the elapsed time in milliseconds since the last `StopwatchStart` call, logs it (prefixed `[STOPWATCH]`) via `GameLogger.Log`, and returns the value.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SaveLogAsync(string)

```csharp
public static Task SaveLogAsync(string fullpath)
```

Appends every currently buffered game log line (from `GameLogger.FetchLogs`) to the file at `fullpath`. Typically used when generating a diagnostic bundle for a crash or feedback report (see [FeedbackServices](../../Murder/Services/FeedbackServices.html)) or for manually dumping the session log during a debugging session.

**Parameters** \
`fullpath` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

**Returns** \
[Task](https://learn.microsoft.com/en-us/dotnet/api/System.Threading.Tasks.Task?view=net-7.0) \

#### DrawText(World, string, Vector2, float, Color)

```csharp
public static void DrawText(World world, string ev, Vector2 position, float duration, Color color)
```

Spawns a temporary entity (`DEBUG` builds only) that draws `ev` as text at `position` for `duration` seconds, fading the text and its shadow/outline out over that time before destroying itself. Useful for labeling a position, entity state, or value transiently while iterating on gameplay logic without polluting the release build.

**Parameters** \
`world` [World](../../Bang/World.html) \
`ev` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \

#### DrawLine(World, Vector2, Vector2, Color, float)

```csharp
public static void DrawLine(World world, Vector2 start, Vector2 end, Color color, float duration = 1 / 30f)
```

Spawns a temporary entity (`DEBUG` builds only) that draws a line from `start` to `end` in `color`, fading in over `duration` seconds before self-destructing. Handy for visualizing raycasts, movement vectors, or pathfinding segments while debugging.

**Parameters** \
`world` [World](../../Bang/World.html) \
`start` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`end` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DrawRectangle(World, Rectangle, Color, float)

```csharp
public static void DrawRectangle(World world, Rectangle rect, Color color, float duration = 1 / 30f)
```

Spawns a temporary entity (`DEBUG` builds only) that draws the outline of `rect` in `color`, fading in over `duration` seconds before self-destructing. Useful for visualizing bounding boxes, trigger areas, or collider shapes while debugging.

**Parameters** \
`world` [World](../../Bang/World.html) \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../Murder/Core/Graphics/Color.html) \
`duration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
