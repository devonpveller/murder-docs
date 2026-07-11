# CellProperties

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct CellProperties
```

Stores the pathfinding properties of a single tile in the navigation grid.

**Intent:** Encodes per-cell overrides for movement cost and collision layer so the pathfinding system can treat individual tiles differently from the map defaults.

**Use-case:** Used internally by `PathfindGridComponent.Cells` to record which tiles have custom weights or collision masks authored in the editor.

### ⭐ Constructors
```csharp
public CellProperties(Point coordinates, int weight, int collisionMask)
```

Creates a cell entry at `coordinates` with explicit weight and collision mask.

**Parameters** \
`coordinates` [Point](../../Murder/Core/Geometry/Point.html) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public CellProperties(Point coordinates)
```

Creates a cell entry at `coordinates` with default weight (`0`) and no collision mask.

**Parameters** \
`coordinates` [Point](../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties
#### CollisionMask
```csharp
public int CollisionMask { get; public set; }
```

Bitmask of `CollisionLayersBase` flags that apply to this tile; controls which physics layers treat the cell as blocked.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Point
```csharp
public Point Point { get; public set; }
```

Tile-space grid coordinates of this cell.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### Weight
```csharp
public int Weight { get; public set; }
```

Pathfinding traversal cost for this cell; higher values make the pathfinder prefer alternative routes.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡