# PositionExtensions

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class PositionExtensions
```

Extension methods bridging [PositionComponent](../../Bang/Components/PositionComponent.html) (Bang's built-in transform component), `System.Numerics.Vector2`/[Point](../../Murder/Core/Geometry/Point.html), and the tile grid (`Grid.CellSize`).

**Intent:** Used throughout rendering, physics and AI systems whenever a position needs to move between "local component space", "world-space pixels" and "grid cell coordinates".

**Use-case:** Call the `Entity`-based overloads (`GetGlobalPosition`, `SetGlobalPosition`, `SetLocalPosition`) when working with a live entity, and the `PositionComponent`/`Vector2`/`Point` overloads when transforming raw coordinates (e.g. converting a mouse click to a grid cell, or offsetting a component's position by a delta).

### ⭐ Methods

#### GetGlobalPosition(Entity)

```csharp
public Vector2 GetGlobalPosition(Entity entity)
```

Returns the entity's resolved world-space position (i.e. including any parent offset via `PositionComponent.GetGlobal`). Logs an error and returns `Vector2.Zero` if the entity has no `PositionComponent` or is no longer active — prefer `TryGetGlobalPosition` when the entity might legitimately lack a position.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### TryGetGlobalPosition(Entity)

```csharp
public Vector2? TryGetGlobalPosition(Entity entity)
```

Returns the entity's resolved world-space position, or `null` if the entity has no `PositionComponent`. Delegates to `EntityServices.GetGlobalPositionIfValid`. The safe counterpart to `GetGlobalPosition` for code paths where a missing position is expected (e.g. checking two entities before a distance test).

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0)? \

#### SetLocalPosition(Entity, Vector2)

```csharp
public void SetLocalPosition(Entity entity, Vector2 position)
```

Sets the entity's position relative to its parent (if any), preserving the parent relationship. Reads the current `PositionComponent`, applies `PositionComponent.WithLocal(float, float)`, and replaces the component. Use this instead of directly replacing the component when the entity may be parented, so the cached global position stays consistent.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SetGlobalPosition(Entity, Vector2)

```csharp
public void SetGlobalPosition(Entity entity, Vector2 position)
```

Moves the entity to an absolute world-space position. If the entity already has a `PositionComponent`, this preserves its parent relationship via `PositionComponent.SetGlobal` (adjusting the local offset accordingly); otherwise it simply assigns `position` as a brand-new, unparented position.

**Parameters** \
`entity` [Entity](../../Bang/Entities/Entity.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToPosition(Point)

```csharp
public PositionComponent ToPosition(Point position)
```

Wraps an integer grid `Point` in a new, unparented `PositionComponent` (component space, not pixel space).

**Parameters** \
`position` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### ToPosition(Vector2)

```csharp
public PositionComponent ToPosition(Vector2 position)
```

Wraps a `Vector2` in a new, unparented `PositionComponent`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### FromCellToVector2Position(Point)

```csharp
public Vector2 FromCellToVector2Position(Point point)
```

Converts a tile-grid cell coordinate to the world-space pixel position of its top-left corner.

**Parameters** \
`point` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### FromWorldToLowerBoundGridPosition(Point)

```csharp
public Point FromWorldToLowerBoundGridPosition(Point point)
```

Snaps a world-space pixel position down (floor) to the grid cell that contains it.

**Parameters** \
`point` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### FromCellToVector2CenterPosition(Point)

```csharp
public Vector2 FromCellToVector2CenterPosition(Point point)
```

Converts a tile-grid cell coordinate to the world-space pixel position at the center of that cell.

**Parameters** \
`point` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### FromCellToPointPosition(Point)

```csharp
public Point FromCellToPointPosition(Point point)
```

Converts a tile-grid cell coordinate to the world-space pixel position of its top-left corner, as a `Point`.

**Parameters** \
`point` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToSysVector2(PositionComponent)

```csharp
public Vector2 ToSysVector2(PositionComponent position)
```

Returns the component's local X/Y as a `Vector2`. Equivalent to `PositionComponent.Vector2`.

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToPoint(PositionComponent)

```csharp
public Point ToPoint(PositionComponent position)
```

Returns the component's local X/Y rounded to the nearest integer `Point`.

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToCellPoint(PositionComponent)

```csharp
public Point ToCellPoint(PositionComponent position)
```

Returns the tile-grid cell that this component's local position falls in.

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToCellPoint(Vector2)

```csharp
public Point ToCellPoint(Vector2 v)
```

Returns the tile-grid cell that a world-space `Vector2` falls in (floor of position divided by `Grid.CellSize`).

**Parameters** \
`v` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToVector2(PositionComponent)

```csharp
public Vector2 ToVector2(PositionComponent position)
```

Returns the component's local X/Y as a `Vector2`. Equivalent to `ToSysVector2`.

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### AddToVector2(PositionComponent, Vector2)

```csharp
public Vector2 AddToVector2(PositionComponent position, Vector2 delta)
```

Returns the component's local X/Y offset by `delta`, as a plain `Vector2` (does not create a new component).

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \
`delta` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### AddToVector2(PositionComponent, float, float)

```csharp
public Vector2 AddToVector2(PositionComponent position, float dx, float dy)
```

Returns the component's local X/Y offset by (`dx`, `dy`), as a plain `Vector2` (does not create a new component).

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \
`dx` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`dy` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Add(PositionComponent, float, float)

```csharp
public PositionComponent Add(PositionComponent position, float dx, float dy)
```

Returns a new `PositionComponent` with local X/Y offset by (`dx`, `dy`). Note this discards any cached global/parent position, same as `PositionComponent`'s own `operator +`.

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \
`dx` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`dy` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### Add(PositionComponent, Vector2)

```csharp
public PositionComponent Add(PositionComponent position, Vector2 delta)
```

Returns a new `PositionComponent` with local X/Y offset by `delta`.

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \
`delta` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### Add(PositionComponent, Point)

```csharp
public PositionComponent Add(PositionComponent position, Point delta)
```

Returns a new `PositionComponent` with local X/Y offset by the integer `delta`.

**Parameters** \
`position` [PositionComponent](../../Bang/Components/PositionComponent.html) \
`delta` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### IsSameCell(PositionComponent, PositionComponent)

```csharp
public bool IsSameCell(PositionComponent this, PositionComponent other)
```

Returns `true` if both components' local positions fall in the same tile-grid cell.

**Parameters** \
`this` [PositionComponent](../../Bang/Components/PositionComponent.html) \
`other` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CellPoint(PositionComponent)

```csharp
public Point CellPoint(PositionComponent this)
```

Returns the tile-grid cell that this component's local position falls in.

**Parameters** \
`this` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

⚡
