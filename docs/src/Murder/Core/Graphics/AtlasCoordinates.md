# AtlasCoordinates

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AtlasCoordinates
```

An image coordinate inside an atlas

**Intent:** Describes a single sprite frame — its pixel rectangle within a packed texture atlas, its original (pre-trim) size, and UV coordinates ready for the GPU.

**Use-case:** Obtained from `Game.Data.FetchAtlas()` or from a `SpriteAsset` frame lookup; passed directly to `Batch2D.Draw` or `AtlasCoordinates.Draw` to render the frame.

### ⭐ Constructors

```csharp
public AtlasCoordinates(string name, string atlasId, IntRectangle atlasRectangle, Point contentOffset, Point size, int atlasIndex, int atlasWidth, int atlasHeight)
```

**Parameters** \
`name` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`atlasId` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \
`atlasRectangle` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \
`contentOffset` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \
`atlasIndex` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`atlasWidth` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`atlasHeight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Atlas

```csharp
public Texture2D Atlas { get; }
```

The GPU texture object for the atlas page that contains this coordinate.

**Returns** \
[Texture2D](https://docs.monogame.net/api/Microsoft.Xna.Framework.Graphics.Texture2D.html) \

#### AtlasId

```csharp
public readonly string AtlasId;
```

The name of the atlas that owns this coordinate (e.g. `"atlas"`, `"editor"`), used with `Game.Data.FetchAtlas()` to retrieve the correct `TextureAtlas` page. Despite the name, this is a plain string key, not the `Data.AtlasId` enum.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### AtlasIndex

```csharp
public readonly int AtlasIndex;
```

Zero-based index of the atlas texture page that stores this image, for multi-page atlases.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### AtlasSize

```csharp
public Point AtlasSize { get; }
```

The pixel dimensions of the atlas texture page (width × height), used for UV normalisation.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### ContentOffset

```csharp
public readonly Point ContentOffset { get; init; }
```

The offset of the bounding box of the pixels that survived trimming, i.e. how far the visible (non-transparent) region of `SourceRectangle` is shifted from the top-left of the original, un-trimmed artwork. Used by `Draw()` to reposition the sprite so it lines up as if it were never trimmed.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Empty

```csharp
public static AtlasCoordinates Empty;
```

A default-initialised `AtlasCoordinates` with no atlas or rectangle data; safe to use as a null-equivalent sentinel.

**Returns** \
[AtlasCoordinates](../../../Murder/Core/Graphics/AtlasCoordinates.html) \

#### Height

```csharp
public int Height { get; }
```

Pixel height of the source rectangle within the atlas (the visible trimmed area).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Name

```csharp
public readonly string Name;
```

The asset name of the sprite as packed in the atlas (matches the key used to fetch it).

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

#### Size

```csharp
public readonly Point Size;
```

The real size of the image, without trimming

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### SourceRectangle

```csharp
public readonly IntRectangle SourceRectangle;
```

Pixel rectangle within the atlas texture that contains this image's visible pixels (after trimming transparent borders).

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### ContentOffset

```csharp
public readonly Point ContentOffset { get; init; }
```

The offset of the bounding box of the pixels that survived trimming, i.e. how far the visible (non-transparent) region of `SourceRectangle` is shifted from the top-left of the original, un-trimmed artwork. Used by `Draw()` to reposition the sprite so it lines up as if it were never trimmed.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### UV

```csharp
public readonly Rectangle UV;
```

Normalized (0–1) UV rectangle mapping `SourceRectangle` into the atlas texture, ready to pass to the GPU shader.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Width

```csharp
public int Width { get; }
```

Pixel width of the source rectangle within the atlas (the visible trimmed area).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### Draw(Batch2D, Rectangle, Rectangle, Color, float, Vector3)

```csharp
public void Draw(Batch2D spriteBatch, Rectangle clip, Rectangle target, Color color, float depthLayer, Vector3 blend)
```

Draws a partial image stored inside an atlas to the spritebatch to a specific rect

**Parameters** \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`clip` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`target` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`depthLayer` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### Draw(Batch2D, Vector2, Rectangle, Color, Vector2, float, Vector2, ImageFlip, Vector3, MurderBlendState, float)

```csharp
public void Draw(Batch2D spriteBatch, Vector2 position, Rectangle clip, Color color, Vector2 scale, float rotation, Vector2 offset, ImageFlip imageFlip, Vector3 blend, MurderBlendState blendState, float sort)
```

Draws a partial image stored inside an atlas to the spritebatch, handling trimming, flipping and an optional clip rectangle. This is the low-level overload used internally by sprite-rendering helpers; most gameplay code instead goes through `RenderServices` or component-level draw calls.

**Parameters** \
`spriteBatch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`clip` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`imageFlip` [ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \
`blendState` [MurderBlendState](../../../Murder/Core/Graphics/MurderBlendState.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
