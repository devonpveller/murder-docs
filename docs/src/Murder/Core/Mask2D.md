# Mask2D

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class Mask2D : IDisposable
```

A 2D render-target-backed mask used to draw visibility regions, light cones, or any GPU-composited area overlay. Wraps a `RenderTarget2D` with a dedicated `Batch2D` and supports drawing content into it and then compositing the result onto the main batch.

**Intent:** Off-screen render texture for masking or overlay effects that need to be rendered separately and then blended into the scene.

**Use-case:** Create a `Mask2D` once per effect area, call `Begin` to start drawing the mask contents, then call `Draw` to composite the result onto the target batch at the desired world position.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
public Mask2D(int width, int height, T? color)
```

Creates a `Mask2D` of the given pixel dimensions, optionally tinted with `color` when composited.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`color` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

```csharp
public Mask2D(Vector2 size, T? color)
```

Creates a `Mask2D` whose dimensions are taken from the `size` vector.

**Parameters** \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`color` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

### ⭐ Properties
#### IsDisposed
```csharp
public bool IsDisposed { get; }
```

Whether the underlying render target has already been disposed.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### RenderTarget
```csharp
public RenderTarget2D RenderTarget { get; }
```

The underlying MonoGame render target this mask draws into.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \
#### Size
```csharp
public readonly Vector2 Size;
```

The pixel dimensions of this mask's render target.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
### ⭐ Methods
#### Begin(bool)
```csharp
public Batch2D Begin(bool debug)
```

Activates this mask's render target and returns its internal `Batch2D` so callers can draw mask content into it.

**Parameters** \
`debug` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[Batch2D](../../Murder/Core/Graphics/Batch2D.html) \

#### Dispose()
```csharp
public virtual void Dispose()
```

Releases the underlying `RenderTarget2D` and associated GPU resources.

#### Draw(Batch2D, Vector2, DrawInfo)
```csharp
public void Draw(Batch2D targetBatch, Vector2 position, DrawInfo drawInfo)
```

Ends the batch (if it is still running) and draws the render target to the target batch. If already ended, it will just draw the render target.

**Parameters** \
`targetBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### End(Batch2D, Vector2, DrawInfo)
```csharp
public void End(Batch2D targetBatch, Vector2 position, DrawInfo drawInfo)
```

Flushes the internal batch and immediately composites the mask's render target onto `targetBatch` at `position`.

**Parameters** \
`targetBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \

#### End(Batch2D, Vector2, Vector2, DrawInfo)
```csharp
public void End(Batch2D targetBatch, Vector2 position, Vector2 camera, DrawInfo drawInfo)
```

Flushes the internal batch and composites the mask onto `targetBatch`, offsetting by the camera position.

**Parameters** \
`targetBatch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`camera` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \



⚡