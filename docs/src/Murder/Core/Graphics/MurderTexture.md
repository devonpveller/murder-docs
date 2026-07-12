# MurderTexture

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct MurderTexture
```

A unified texture handle that can represent either an `AtlasCoordinates` sprite frame or a standalone `Texture2D` loaded by file path.

**Intent:** Provides a single value type that works with both atlas-packed sprites and raw textures, so rendering code does not need to branch on the source type.

**Use-case:** Construct with an `AtlasCoordinates` for atlas sprites or with a string path for standalone textures; call `Draw()` to render and `Preload()` to warm the texture cache before first use.

### ⭐ Constructors

```csharp
public MurderTexture(AtlasCoordinates AtlasCoordinates)
```

Creates a `MurderTexture` backed by an atlas-packed sprite frame.

**Parameters** \
`AtlasCoordinates` [AtlasCoordinates](../../../Murder/Core/Graphics/AtlasCoordinates.html) \

```csharp
public MurderTexture(string texture)
```

Creates a `MurderTexture` backed by a standalone texture loaded from the given file path.

**Parameters** \
`texture` [string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### Draw(Batch2D, Vector2, Vector2, Rectangle, Color, ImageFlip, float, Vector3)

```csharp
public void Draw(Batch2D batch2D, Vector2 position, Vector2 scale, Rectangle clip, Color color, ImageFlip flip, float sort, Vector3 blend)
```

Draws a texture with a clipping area.

**Parameters** \
`batch2D` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`scale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`clip` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \
`flip` [ImageFlip](../../../Murder/Core/Graphics/ImageFlip.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`blend` [Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### Preload()

```csharp
public void Preload()
```

Ensures the underlying standalone texture is loaded into memory; no-op for atlas-backed textures. Call this during a loading screen to avoid hitches on first render.

⚡
