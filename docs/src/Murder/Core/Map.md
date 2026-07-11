# Map

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class Map
```

Runtime tile-based map that stores per-cell collision masks and floor-type data for a level.

**Intent:** The authoritative spatial data structure for tile collision, pathfinding weights, and floor properties within a scene.

**Use-case:** Systems that move actors, cast rays, or run pathfinding query this map to determine whether a cell is solid, a trigger, a hole, or passable.

### ⭐ Constructors
```csharp
public Map(int width, int height)
```

Creates a map with the specified tile dimensions, initializing all cells to empty.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Height
```csharp
public readonly int Height;
```

The height of the map in tile units.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Width
```csharp
public readonly int Width;
```

The width of the map in tile units.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### HasCollision(int, int, int)
```csharp
public bool HasCollision(int x, int y, int layer)
```

Returns `true` when the tile at `(x, y)` has the specified collision layer bit set.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`layer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasCollision(int, int, int, int, int)
```csharp
public bool HasCollision(int x, int y, int width, int height, int mask)
```

Returns `true` when any tile within the axis-aligned rectangle `(x, y, width, height)` matches the given collision `mask`.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasLineOfSight(Point, Point, bool, int)
```csharp
public bool HasLineOfSight(Point start, Point end, bool excludeEdges, int blocking)
```

A fast Line of Sight check
            It is not exact by any means, just tries to draw A line of tiles between start and end.

**Parameters** \
`start` [Point](../../Murder/Core/Geometry/Point.html) \
\
`end` [Point](../../Murder/Core/Geometry/Point.html) \
\
`excludeEdges` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\
`blocking` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
\

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### IsInsideGrid(int, int)
```csharp
public bool IsInsideGrid(int x, int y)
```

Returns `true` when the tile coordinates `(x, y)` fall within the map bounds.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsObstacle(Point)
```csharp
public bool IsObstacle(Point p)
```

Returns `true` when the tile at `p` has the `SOLID` collision layer set, making it impassable.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsObstacleOrBlockVision(Point)
```csharp
public bool IsObstacleOrBlockVision(Point p)
```

Returns `true` when the tile at `p` is either a solid obstacle or marked as vision-blocking.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetStaticCollisions(IntRectangle)
```csharp
public IEnumerable<T> GetStaticCollisions(IntRectangle rect)
```

Enumerates all static collision entries whose bounds overlap the given rectangle.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### FloorAt(Point)
```csharp
public int FloorAt(Point p)
```

Returns the floor-type identifier stored in the floor map at tile position `p`.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetCollision(int, int)
```csharp
public int GetCollision(int x, int y)
```

Returns the raw collision bitmask for the tile at `(x, y)`, or `SOLID` if the position is outside the grid.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### WeightAt(Point)
```csharp
public int WeightAt(Point p)
```

Returns the pathfinding traversal weight for the tile at position `p`.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### WeightAt(int, int)
```csharp
public int WeightAt(int x, int y)
```

Returns the pathfinding traversal weight for the tile at `(x, y)`.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetGridMap(int, int)
```csharp
public MapTile GetGridMap(int x, int y)
```

Returns the `MapTile` data stored at `(x, y)`. Returns a solid tile for out-of-bounds coordinates.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[MapTile](../../Murder/Core/MapTile.html) \

#### HasCollisionAt(IntRectangle, int)
```csharp
public T? HasCollisionAt(IntRectangle rect, int mask)
```

Checks whether any tile within `rect` matches the collision `mask`, returning the first matching tile info or null.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### HasCollisionAt(int, int, int, int, int)
```csharp
public T? HasCollisionAt(int x, int y, int width, int height, int mask)
```

Check for collision using tiles coordinates.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### OverrideValueAt(Point, int, int)
```csharp
public void OverrideValueAt(Point p, int collisionMask, int weight)
```

Force-sets the collision mask and pathfinding weight for the tile at `p`, replacing whatever was there.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetFloorAt(IntRectangle, int)
```csharp
public void SetFloorAt(IntRectangle rect, int type)
```

Sets the floor-type identifier for every tile within the given rectangle.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`type` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetFloorAt(int, int, int)
```csharp
public void SetFloorAt(int x, int y, int type)
```

Sets the floor-type identifier for the single tile at `(x, y)`.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`type` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetOccupied(Point, int, int)
```csharp
public void SetOccupied(Point p, int collisionMask, int weight)
```

Marks the tile at `p` as occupied by OR-ing in the given `collisionMask` and setting its traversal weight.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetOccupiedAsCarve(IntRectangle, bool, bool, bool, int)
```csharp
public void SetOccupiedAsCarve(IntRectangle rect, bool blockVision, bool isObstacle, bool isClearPath, int weight)
```

Applies carve-layer collision flags to all tiles in `rect`, controlling whether they block vision, act as obstacles, or clear the path.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`blockVision` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`isObstacle` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`isClearPath` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetOccupiedAsStatic(int, int, int)
```csharp
public void SetOccupiedAsStatic(int x, int y, int layer)
```

Marks a single tile as statically occupied on the given collision layer (used for tilemap geometry baked at load time).

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`layer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetUnoccupied(Point, int, int)
```csharp
public void SetUnoccupied(Point p, int collisionMask, int weight)
```

Clears the given `collisionMask` bits from the tile at `p` and resets its traversal weight.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetUnoccupiedCarve(IntRectangle, bool, bool, int)
```csharp
public void SetUnoccupiedCarve(IntRectangle rect, bool blockVision, bool isObstacle, int weight)
```

Removes carve-layer collision flags from all tiles in `rect`.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`blockVision` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`isObstacle` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ZeroAll()
```csharp
public void ZeroAll()
```

Resets all tile collision masks and pathfinding weights to zero, effectively clearing the entire map.



⚡