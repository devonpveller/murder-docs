# PositionExtensions

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class PositionExtensions
```

Extension methods for `IMurderTransformComponent` and related types for grid-coordinate conversion, global transform queries, and cell comparison.

**Intent:** Provides the coordinate-space conversions that game systems need when working with the tile grid and entity positions.

**Use-case:** Use in any system that needs to convert world-space positions to tile-grid cells, compare entity occupancy, or retrieve an entity's world-space position including parent transforms.

### ⭐ Methods
#### IsSameCell(IMurderTransformComponent, IMurderTransformComponent)
```csharp
public bool IsSameCell(IMurderTransformComponent this, IMurderTransformComponent other)
```

Returns `true` if both transforms occupy the same tile-grid cell.

**Parameters** \
`this` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \
`other` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetGlobalTransform(Entity)
```csharp
public IMurderTransformComponent GetGlobalTransform(Entity entity)
```

Returns the entity's transform in world space, composing all parent transforms up the hierarchy.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

#### CellPoint(IMurderTransformComponent)
```csharp
public Point CellPoint(IMurderTransformComponent this)
```

Returns the tile-grid cell coordinate of the transform as a `Point`.

**Parameters** \
`this` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### FromCellToPointPosition(Point&)
```csharp
public Point FromCellToPointPosition(Point& point)
```

Converts a tile-grid cell coordinate to its world-space pixel position (top-left of the cell).

**Parameters** \
`point` [Point&](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### FromWorldToLowerBoundGridPosition(Point&)
```csharp
public Point FromWorldToLowerBoundGridPosition(Point& point)
```

Snaps a world-space pixel position down to the lower-left corner of its enclosing grid cell.

**Parameters** \
`point` [Point&](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToCellPoint(IMurderTransformComponent)
```csharp
public Point ToCellPoint(IMurderTransformComponent position)
```

Converts the given world-space transform to its tile-grid cell coordinate.

**Parameters** \
`position` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToPoint(PositionComponent)
```csharp
public Point ToPoint(PositionComponent position)
```

Returns the position component's coordinates as an integer `Point`.

**Parameters** \
`position` [PositionComponent](../../Murder/Components/PositionComponent.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

```csharp
public PositionComponent Add(PositionComponent position, Point delta)
```

Returns a new `PositionComponent` offset from `position` by the integer `delta`.

**Parameters** \
`position` [PositionComponent](../../Murder/Components/PositionComponent.html) \
`delta` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[PositionComponent](../../Murder/Components/PositionComponent.html) \

```csharp
public PositionComponent Add(PositionComponent position, float dx, float dy)
```

Returns a new `PositionComponent` offset from `position` by the given float deltas.

**Parameters** \
`position` [PositionComponent](../../Murder/Components/PositionComponent.html) \
`dx` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`dy` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[PositionComponent](../../Murder/Components/PositionComponent.html) \

```csharp
public PositionComponent Add(PositionComponent position, Vector2 delta)
```

Returns a new `PositionComponent` offset from `position` by the given `Vector2` delta.

**Parameters** \
`position` [PositionComponent](../../Murder/Components/PositionComponent.html) \
`delta` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[PositionComponent](../../Murder/Components/PositionComponent.html) \

```csharp
public PositionComponent ToPosition(Point& position)
```

Converts an integer `Point` to a `PositionComponent`.

**Parameters** \
`position` [Point&](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[PositionComponent](../../Murder/Components/PositionComponent.html) \

```csharp
public PositionComponent ToPosition(Vector2& position)
```

Converts a `Vector2` to a `PositionComponent`.

**Parameters** \
`position` [Vector2&](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[PositionComponent](../../Murder/Components/PositionComponent.html) \

```csharp
public Vector2 AddToVector2(IMurderTransformComponent position, Vector2 delta)
```

Returns the transform's position as a `Vector2` offset by `delta`.

**Parameters** \
`position` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \
`delta` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public Vector2 AddToVector2(PositionComponent position, float dx, float dy)
```

Returns the position component as a `Vector2` offset by the given float deltas.

**Parameters** \
`position` [PositionComponent](../../Murder/Components/PositionComponent.html) \
`dx` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`dy` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### FromCellToVector2CenterPosition(Point&)
```csharp
public Vector2 FromCellToVector2CenterPosition(Point& point)
```

Converts a tile-grid cell coordinate to the world-space `Vector2` position at the center of that cell.

**Parameters** \
`point` [Point&](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### FromCellToVector2Position(Point&)
```csharp
public Vector2 FromCellToVector2Position(Point& point)
```

**Parameters** \
`point` [Point&](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToSysVector2(PositionComponent)
```csharp
public Vector2 ToSysVector2(PositionComponent position)
```

**Parameters** \
`position` [PositionComponent](../../Murder/Components/PositionComponent.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToVector2(IMurderTransformComponent)
```csharp
public Vector2 ToVector2(IMurderTransformComponent position)
```

**Parameters** \
`position` [IMurderTransformComponent](../../Murder/Components/IMurderTransformComponent.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SetGlobalPosition(Entity, Vector2)
```csharp
public void SetGlobalPosition(Entity entity, Vector2 position)
```

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SetGlobalTransform(Entity, T)
```csharp
public void SetGlobalTransform(Entity entity, T transform)
```

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`transform` [T](../../) \

#### SetLocalPosition(Entity, Vector2)
```csharp
public void SetLocalPosition(Entity entity, Vector2 position)
```

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \



⚡