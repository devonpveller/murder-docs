# RuntimeAtlas

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class RuntimeAtlas : IDisposable
```

A dynamically managed render-target atlas that game systems can write into at runtime, one fixed-size "chunk" at a time.

**Intent:** Lets many small pieces of dynamically generated content (e.g. cached rich text, procedural sprites) be batched together and drawn from a single GPU texture instead of one texture per piece. Chunks are handed out from a ring buffer, so old chunks are silently overwritten once the atlas wraps around.

**Use-case:** Call `PlaceChunk()` to reserve a slot, use `Begin()` to obtain the atlas's `Batch2D` to render into that slot, then call `End()` to commit the drawing. Render the chunk to the screen later with `Draw()`. `FloorWithBatchOptimizationRenderSystem` uses a `RuntimeAtlas` to cache pre-composited floor tiles.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors

```csharp
public RuntimeAtlas(string name, Point atlasSize, Point chunkSize)
```

Creates a new atlas render target with the given debug name, total size, and chunk size. The atlas is laid out as a grid of equally sized chunks; `atlasSize` is rounded down to the nearest whole number of chunks that fit, so the actual `Size` may end up smaller than requested.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`atlasSize` [Point](../../../Murder/Core/Geometry/Point.html) \
`chunkSize` [Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties

#### \_debug

```csharp
public bool _debug;
```

When set to true, each chunk is drawn with its numeric id overlaid and a gray outline around its bounds, useful for visually inspecting chunk allocation and boundaries while debugging.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AllLoadedAtlas

```csharp
public readonly static List<T> AllLoadedAtlas;
```

Every `RuntimeAtlas` instance currently alive (created but not yet disposed via `Dispose()`). Used to track and manage all runtime atlases, e.g. when reloading graphics resources.

**Returns** \
[List\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### Size

```csharp
public readonly Vector2 Size;
```

Pixel dimensions of the full atlas render target.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Methods

#### Begin(int)

```csharp
public Batch2D Begin(int chunkId)
```

Starts a drawing session for the specified chunk and returns the atlas's internal `Batch2D` to render into it. Must be followed by a matching call to `End()`; only one chunk can be in progress at a time. Throws if a chunk drawing session is already in progress.

**Parameters** \
`chunkId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \

#### Draw(int, Batch2D, Vector2, DrawInfo)

```csharp
public bool Draw(int id, Batch2D batch, Vector2 position, DrawInfo drawInfo)
```

Draws a chunk to the screen and returns if it was successful

**Parameters** \
`id` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`drawInfo` [DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PlaceChunk()

```csharp
public int PlaceChunk()
```

Reserves the next available chunk slot in the atlas and returns its ID. Slots are handed out from a ring buffer: once every slot has been used, subsequent calls wrap back around to the start and reuse (evict) the oldest chunks. Call `Begin()`/`End()` with the returned id to actually render content into the reserved slot.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetBrush()

```csharp
public RenderTarget2D GetBrush()
```

Returns the small scratch render target used internally as a transparent "eraser" brush when clearing and re-painting individual chunks. Exposed mainly for debugging the atlas internals.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### GetFullAtlas()

```csharp
public RenderTarget2D GetFullAtlas()
```

Returns the full atlas render target, e.g. to sample it directly in a shader or to inspect it in a debug view. Prefer `Draw()` for drawing a single chunk.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### Dispose()

```csharp
public void Dispose()
```

Releases the GPU render targets (the atlas texture and the scratch brush) held by this atlas and removes it from `AllLoadedAtlas`. Does not dispose the internal `Batch2D`.

#### Cleanup()

```csharp
public void Cleanup()
```

Resets the chunk allocator, discarding all chunk data logically (the pixels are not cleared until each slot is reused) and restarting allocation from the first slot.

#### End()

```csharp
public void End()
```

Commits the drawing session started by `Begin()`: flushes the batched draw calls into a scratch "brush" render target first (to avoid bleeding into neighboring chunks), then blits that brush onto the chunk's slot in the atlas. Throws if no chunk drawing session is currently in progress.

#### FreeChunk(int)

```csharp
public void FreeChunk(int chunkId)
```

Clears the contents of the specified chunk by painting it with a transparent "eraser" brush, so no stale pixels remain when the slot is reused by `PlaceChunk()` or discarded via `Cleanup()`.

**Parameters** \
`chunkId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
