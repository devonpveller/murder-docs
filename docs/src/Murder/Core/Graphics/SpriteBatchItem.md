# SpriteBatchItem

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public class SpriteBatchItem
```

A single queued draw call inside a `Batch2D`: the source texture, the transformed vertex positions/UVs/colors for its quad (or polygon), the triangle index list, and the blend state to draw with.

**Intent:** Encapsulates all GPU data needed to draw one sprite quad or polygon, including rotation, scale, flipping, tint color, and blend mode. Instances are pooled and reused by `Batch2D` rather than allocated per draw call.

**Use-case:** Created and pooled automatically by `Batch2D`; call `Set()` directly to overwrite a pooled item with a textured quad, or `SetPolygon()` to overwrite it with arbitrary polygon geometry.

### ⭐ Constructors

```csharp
public SpriteBatchItem()
```

### ⭐ Properties

#### BlendState

```csharp
public MurderBlendState BlendState;
```

The blend state this item should be drawn with, set from the caller's draw parameters (e.g. `DrawInfo`).

**Returns** \
[MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \

#### IndexData

```csharp
public short[] IndexData;
```

Triangle index list into `VertexData`. Six indices describing two triangles for a quad by default, or resized to fit an arbitrary polygon's triangle fan by `SetPolygon()`.

**Returns** \
[short[]](https://learn.microsoft.com/en-us/dotnet/api/System.Int16?view=net-7.0) \

#### Texture

```csharp
public Texture2D Texture;
```

The source texture sampled when rendering this item; typically a page of a `TextureAtlas`.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### VertexCount

```csharp
public short VertexCount;
```

Number of active vertices in `VertexData`; 4 for a quad drawn via `Set()`, or the polygon's vertex count when set via `SetPolygon()`.

**Returns** \
[short](https://learn.microsoft.com/en-us/dotnet/api/System.Int16?view=net-7.0) \

#### VertexData

```csharp
public VertexInfo[] VertexData;
```

Per-vertex data (position, tint color, UV, blend selector) for this item's geometry. Sized to 4 for a regular textured quad drawn via `Set()`, or resized to fit an arbitrary polygon by `SetPolygon()`.

**Returns** \
[VertexInfo[]](../../../Murder/Core/Graphics/VertexInfo.html) \

### ⭐ Methods

#### Set(Texture2D, Vector2, Vector2, T?, float, Vector2, ImageFlip, Color, Vector2, Vector3, MurderBlendState, float)

```csharp
public void Set(Texture2D texture, Vector2 position, Vector2 destinationSize, T? sourceRectangle, float rotation, Vector2 scale, ImageFlip flip, Color color, Vector2 origin, Vector3 colorBlend, MurderBlendState blendState, float layerDepth = 1f)
```

Sets a Texture to be drawn to the batch

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`position` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`destinationSize` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`sourceRectangle` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`scale` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`flip` [ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`origin` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`colorBlend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
`blendState` [MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \
`layerDepth` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SetPolygon(Texture2D, Vector2, ReadOnlySpan<T>, DrawInfo)

```csharp
public void SetPolygon(Texture2D texture, Vector2 position, ReadOnlySpan<T> vertices, DrawInfo drawInfo)
```

Configures this item to draw an arbitrary (non-quad) polygon: uploads a transformed copy of `vertices` (scaled, rotated, and flipped according to `drawInfo`, and offset by `position`) and builds a triangle-fan index list connecting them. Resizes `VertexData`/`IndexData` if the supplied polygon is larger than the current buffers. Texture coordinates are left at (0,0) for every vertex.

**Parameters** \
`texture` [Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \
`position` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \
`vertices` [ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \
`drawInfo` [DrawInfo](../../../Murder/Core/Graphics/DrawInfo.html) \

⚡
