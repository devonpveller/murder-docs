# Batch2D

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class Batch2D
```

A sprite batch that collects 2D draw calls for a single render layer and submits them to the GPU in as few draw calls as possible, grouping consecutive sprites that share a texture and blend state.

**Intent:** Provides the low-level sprite-batching infrastructure used by every render layer in a `RenderContext` (and by helpers such as `Mask2D`); conceptually similar to MonoGame's `SpriteBatch`, but with configurable depth-sorting via `BatchMode` and support for custom shader effects.

**Use-case:** Obtain the relevant `Batch2D` from `RenderContext` (e.g. `RenderContext.GameplayBatch`) or a custom index registered via `Batches2D`, call `Begin`, issue `Draw`/`DrawPolygon` calls, then call `End`. The `BatchMode` passed at construction controls whether sprites are sorted by depth or drawn in submission order.

### ⭐ Constructors

```csharp
public Batch2D(string name, GraphicsDevice graphicsDevice, Effect? effect, BatchMode batchMode, SamplerState samplerState, DepthStencilState? depthStencilState, RasterizerState? rasterizerState)
```

Creates a `Batch2D` that does **not** follow the camera transform (its `Transform` stays at `Matrix.Identity`); suitable for screen-space layers such as the static UI batch. Delegates to the other constructor with `followCamera: false`.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`batchMode` [BatchMode](../../../Murder/Core/Graphics/BatchMode.html) \
`samplerState` [SamplerState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.SamplerState.html) \
`depthStencilState` [DepthStencilState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.DepthStencilState.html) \
`rasterizerState` [RasterizerState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RasterizerState.html) \

```csharp
public Batch2D(string name, GraphicsDevice graphicsDevice, bool followCamera, Effect? effect, BatchMode batchMode, SamplerState samplerState, DepthStencilState? depthStencilState, RasterizerState? rasterizerState)
```

Creates a `Batch2D` with explicit control over whether the batch follows the camera transform. Pass `followCamera: true` for world-space layers (gameplay, floor) so sprites scroll with `Camera2D`, or `false` for layers that should stay fixed to the screen. `depthStencilState` defaults to `DepthStencilState.None` and `rasterizerState` to `RasterizerState.CullNone` when omitted.

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`graphicsDevice` [GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \
`followCamera` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`effect` [Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \
`batchMode` [BatchMode](../../../Murder/Core/Graphics/BatchMode.html) \
`samplerState` [SamplerState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.SamplerState.html) \
`depthStencilState` [DepthStencilState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.DepthStencilState.html) \
`rasterizerState` [RasterizerState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RasterizerState.html) \

### ⭐ Properties

#### BatchMode

```csharp
public readonly BatchMode BatchMode;
```

The sorting and batching strategy used when `Flush()`/`End()` submits draw calls to the GPU; set once at construction.

**Returns** \
[BatchMode](../../../Murder/Core/Graphics/BatchMode.html) \

#### DepthStencilState

```csharp
public readonly DepthStencilState DepthStencilState;
```

The MonoGame depth/stencil state applied during rendering; controls depth writes and reads for this batch.

**Returns** \
[DepthStencilState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.DepthStencilState.html) \

#### Effect

```csharp
public Effect? Effect { get; public set; }
```

The shader effect applied to all sprites in this batch when `Render()` draws them. Can be swapped between frames (e.g. `Game.Data.ShaderSprite`) to change the visual appearance of the entire layer.

**Returns** \
[Effect](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Effect.html) \

#### GraphicsDevice

```csharp
public GraphicsDevice GraphicsDevice { get; public set; }
```

The MonoGame graphics device used to create GPU resources and submit draw calls.

**Returns** \
[GraphicsDevice](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.GraphicsDevice.html) \

#### IsBatching

```csharp
public bool IsBatching { get; private set; }
```

`true` after `Begin()` has been called and before `End()` completes; indicates that `Draw`/`DrawPolygon` calls may be queued. Calling `Draw` while this is `false` logs a warning (in `DEBUG`) and is ignored.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### ItemsQueued

```csharp
public int ItemsQueued { get; }
```

Number of sprite items that were queued and submitted the last time this batch was flushed (via `Flush()`, `End()`, or `GiveUp()`). Useful for diagnostics/HUD overlays that report per-layer sprite counts.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### MaxTextureSwaps

```csharp
public int MaxTextureSwaps { get; private set; }
```

The largest number of texture swaps observed in a single render pass so far this session. Texture swaps force a draw-call flush, so a high value signals that sprites in this batch are not grouped by texture/atlas and could benefit from re-ordering or atlas consolidation.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Name

```csharp
public string Name;
```

A human-readable label for this batch (e.g. `"Gameplay"`, `"Ui"`, `"Debug"`), used in diagnostics, logging, and the editor's batch-preview tooling.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### RasterizerState

```csharp
public readonly RasterizerState RasterizerState;
```

The MonoGame rasterizer state (e.g., culling mode, fill mode) applied when this batch is rendered.

**Returns** \
[RasterizerState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.RasterizerState.html) \

#### SamplerState

```csharp
public readonly SamplerState SamplerState;
```

The texture sampling mode (e.g., point, linear, anisotropic) applied when drawing atlas textures in this batch. Murder's pixel-art layers typically use `SamplerState.PointClamp`.

**Returns** \
[SamplerState](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.SamplerState.html) \

#### SpriteCount

```csharp
public static int SpriteCount { get; private set; }
```

`DEBUG`-only running total of sprites flushed across all `Batch2D` instances since the game started; reset only on process restart. Used for coarse performance diagnostics.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### StartBatchItemsCount

```csharp
public static const int StartBatchItemsCount;
```

Initial capacity of the internal sprite-item buffer (128 items). The buffer doubles automatically whenever more items are queued than it can hold.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### TotalDrawCalls

```csharp
public static int TotalDrawCalls { get; private set; }
```

`DEBUG`-only running total of GPU draw calls issued across all `Batch2D` instances; incremented once per `DrawQuads` call. Useful for spotting excessive texture/blend-state swapping in the editor's performance overlay.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### TotalItemCount

```csharp
public int TotalItemCount { get; }
```

Total number of sprite-item slots currently allocated in the internal buffer (including empty slots left over from a previous larger frame). This reflects buffer capacity, not the number of sprites queued this frame — see `ItemsQueued` for that.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Transform

```csharp
public Matrix Transform { get; private set; }
```

The current transform matrix applied to all sprites submitted since `Begin()` was last called; either the camera's view-projection matrix (when the batch follows the camera) or `Matrix.Identity`/a manual value set via `SetTransform`.

**Returns** \
[Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \

### ⭐ Methods

#### Begin(Matrix)

```csharp
public void Begin(Matrix cameraMatrix)
```

Opens the batch for draw calls. If this batch was constructed with `followCamera: true`, `cameraMatrix` becomes the active `Transform`; otherwise the batch stays at `Matrix.Identity`. Must be called before any `Draw`/`DrawPolygon` call.

**Parameters** \
`cameraMatrix` [Matrix](https://docs.monogame.net/api/Microsoft.Xna.Framework.Matrix.html) \

#### Draw(Texture2D, Vector2, Vector2, Rectangle, float, float, Vector2, ImageFlip, Color, Vector2, Vector3, MurderBlendState)

```csharp
public void Draw(Texture2D texture, Vector2 position, Vector2 targetSize, Rectangle sourceRectangle, float sort, float rotation, Vector2 scale, ImageFlip flip, Color color, Vector2 offset, Vector3 blendStyle, MurderBlendState blendState)
```

Queues a single sprite quad for drawing. This is the core primitive underlying almost every higher-level draw helper in the engine (`AtlasCoordinates.Draw`, `MurderTexture.Draw`, etc). If `BatchMode` is `BatchMode.Immediate`, the sprite is flushed to the GPU immediately instead of being batched.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`position` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`targetSize` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`sourceRectangle` [Rectangle](https://docs.monogame.net/api/Microsoft.Xna.Framework.Rectangle.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scale` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`flip` [ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \
`color` [Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \
`offset` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`blendStyle` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
`blendState` [MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \

#### DrawPolygon(Texture2D, Vector2, ReadOnlySpan\<Vector2\>, DrawInfo)

```csharp
public void DrawPolygon(Texture2D texture, Vector2 position, ReadOnlySpan<Vector2> vertices, DrawInfo drawInfo)
```

Draws a textured convex polygon defined by an arbitrary vertex fan, offset by `position`. Used for non-rectangular geometry (e.g. light volumes, custom shapes) that can't be expressed as a simple sprite quad. Throws if called before `Begin()`.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`vertices` [ReadOnlySpan\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`drawInfo` [DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \

**Exceptions** \
[InvalidOperationException](https://learn.microsoft.com/en-us/dotnet/api/System.InvalidOperationException?view=net-7.0) \

#### DrawPolygon(Texture2D, Vector2, ImmutableArray\<Vector2\>, DrawInfo)

```csharp
public void DrawPolygon(Texture2D texture, Vector2 position, ImmutableArray<Vector2> vertices, DrawInfo drawInfo)
```

Same as the `ReadOnlySpan<Vector2>` overload, but convenient for callers that already store their vertex list as an `ImmutableArray<Vector2>` (e.g. cached polygon shapes). Throws if called before `Begin()`.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`vertices` [ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`drawInfo` [DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \

**Exceptions** \
[InvalidOperationException](https://learn.microsoft.com/en-us/dotnet/api/System.InvalidOperationException?view=net-7.0) \

#### End()

```csharp
public void End()
```

Flushes all queued sprites to the GPU (via `Flush()`) and marks the batch as no longer accepting draw calls (`IsBatching` becomes `false`). Throws if `Begin()` was not called first.

**Exceptions** \
[InvalidOperationException](https://learn.microsoft.com/en-us/dotnet/api/System.InvalidOperationException?view=net-7.0) \

#### Flush(bool)

```csharp
public void Flush(bool includeAlphaBlendedSprites)
```

Sends all currently queued sprites to the GPU without ending the batching session (`IsBatching` stays `true`), so more `Draw` calls can follow. `End()` calls this internally. `includeAlphaBlendedSprites` is currently unused by the implementation but reserved for future partial-flush support — be careful when relying on its exact semantics.

**Parameters** \
`includeAlphaBlendedSprites` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GiveUp()

```csharp
public void GiveUp()
```

Discards all sprites queued since the last flush without drawing them, resetting the internal cursor. Similar to `End()` but skips the GPU submission entirely — useful when a frame's contents need to be thrown away (e.g. an aborted debug preview).

#### SetTransform(Vector2)

```csharp
public void SetTransform(Vector2 position)
```

Overrides `Transform` with a pure translation matrix, ignoring the camera. Used by callers (e.g. `Mask2D`) that need to position a batch's output manually instead of following the world camera.

**Parameters** \
`position` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### SetTransform(Vector2, Vector2)

```csharp
public void SetTransform(Vector2 position, Vector2 scale)
```

Overrides `Transform` with a combined scale-then-translate matrix, ignoring the camera. Used to place and size batch output manually (e.g. rendering a `Mask2D` render target into a target batch at an arbitrary screen position and scale).

**Parameters** \
`position` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`scale` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

⚡
