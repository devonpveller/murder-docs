# GeometryServices

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
public static class GeometryServices
```

Math and geometry utilities for overlap tests, distance calculations, polygon analysis, rectangle manipulation, and cached shape-point generation (circles and triangles).

**Intent:** Centralizes pure geometry helpers that don't depend on ECS/world state, including caches (`GetUnitCircle`, `GetCircle`, `GetTriangle`, `GetUnitTriangle`) for expensive-to-regenerate point sets used repeatedly for rendering or collision approximation.

**Use-case:** Use for point-in-rectangle tests (`InRect`), overlap/intersection checks (`CheckOverlap`, `IntersectsCircle`), distance calculations (`Distance`, `DistanceLinePoint`, `DistanceRectPoint`), rectangle resizing (`Shrink`, `Expand`), polygon analysis (`SignedPolygonArea`, `IsConvex`), and generating cached circle/triangle vertex arrays for debug drawing or approximate collision shapes without recomputing trigonometry every call.

### ⭐ Methods

#### GetUnitCircle(int)

```csharp
public static ImmutableArray<Vector2> GetUnitCircle(int sides)
```

Gets or creates (and caches) a unit circle (radius `1.0`) approximated with `sides` vertices. Equivalent to `GetCircle(1f, sides)`; kept as a separate entry point for the common case of needing a normalized circle to scale/transform yourself.

**Parameters** \
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetCircle(float, int)

```csharp
public static ImmutableArray<Vector2> GetCircle(float radius, int sides)
```

Gets or creates (and caches, keyed by a quantized radius/side count) a circle of the given `radius` approximated with `sides` vertices, going clockwise starting from the top. Repeated calls with the same (quantized) radius and side count reuse the cached array instead of recomputing trigonometry, which matters for shapes regenerated every frame (e.g. debug-drawing a collider radius).

**Parameters** \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`sides` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetTriangle(float, float)

```csharp
public static ImmutableArray<Vector2> GetTriangle(float radius, float rotation = 0f)
```

Gets or creates (and caches) an equilateral triangle pointing up, with vertices at distance `radius` from the center, rotated by `rotation` radians (`0` = pointing up). The returned array closes the loop (the first vertex is repeated at the end) so it can be drawn directly as a connected outline.

**Parameters** \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### GetUnitTriangle(float)

```csharp
public static ImmutableArray<Vector2> GetUnitTriangle(float rotation = 0f)
```

Gets a unit triangle (radius `1.0`) pointing up, optionally rotated. Equivalent to `GetTriangle(1f, rotation)`.

**Parameters** \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### CheckOverlap(float, float, float, float)

```csharp
public static bool CheckOverlap(float minA, float maxA, float minB, float maxB)
```

Returns `true` if the 1D ranges `[minA, maxA]` and `[minB, maxB]` overlap at any point. The building block for separating-axis-style overlap tests.

**Parameters** \
`minA` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`maxA` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`minB` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`maxB` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CheckOverlap((float, float), (float, float))

```csharp
public static bool CheckOverlap((float Min, float Max) a, (float Min, float Max) b)
```

Tuple-based overload of `CheckOverlap` for when a projection range is already expressed as a `(Min, Max)` pair (e.g. from an SAT-style projection helper), avoiding manual field unpacking.

**Parameters** \
`a` [ValueTuple\<float, float\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \
`b` [ValueTuple\<float, float\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### CheckOverlap((float, float), (float, float), float)

```csharp
public static bool CheckOverlap((float Min, float Max) projectionA, (float Min, float Max) projectionB, float epsilon)
```

Tolerant variant of the tuple-based `CheckOverlap` that treats ranges within `epsilon` of touching as overlapping. Use this instead of the exact overload when floating-point error could otherwise cause a should-be-touching pair of shapes to be reported as not overlapping (or vice versa).

**Parameters** \
`projectionA` [ValueTuple\<float, float\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \
`projectionB` [ValueTuple\<float, float\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \
`epsilon` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### InRect(float, float, Rectangle)

```csharp
public static bool InRect(float x, float y, Rectangle rect)
```

Returns `true` if the point `(x, y)` lies strictly inside `rect` (edges are exclusive — a point exactly on the boundary returns `false`).

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### InRect(float, float, float, float, float, float)

```csharp
public static bool InRect(float x, float y, float rx, float ry, float rw, float rh)
```

Same strict point-in-rectangle test as `InRect(float, float, Rectangle)`, but with the rectangle expressed as separate `x`/`y`/`width`/`height` values instead of a `Rectangle`, for call sites that don't already have one constructed.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rx` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`ry` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rw` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rh` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### InRect(Vector2, Rectangle)

```csharp
public static bool InRect(Vector2 xy, Rectangle rect)
```

`Vector2` convenience overload of `InRect(float, float, Rectangle)`.

**Parameters** \
`xy` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`rect` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RoundedDecimals(float)

```csharp
public static float RoundedDecimals(float x)
```

Returns the fractional (decimal) part of `x` (`x - MathF.Floor(x)`). Despite the name, this is currently identical to `Decimals` — no rounding is applied.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Decimals(float)

```csharp
public static float Decimals(float x)
```

Returns the fractional (decimal) part of `x` (`x - MathF.Floor(x)`).

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Distance(float, float, float, float)

```csharp
public static float Distance(float x1, float y1, float x2, float y2)
```

Standard Euclidean distance between points `(x1, y1)` and `(x2, y2)`.

**Parameters** \
`x1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`x2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DistanceRectPoint(float, float, float, float, float, float)

```csharp
public static float DistanceRectPoint(float px, float py, float rx, float ry, float rw, float rh)
```

Finds the shortest distance between the point `(px, py)` and the rectangle `(rx, ry, rw, rh)`; returns `0` if the point is inside (or on the edge of) the rectangle. Used, for example, when ranking or filtering entities by proximity to a target area rather than a target point.

**Parameters** \
`px` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`py` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rx` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`ry` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rw` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rh` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### DistanceLinePoint(float, float, float, float, float, float)

```csharp
public static float DistanceLinePoint(float x, float y, float x1, float y1, float x2, float y2)
```

Finds the shortest distance between the point `(x, y)` and the line *segment* from `(x1, y1)` to `(x2, y2)` (the closest point on the segment is clamped to its endpoints, it does not treat the line as infinite). Falls back to a plain point-distance if the segment has zero length.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`x1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y1` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`x2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y2` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SignedPolygonArea(Vector2[])

```csharp
public static float SignedPolygonArea(Vector2[] vertices)
```

Calculates the signed area of a polygon using the shoelace formula. The sign indicates winding order: positive for clockwise vertices, negative for counter-clockwise. Use the sign to detect or normalize polygon winding order before further processing (e.g. triangulation or convexity checks).

**Parameters** \
`vertices` [Vector2[]](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### IsConvex(Vector2[], bool)

```csharp
public static bool IsConvex(Vector2[] vertices, bool isClockwise)
```

Determines whether the polygon described by `vertices` is convex, by walking its internal angles and checking that the cumulative turn never exceeds 180°. The caller must specify `isClockwise` to match the polygon's actual winding order (e.g. as determined by `SignedPolygonArea`), since the angle-sign convention depends on it.

**Parameters** \
`vertices` [Vector2[]](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`isClockwise` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IntersectsCircle(Rectangle, Vector2, float)

```csharp
public static bool IntersectsCircle(this Rectangle rectangle, Vector2 circleCenter, float circleRadiusSquared)
```

Extension method returning `true` if `rectangle` overlaps the circle defined by `circleCenter` and `circleRadiusSquared` (a squared radius, to avoid a `sqrt` at the call site — pass `radius * radius`). Uses the standard "closest point on rectangle to circle center" distance check.

**Parameters** \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`circleCenter` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`circleRadiusSquared` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Shrink(Rectangle, int)

```csharp
public static Rectangle Shrink(this Rectangle rectangle, int amount)
```

Extension method returning a new rectangle inset by `amount` pixels on every side (width/height each shrink by `2 * amount`). Pass a negative `amount` to grow the rectangle instead.

**Parameters** \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`amount` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### Expand(Rectangle, Vector2)

```csharp
public static Rectangle Expand(this Rectangle rectangle, Vector2 size)
```

Extension method returning a new rectangle with the same position but `Width`/`Height` increased by `size.X`/`size.Y` respectively (unlike `Shrink`, this only grows from the bottom-right — the top-left corner does not move).

**Parameters** \
`rectangle` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### PointInCircleEdge(float)

```csharp
public static Vector2 PointInCircleEdge(float percent)
```

Returns a unit-circle point at the angle corresponding to `percent`, where `0`–`1` maps to `0`–`360` degrees. Useful for evenly distributing points/entities around a circle by iterating `percent` from `0` to `1`.

**Parameters** \
`percent` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetOuterIntersection(Rectangle, Rectangle)

```csharp
public static IList<Rectangle> GetOuterIntersection(Rectangle a, Rectangle b)
```

Returns the sub-rectangles of `b` that fall *outside* `a` — i.e. the parts of `b` not covered by `a` — split into up to four pieces (above, below, left, right of `a`). Returns an empty list if `b` is fully contained by `a`. Used by `IsValidPosition` to determine how much of a candidate rectangle spills outside a given collider area.

**Parameters** \
`a` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \
`b` [Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[IList\<Rectangle\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \

#### IsValidPosition(IntRectangle[], Vector2, Point)

```csharp
public static bool IsValidPosition(IntRectangle[] area, Vector2 endPosition, Point size)
```

Checks whether a rectangle of `size` placed at `endPosition` is fully covered by the union of the rectangles in `area` — either because it fits entirely within a single entry, or because the parts of it that spill outside each entry (via `GetOuterIntersection`) are each covered by one of the *other* entries in `area`. Returns `false` if `area` is empty. Used to validate that a candidate placement (e.g. for `PhysicsServices.FindNextAvailablePosition`) actually lands on walkable/allowed ground rather than partially off the edge of it.

**Parameters** \
`area` [IntRectangle[]](../../Murder/Core/Geometry/IntRectangle.html) \
`endPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Point](../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
