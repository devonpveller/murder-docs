# RuntimeAtlas

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class RuntimeAtlas : IDisposable
```

A dynamically managed GPU texture atlas assembled at runtime from individually rendered chunks.

**Intent:** Provides a growable render-target atlas that game systems can write into at runtime, enabling efficient batching of dynamically generated content such as cached text or procedural sprites.

**Use-case:** Call `PlaceChunk()` to reserve a slot, use `Begin()` to obtain a `Batch2D` to render into that slot, then call `End()` to commit. Render the chunk to the screen with `Draw()`.

**Implements:** _[IDisposable](https://learn.microsoft.com/en-us/dotnet/api/System.IDisposable?view=net-7.0)_

### ⭐ Constructors
```csharp
public RuntimeAtlas(string name, Point atlasSize, Point chunkSize)
```

Creates a new atlas render target with the given name, total size, and chunk size. The atlas size is clamped to a whole number of chunks.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`atlasSize` [Point](../../../Murder/Core/Geometry/Point.html) \
`chunkSize` [Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties
#### _debug
```csharp
public bool _debug;
```

Enables debug visualization of atlas chunk boundaries and occupancy when set to true.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### AllLoadedAtlas
```csharp
public readonly static List<T> AllLoadedAtlas;
```

Global list of every `RuntimeAtlas` instance that is currently loaded and has not been disposed.

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

Starts a drawing session for the specified chunk and returns a `Batch2D` to render into it. Must be followed by a call to `End()`.

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

Reserves the next available chunk slot in the atlas and returns its ID, cycling from the start if the atlas is full.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetBrush()
```csharp
public RenderTarget2D GetBrush()
```

Returns the small scratch render target used internally as a transparent eraser brush when clearing chunks.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### GetFullAtlas()
```csharp
public RenderTarget2D GetFullAtlas()
```

Returns the full atlas render target for inspection, sampling, or use as a texture in a shader.

**Returns** \
[RenderTarget2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RenderTarget2D.html) \

#### Dispose()
```csharp
public virtual void Dispose()
```

Releases all GPU resources (render targets and batch) held by this atlas and removes it from `AllLoadedAtlas`.

#### Cleanup()
```csharp
public void Cleanup()
```

Clears all chunk data from the atlas, resetting the next-available pointer to zero.

#### End()
```csharp
public void End()
```

Commits the current drawing session and flushes the `Batch2D` contents into the atlas render target.

#### FreeChunk(int)
```csharp
public void FreeChunk(int chunkId)
```

Clears the contents of the specified chunk by painting it with a transparent brush.

**Parameters** \
`chunkId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡