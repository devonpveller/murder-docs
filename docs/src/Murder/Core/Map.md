# Map

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public class Map
```

The authoritative runtime, tile-based spatial data structure for a level: a flat grid of `MapTile` collision/weight data plus a parallel floor-type grid.

**Intent:** Systems that move actors, carve out collision from level geometry or dynamic obstacles, cast lines of sight, or run pathfinding all query (and, for carve-style systems, mutate) this map rather than talking to entities directly — it is the single source of truth for "what is at this tile" once a world has been built.

**Use-case:** Built once per world by the map-initialization systems (e.g. baking tilemap collision via `SetOccupiedAsStatic`), then queried every frame by movement, physics, and pathfinding systems (`At`, `HasCollision`, `IsObstacle`, `WeightAt`), and mutated at runtime by entities carrying a `CarveComponent` as they move (`SetOccupiedAsCarve`/`SetUnoccupiedCarve`).

### ⭐ Constructors

```csharp
public Map(Point origin, int width, int height)
```

Allocates a new, empty `width` x `height` map with every tile at its default (no collision, weight 1) state. Marked as the JSON constructor so a serialized `Map` is rebuilt with the correct dimensions before its tile arrays are populated.

**Parameters** \
`origin` [Point](../../Murder/Core/Geometry/Point.html) \
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

#### Origin

```csharp
public readonly Point Origin;
```

Origin offset used only for visualization/editor purposes; this is **not** added to `Width`/`Height` and does not shift the coordinate space that `At`/`GetGridMap`/etc. operate in.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Width

```csharp
public readonly int Width;
```

The width of the map in tile units.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### At(int, int)

```csharp
public int At(int x, int y)
```

Returns the raw collision bitmask for the tile at `(x, y)`, or `SOLID | BLOCK_VISION` if the position is outside the grid. This is the lowest-level collision read; most callers prefer `HasCollision`, `IsObstacle`, or `IsObstacleOrBlockVision`, which build on top of it.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### FloorAt(Point)

```csharp
public int FloorAt(Point p)
```

Returns the floor-type identifier stored in the floor map at tile position `p`, or `-1` if `p` is outside the grid.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetGridMap(int, int)

```csharp
public MapTile GetGridMap(int x, int y)
```

Returns the full `MapTile` (collision mask and pathfinding weight together) stored at `(x, y)`. Out-of-bounds coordinates report a synthetic solid tile so callers don't need a separate bounds check before treating map edges as impassable.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[MapTile](../../Murder/Core/MapTile.html) \

#### GetStaticCollisions(IntRectangle)

```csharp
public IEnumerable<Point> GetStaticCollisions(IntRectangle rect)
```

Enumerates every tile position within (or bordering) `rect` that has the `SOLID` collision layer set. A thin wrapper over the internal collision-scanning enumerator fixed to the `SOLID` mask.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[IEnumerable\<Point\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### HasCollision(int, int, int)

```csharp
public bool HasCollision(int x, int y, int layer)
```

Returns `true` when the tile at `(x, y)` has any bit of the specified collision `layer` set.

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

Returns `true` when any tile within the axis-aligned rectangle `(x, y, width, height)` matches the given collision `mask`, or when the rectangle falls (even partially) outside the map bounds — out-of-bounds space is treated as always colliding.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### HasCollisionAt(IntRectangle, int)

```csharp
public Point? HasCollisionAt(IntRectangle rect, int mask)
```

Checks tiles within `rect` for a match against `mask`, returning the tile-space position of the first match (including synthetic out-of-bounds edge positions) or `null` if none is found. Forwards to the `(x, y, width, height, mask)` overload.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Point?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### HasCollisionAt(int, int, int, int, int)

```csharp
public Point? HasCollisionAt(int x, int y, int width, int height, int mask)
```

Check for collision using tile coordinates, scanning the rectangle `(x, y, width, height)` for the first tile matching `mask`. Positions outside the map bounds are reported as colliding (clamped to the nearest edge coordinate) rather than silently ignored, so callers can detect a shape that would extend off the map.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`mask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Point?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### HasLineOfSight(Point, Point, bool, int)

```csharp
public bool HasLineOfSight(Point start, Point end, bool excludeEdges, int blocking)
```

A fast line-of-sight check. It is not exact by any means — it just walks the tiles that a straight line from `start` to `end` would pass through and tests each against the `blocking` mask.

**Parameters** \
`start` [Point](../../Murder/Core/Geometry/Point.html) \
`end` [Point](../../Murder/Core/Geometry/Point.html) \
`excludeEdges` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`blocking` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsInsideGrid(int, int)

```csharp
public bool IsInsideGrid(int x, int y)
```

Returns `true` when the tile coordinates `(x, y)` fall within `[0, Width)` x `[0, Height)`.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsObstacle(Point)

```csharp
public bool IsObstacle(Point p)
```

Returns `true` when the tile at `p` has the `SOLID` or `HOLE` collision layer set, making it impassable.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsObstacleOrBlockVision(Point)

```csharp
public bool IsObstacleOrBlockVision(Point p)
```

Returns `true` when the tile at `p` is a solid obstacle, a hole, or marked as vision-blocking.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### OverrideValueAt(Point, int, int)

```csharp
public void OverrideValueAt(Point p, int collisionMask, int weight)
```

Force-sets the collision mask and pathfinding weight for the tile at `p`, replacing whatever was there. No-ops if `p` is outside the grid.

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

Marks the tile at `p` as occupied by OR-ing in the given `collisionMask` and adding to its traversal weight. A 1x1 shortcut over `SetGridCollision`, used by dynamic carve entities as they move onto a tile.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetOccupiedAsCarve(IntRectangle, CarveComponent)

```csharp
public void SetOccupiedAsCarve(IntRectangle rect, CarveComponent carve)
```

Applies a `CarveComponent`'s configuration to every tile in `rect`: sets the `CARVE` layer (plus `BLOCK_VISION`/`SOLID` as configured), or, when `CarveComponent.ClearPath` is set, instead removes collision layers to re-open a path (e.g. for a bridge or door placed over otherwise-blocking terrain). This is how carve entities (anything with a `CarveComponent`) stamp their footprint into the map.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`carve` [CarveComponent](../../Murder/Components/CarveComponent.html) \

#### SetOccupiedAsStatic(int, int, int, bool)

```csharp
public void SetOccupiedAsStatic(int x, int y, int layer, bool @override = false)
```

Marks a single tile as statically occupied on the given collision `layer` — used by map-building systems to bake tilemap/level geometry collision into the map at load time, as opposed to the dynamic, weight-tracking `SetOccupied`/`SetUnoccupied` pair used for carve entities that can move or be added/removed at runtime.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`layer` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`override` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SetUnoccupied(Point, int, int)

```csharp
public void SetUnoccupied(Point p, int collisionMask, int weight)
```

Clears the given `collisionMask` bits from the tile at `p` and reduces its traversal weight back down (clamped to a minimum of 1). The inverse of `SetOccupied`, called when a carve entity moves off a tile.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### SetUnoccupiedCarve(IntRectangle, bool, bool, int)

```csharp
public void SetUnoccupiedCarve(IntRectangle rect, bool blockVision, bool isObstacle, int weight)
```

Removes carve-layer collision flags (`CARVE`, plus `BLOCK_VISION`/`SOLID` as specified) from all tiles in `rect`. The inverse of `SetOccupiedAsCarve`, called when a carve entity is removed or moves away from the area.

**Parameters** \
`rect` [IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \
`blockVision` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`isObstacle` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### WeightAt(Point)

```csharp
public int WeightAt(Point p)
```

Returns the pathfinding traversal weight for the tile at position `p`, or `100` if `p` is outside the grid.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### WeightAt(int, int)

```csharp
public int WeightAt(int x, int y)
```

Returns the pathfinding traversal weight for the tile at `(x, y)`, or `100` if outside the grid.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ZeroAll()

```csharp
public void ZeroAll()
```

Resets every tile's collision mask and pathfinding weight to zero (rather than the default weight of 1), clearing the entire map to a fully-open, zero-cost state. Used when rebuilding the map from scratch before re-carving collision from level geometry.

⚡
