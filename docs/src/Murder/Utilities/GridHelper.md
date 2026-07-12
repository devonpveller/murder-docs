# GridHelper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class GridHelper
```

Utility methods for enumerating tile-grid cell positions, snapping coordinates to the grid, and building cell rectangles.

**Intent:** Provides geometry and iteration helpers for working with the tile grid used by map and pathfinding systems.

**Use-case:** Call from map systems and AI code to enumerate cells in circular or linear areas, snap positions to the grid, find neighbouring cells for pathfinding, or convert between world-space and grid-cell coordinates.

### ⭐ Methods

#### Circle(int, int, int)

```csharp
public IEnumerable<T> Circle(int cx, int cy, int radius)
```

Returns all grid cell positions within a circular radius of the given center cell `(cx, cy)`.

**Parameters** \
`cx` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`cy` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`radius` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### Line(Point, Point)

```csharp
public IEnumerable<T> Line(Point start, Point end)
```

Returns all grid cell positions along the straight line from `start` to `end` using a Bresenham-style traversal.

**Parameters** \
`start` [Point](../../Murder/Core/Geometry/Point.html) \
`end` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### IsNeighbour(Point, Point, bool)

```csharp
public bool IsNeighbour(this Point p, Point otherP, bool includeDiagonals = true)
```

Returns `true` if `otherP` is directly adjacent to `p` (one of the four cardinal cells, or additionally one of the four diagonal cells if `includeDiagonals` is `true`, which is the default).

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`otherP` [Point](../../Murder/Core/Geometry/Point.html) \
`includeDiagonals` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Reverse(IDictionary<TKey, TValue>, Point, Point)

```csharp
public ComplexDictionary<Point, Point> Reverse(this IDictionary<Point, Point> input, Point initial, Point target)
```

Reverses a route dictionary produced by a pathfinder — where each entry maps a cell to the cell that leads *toward* `initial` — into the opposite direction (source-to-target order), by walking backward from `target` until it reaches `initial`. Used to convert a search-derived "came from" map into a directly walkable "go to next" map.

**Parameters** \
`input` [IDictionary\<Point, Point\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IDictionary-2?view=net-7.0) \
`initial` [Point](../../Murder/Core/Geometry/Point.html) \
`target` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[ComplexDictionary\<Point, Point\>](../../Murder/Serialization/ComplexDictionary-2.html) \

#### SnapToGridDelta(PositionComponent)

```csharp
public PositionComponent SnapToGridDelta(this PositionComponent transform)
```

Snaps `transform`'s local X/Y position down to the nearest grid cell boundary (i.e. floors each axis to a multiple of `Grid.CellSize`), returning the adjusted `PositionComponent`. Note this page previously (and incorrectly) documented this overload as taking an `IMurderTransformComponent`; the actual extension target is Bang's `PositionComponent`.

**Parameters** \
`transform` [PositionComponent](../../Bang/Components/PositionComponent.html) \

**Returns** \
[PositionComponent](../../Bang/Components/PositionComponent.html) \

#### FromTopLeftToBottomRight(Point, Point)

```csharp
public IntRectangle FromTopLeftToBottomRight(Point p1, Point p2)
```

Creates a rectangle from <paramref name="p1" /> to <paramref name="p2" />.

**Parameters** \
`p1` [Point](../../Murder/Core/Geometry/Point.html) \
`p2` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetBoundingBox(Rectangle)

```csharp
public IntRectangle GetBoundingBox(Rectangle rect)
```

Returns the smallest integer-cell rectangle that fully contains the given world-space `rect`.

**Parameters** \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### GetCarveBoundingBox(Rectangle, float)

```csharp
public IntRectangle GetCarveBoundingBox(Rectangle rect, float occupiedThreshold = .3f)
```

Like `GetBoundingBox`, but decides per-edge whether to floor or ceil to the grid based on how much of the boundary cell `rect` actually occupies: an edge is only expanded outward to the next cell if `rect` covers more than `occupiedThreshold` of that cell, otherwise it rounds inward. Used by `PhysicsServices.GetCarveBoundingBox` and `MapCarveCollisionSystem` to compute which grid cells a collider should mark as occupied ("carved") without over-claiming cells it barely overlaps.

**Parameters** \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`occupiedThreshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IntRectangle](../../Murder/Core/Geometry/IntRectangle.html) \

#### ToGrid(Point)

```csharp
public Point ToGrid(this Point position)
```

Converts a world-space `Point` (in pixels) to its containing grid cell coordinate by floor-dividing each axis by `Grid.CellSize`.

**Parameters** \
`position` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToGrid(Vector2)

```csharp
public Point ToGrid(this Vector2 position)
```

`Vector2` overload of `ToGrid(Point)`: converts a world-space position (in pixels) to its containing grid cell coordinate by floor-dividing each axis by `Grid.CellSize`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Neighbours(Point, int, int, bool)

```csharp
public ReadOnlySpan<T> Neighbours(Point p, int width, int height, bool includeDiagonals)
```

Returns all the neighbours of a position.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`includeDiagonals` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

#### Neighbours(Point, int, int, int, int, bool)

```csharp
public ReadOnlySpan<T> Neighbours(Point p, int x, int y, int edgeX, int edgeY, bool includeDiagonals)
```

Returns all the neighbours of a position.

**Parameters** \
`p` [Point](../../Murder/Core/Geometry/Point.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`edgeX` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`edgeY` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`includeDiagonals` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[ReadOnlySpan\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.ReadOnlySpan-1?view=net-7.0) \

#### FromTopLeftToBottomRight(Vector2, Vector2)

```csharp
public Rectangle FromTopLeftToBottomRight(Vector2 p1, Vector2 p2)
```

Creates a rectangle from <paramref name="p1" /> to <paramref name="p2" />.

**Parameters** \
`p1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`p2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### ToRectangle(Point)

```csharp
public Rectangle ToRectangle(Point grid)
```

**Parameters** \
`grid` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### SnapToGridDelta(Vector2)

```csharp
public Vector2 SnapToGridDelta(this Vector2 vector2)
```

`Vector2` overload of `SnapToGridDelta(PositionComponent)`: floors each axis down to the nearest multiple of `Grid.CellSize`.

**Parameters** \
`vector2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SnapToGridDelta(Point)

```csharp
public Point SnapToGridDelta(this Point point)
```

`Point` overload of `SnapToGridDelta(PositionComponent)`: floors each axis down to the nearest multiple of `Grid.CellSize`.

**Parameters** \
`point` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

⚡
