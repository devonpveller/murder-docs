# ThreeSlice

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public readonly struct ThreeSlice
```

The runtime, draw-ready counterpart to [ThreeSliceInfo](../../Murder/Utilities/ThreeSliceInfo.html): it eagerly resolves the info's image GUID into an actual `SpriteAsset` reference in its constructor, so `Draw` can render immediately without further asset lookups.

**Intent:** Represents a fully resolved, draw-ready three-slice sprite whose end caps are drawn at native size and whose core region is stretched to fill the target area.

**Use-case:** Construct from a `ThreeSliceInfo` (which stores only the GUID) and call `Draw` to render a scalable bordered sprite such as a text box or button. Used by `SpriteThreeSliceRenderSystem` to draw entities carrying a three-slice component.

### ⭐ Constructors

```csharp
public ThreeSlice(ThreeSliceInfo info)
```

Resolves `info`'s image GUID into an actual `SpriteAsset` reference via `Game.Data`, and copies its core rectangle.

**Parameters** \
`info` [ThreeSliceInfo](../../Murder/Utilities/ThreeSliceInfo.html) \

### ⭐ Properties

#### Core

```csharp
public readonly Rectangle Core;
```

The sub-rectangle of the sprite (in sprite pixel space) that gets stretched to fill the middle of the drawn area; the end caps outside this region are drawn at their native pixel size.

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### Image

```csharp
public readonly SpriteAsset Image;
```

The resolved `SpriteAsset` used to render this three-slice.

**Returns** \
[SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \

### ⭐ Methods

#### Draw(Batch2D, Rectangle, Vector2, Orientation, float)

```csharp
public void Draw(Batch2D batch, Rectangle target, Vector2 origin, Orientation orientation, float sort)
```

Draws this three-slice into `target`: the current animation frame of `Image` (evaluated at `Game.NowUnscaled`, looping) is stretched to fit, with the `Core` region scaled to fill the middle while the surrounding pixels are drawn as fixed-size end caps.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) — The batch to draw into. \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) — The destination rectangle (in world/screen space) to fill. \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) — Normalized draw origin/anchor (e.g. `Vector2Helper.Center`), same convention as other sprite draw calls. \
`orientation` [Orientation](../../Murder/Core/Orientation.html) — Flip/orientation to apply when drawing. \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Sort key controlling draw order relative to other batched draws. \

⚡
