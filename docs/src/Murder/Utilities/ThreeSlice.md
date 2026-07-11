# ThreeSlice

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed struct ThreeSlice
```

A runtime three-slice drawable that holds a resolved `SpriteAsset` reference and the core (middle) region rectangle used for stretching.

**Intent:** Represents a fully resolved, draw-ready three-slice sprite whose end caps are drawn at native size and whose core region is stretched to fill the target area.

**Use-case:** Construct from a `ThreeSliceInfo` (which stores only the GUID) and call `Draw` to render a scalable bordered sprite such as a text box or button.

### ⭐ Constructors
```csharp
public ThreeSlice(ThreeSliceInfo info)
```

**Parameters** \
`info` [ThreeSliceInfo](../../Murder/Utilities/ThreeSliceInfo.html) \

### ⭐ Properties
#### Core
```csharp
public readonly Rectangle Core;
```

The rectangle within the sprite that is tiled or stretched (the middle section); the end caps outside this region are drawn at their native pixel size.

**Returns**
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

Renders this three-slice to the batch, stretching the core region to fill the `target` rectangle while drawing the end caps at their native size.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`target` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`orientation` [Orientation](../../Murder/Core/Orientation.html) \
`sort` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \



⚡