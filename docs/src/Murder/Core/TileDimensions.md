# TileDimensions

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct TileDimensions
```

Describes the pixel origin and tile-size of a single tile for use during rendering and placement calculations.

**Intent:** Bundles the pixel-space origin offset and the tile dimensions needed when drawing a tile sprite at a grid position.

**Use-case:** Returned from tile asset queries so rendering systems know exactly where to place and how large each tile's sprite should be.

### ⭐ Constructors
```csharp
public TileDimensions(Vector2 origin, Point size)
```

Creates a `TileDimensions` with the specified pixel origin and tile size.

**Parameters** \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Point](../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties
#### Origin
```csharp
public Vector2 Origin;
```

The pixel-space offset from the top-left of the grid cell to where this tile's sprite should be drawn.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Size
```csharp
public Point Size;
```

The width and height of this tile in pixels.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \


⚡