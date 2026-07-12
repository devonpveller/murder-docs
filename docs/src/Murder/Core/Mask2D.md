# Mask2D

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class Mask2D : IDisposable
```

An off-screen, render-target-backed 2D drawing surface used to compose an effect (a light cone, a fog-of-war mask, a screen-space cutout, etc.) separately from the main scene and then blend the result back into it.

**Intent:** Wraps a dedicated `RenderTarget2D` and `Batch2D`: call `Begin` to point drawing at the mask's own target and get a batch to draw into, then either `Stop` (to just end the batch without compositing) or one of the `End` overloads (to flush the batch and immediately draw the mask's contents into another batch at a given position).

**Use-case:** Create a `Mask2D` once per effect area, call `Begin` to start drawing the mask contents each frame, draw the mask's shapes/sprites into the returned `Batch2D`, then call `End` to composite the result onto the target batch at the desired world position (optionally offset by the camera).

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public Mask2D(int width, int height, Color? color = null)
```

Creates a mask of the given pixel dimensions. `color` (default transparent) is the color the render target is cleared to at the start of every `Begin` call.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [Color?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

```csharp
public Mask2D(Vector2 size, Color? color = null)
```

Creates a mask whose pixel dimensions are taken from `size` (truncated to integers).

**Parameters** \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [Color?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

```csharp
public Mask2D(Point size, Color? color = null)
```

Creates a mask whose pixel dimensions are taken from `size`.

**Parameters** \
`size` [Point](../../Murder/Core/Geometry/Point.html) \
`color` [Color?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

### ⭐ Properties

#### RenderTarget

```csharp
public RenderTarget2D RenderTarget { get; }
```

The underlying MonoGame render target this mask draws into.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### Size

```csharp
public Point Size { get; }
```

The current pixel dimensions of this mask's render target.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

### ⭐ Methods

#### Begin(bool)

```csharp
public Batch2D Begin(bool debug = false)
```

Redirects rendering to this mask's own `RenderTarget` (remembering whatever target was previously active so it can be restored by `Stop`/`End`), clears it to the mask's configured color, and starts its internal `Batch2D`.

**Parameters** \
`debug` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Batch2D](../../Murder/Core/Graphics/Batch2D.html) \

#### Dispose()

```csharp
public void Dispose()
```

Releases the underlying `RenderTarget2D`.

#### End(Batch2D, Vector2, DrawInfo)

```csharp
public void End(Batch2D targetBatch, Vector2 position, DrawInfo drawInfo)
```

Ends the mask's internal batch (drawing a debug outline first if `Begin` was called with `debug: true`), then draws the mask's render target into `targetBatch` at `position`, and restores whatever render target was active before `Begin`.

**Parameters** \
`targetBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### End(Batch2D, Vector2, Vector2, DrawInfo)

```csharp
public void End(Batch2D targetBatch, Vector2 position, Vector2 camera, DrawInfo drawInfo)
```

Applies a camera offset to the mask's internal batch transform, then flushes it and composites the mask's render target onto `targetBatch` at `position`. Use this overload instead of `End(Batch2D, Vector2, DrawInfo)` when the content drawn into the mask was authored in camera/world space and needs the camera translation applied before compositing.

**Parameters** \
`targetBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`camera` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### Resize(Point)

```csharp
public void Resize(Point size)
```

Grows or shrinks the mask's logical `Size` to match `size`. The backing `RenderTarget2D` is only reallocated when it needs to grow (shrinking just reduces the reported `Size` while keeping the larger allocation), so repeatedly resizing down and back up within the same peak dimensions is cheap. No-ops if `size` already matches.

**Parameters** \
`size` [Point](../../Murder/Core/Geometry/Point.html) \

**Exceptions** \
[ArgumentException](https://learn.microsoft.com/en-us/dotnet/api/System.ArgumentException?view=net-7.0) — if either dimension of `size` is zero or negative. \

#### Stop()

```csharp
public void Stop()
```

Stops the current batch (drawing a debug outline first if `Begin` was called with `debug: true`) and resets the render target to the previous one, if any. Does **not** draw the mask's render target to any batch — use one of the `End` overloads instead if the mask's contents need to be composited onto something.

⚡
