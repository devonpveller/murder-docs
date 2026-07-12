# TileDimensions

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed struct TileDimensions
```

Describes a rectangular pixel-space area — an origin offset plus a size.

**Intent:** Used to describe a prefab/entity's footprint when it is drawn or placed on the grid, e.g. in the map editor's grid snapping/selection tools.

**Use-case:** `PrefabAsset.Dimensions` stores one of these to describe how the prefab should be sized and offset when rendered on the map or in the editor. It converts implicitly to `Rectangle`, so it can be passed anywhere a `Rectangle` is expected (bounds checks, drawing calls) without an explicit cast.

### ⭐ Constructors

```csharp
public TileDimensions(Vector2 origin, Point size)
```

Creates a `TileDimensions` with the specified pixel origin and size.

**Parameters** \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Point](../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties

#### Origin

```csharp
public Vector2 Origin;
```

The pixel-space top-left offset of the area.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Size

```csharp
public Point Size;
```

The width and height of the area, in pixels.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

### ⭐ Methods

#### op_Implicit(TileDimensions)

```csharp
public static implicit operator Rectangle(TileDimensions t)
```

Implicitly converts this `TileDimensions` into an equivalent `Rectangle` (using `Origin` as the position and `Size` as the dimensions), so it can be passed anywhere a `Rectangle` is expected without an explicit cast.

**Parameters** \
`t` [TileDimensions](../../Murder/Core/TileDimensions.html) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

⚡
