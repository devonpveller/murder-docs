# Polygon

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct Polygon
```

An immutable convex (or concave) polygon defined by an ordered array of 2D vertices, in either clockwise or counter-clockwise winding depending on how it was built.

**Intent:** Store and query the vertex data for arbitrary 2D collision shapes and geometry operations, backing `PolygonShape` and freeform level geometry (e.g. rooms/triggers authored in the editor as vertex chains).

**Use-case:** Create a `Polygon` from a list of `Vector2` vertices and wrap it in a `PolygonShape` to use as a collision shape. Use `Contains()` for point-in-polygon tests, `Intersects(Polygon, Vector2, Vector2)` for SAT-based overlap resolution, and `GetLines()`/`EarClippingTriangulation()` for edge iteration and triangulation.

### ⭐ Constructors

```csharp
public Polygon()
```

Creates an empty polygon (no vertices). Because `Polygon` is a `record struct` with field initializers, this implicit parameterless constructor is available even though it's not explicitly written in source.

```csharp
public Polygon(ImmutableArray<Vector2> vertices)
```

Creates a polygon from an explicit list of vertices. This is the constructor used by JSON deserialization.

**Parameters** \
`vertices` [ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public Polygon(ImmutableArray<Vector2> vertices, Vector2 position)
```

Creates a polygon from `vertices`, translated by `position`.

**Parameters** \
`vertices` [ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### DIAMOND

```csharp
public readonly static Polygon DIAMOND;
```

A pre-built diamond (rhombus) polygon with vertices at (±10, 0) and (0, ±10). Handy as a quick default/placeholder shape, e.g. the default value of `PolygonShape.Polygon`.

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### EMPTY

```csharp
public readonly static Polygon EMPTY;
```

A polygon with no vertices, used as a default or sentinel/failure return value (e.g. by `MergePolygons(Polygon, Polygon)` when the inputs can't be merged).

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### Normals

```csharp
public Vector2[] Normals { get; }
```

The outward-facing edge normals of this polygon, one per edge, computed (and cached) lazily on first access. Used as the separating axes for SAT (Separating Axis Theorem) overlap tests in `Intersects(Polygon, Vector2, Vector2)`.

**Returns** \
[Vector2[]](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Vertices

```csharp
public readonly ImmutableArray<Vector2> Vertices;
```

The ordered list of vertices that define this polygon's shape, in local space (relative to whatever position the polygon will later be evaluated or drawn at).

**Returns** \
[ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### Contains(Vector2, Vector2)

```csharp
public bool Contains(Vector2 point, Vector2 polygonScale)
```

Returns `true` if `point` lies inside this polygon, using a ray-casting (even-odd rule) algorithm. Vertices are first scaled by `polygonScale` before the test, which lets a scaled entity (e.g. flipped or resized in the editor) test hits without having to materialize a new scaled polygon.

**Parameters** \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`polygonScale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(Vector2)

```csharp
public bool Contains(Vector2 vector)
```

Returns `true` if `vector` lies inside this polygon, using a ray-casting (even-odd rule) algorithm.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(Point, Vector2)

```csharp
public bool Contains(Point point, Vector2 polygonScale)
```

Returns `true` if `point` lies inside this polygon, using a ray-casting (even-odd rule) algorithm, with vertices scaled by `polygonScale` before the test.

**Parameters** \
`point` [Point](../../../Murder/Core/Geometry/Point.html) \
`polygonScale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(Point)

```csharp
public bool Contains(Point point)
```

Returns `true` if `point` lies inside this polygon, using a ray-casting (even-odd rule) algorithm.

**Parameters** \
`point` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Intersect(Circle, Vector2)

```csharp
public bool Intersect(Circle circle, Vector2 polygonScale)
```

Checks for a collision between this polygon (scaled by `polygonScale`) and `circle`, by testing every edge against the circle and falling back to a containment check for the case where the circle is fully enclosed.

**Parameters** \
`circle` [Circle](../../../Murder/Core/Geometry/Circle.html) \
`polygonScale` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Intersect(Circle)

```csharp
public bool Intersect(Circle circle)
```

Checks for a collision between this polygon and `circle`.

**Parameters** \
`circle` [Circle](../../../Murder/Core/Geometry/Circle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Intersects(Polygon, Vector2, Vector2)

```csharp
public Vector2? Intersects(Polygon other, Vector2 positionA, Vector2 positionB)
```

Runs a full SAT (Separating Axis Theorem) test between this polygon (at `positionA`) and `other` (at `positionB`). Returns `null` if there is no overlap; otherwise returns the minimum translation vector that would need to be applied to separate the two polygons, which is exactly what a physics/collision resolution system needs to push two overlapping shapes apart.

**Parameters** \
`other` [Polygon](../../../Murder/Core/Geometry/Polygon.html) \
`positionA` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`positionB` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### IsClockwise(IList<Vector2>)

```csharp
public static bool IsClockwise(IList<Vector2> vertices)
```

Returns `true` if `vertices` are wound in clockwise order (using the shoelace formula's signed area). Used by `MergePolygons(Polygon, Polygon)` to normalise the winding order of its result.

**Parameters** \
`vertices` [IList\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IList-1?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsConvex()

```csharp
public bool IsConvex()
```

Returns `true` if this polygon is convex, i.e. every interior angle turns in the same direction. Polygons with fewer than 4 vertices (triangles) are always considered convex.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsPointInTriangle(Vector2, Vector2, Vector2, Vector2)

```csharp
public static bool IsPointInTriangle(Vector2 point, Vector2 a, Vector2 b, Vector2 c)
```

Returns `true` if `point` lies inside the triangle defined by `a`, `b`, `c`, using barycentric coordinates. Used internally by `EarClippingTriangulation(Polygon)` to decide whether a candidate "ear" is valid (i.e. no other vertex sits inside it).

**Parameters** \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`b` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`c` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TryMerge(Polygon, Polygon, float, out Polygon&)

```csharp
public static bool TryMerge(Polygon a, Polygon b, float minDistance, Polygon& result)
```

Attempts to merge two polygons that share at least two vertices within `minDistance` of each other into a single convex polygon made of their combined unique vertices. Returns `false` (with `result` set to `EMPTY`) if they don't share enough vertices, or if the combined shape would not be convex.

**Parameters** \
`a` [Polygon](../../../Murder/Core/Geometry/Polygon.html) \
`b` [Polygon](../../../Murder/Core/Geometry/Polygon.html) \
`minDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`result` [Polygon&](../../../Murder/Core/Geometry/Polygon.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetLines()

```csharp
public Line2[] GetLines()
```

Returns the polygon's edges as an array of `Line2` segments, one per pair of consecutive vertices (wrapping around from the last vertex back to the first). Used by `MergePolygons(Polygon, Polygon)` to reconstitute a merged outline from shared edges.

**Returns** \
[Line2[]](../../../Murder/Core/Geometry/Line2.html) \

#### EarClippingTriangulation(Polygon)

```csharp
public static List<Polygon> EarClippingTriangulation(Polygon polygon)
```

Triangulates `polygon` using the ear-clipping algorithm, merging adjacent triangles back together where possible to reduce the final triangle count. Used to break an arbitrary (possibly concave) polygon into convex pieces for rendering or physics that only understand convex/triangle shapes.

**Parameters** \
`polygon` [Polygon](../../../Murder/Core/Geometry/Polygon.html) \

**Returns** \
[List\<Polygon\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### FindConcaveVertices(ImmutableArray<Vector2>)

```csharp
public static List<int> FindConcaveVertices(ImmutableArray<Vector2> points)
```

Returns the indices of every concave ("reflex") vertex in `points` — vertices where the polygon turns inward rather than outward. Used as a building block for triangulation (`EarClippingTriangulation(Polygon)`) and convex partitioning (`PartitionToConvex(Polygon)`).

**Parameters** \
`points` [ImmutableArray\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

**Returns** \
[List\<int\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### PartitionToConvex(Polygon)

```csharp
public static List<Polygon> PartitionToConvex(Polygon concave)
```

This doesn't work yet — it's an incomplete, simplified attempt at splitting a concave polygon into convex sub-polygons and should not be relied on for correct results.

**Parameters** \
`concave` [Polygon](../../../Murder/Core/Geometry/Polygon.html) \

**Returns** \
[List\<Polygon\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### ReorderVertices(List<Vector2>)

```csharp
public static List<Vector2> ReorderVertices(List<Vector2> vertices)
```

Sorts `vertices` by their angle around the shape's centroid, producing a consistent (counter-clockwise-by-angle) ordering. Useful for turning an unordered bag of points (e.g. picked in the editor without regard for winding) into a valid simple polygon outline.

**Parameters** \
`vertices` [List\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

**Returns** \
[List\<Vector2\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### AddPosition(Vector2)

```csharp
public Polygon AddPosition(Vector2 add)
```

Returns a new polygon with every vertex translated by `add`. This allocates a new vertex array, so avoid calling it every frame in a hot loop.

**Parameters** \
`add` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### AtPosition(Point)

```csharp
public Polygon AtPosition(Point target)
```

Returns this polygon with a new position. The position is calculated using the vertice 0 as origin — i.e. every vertex is shifted by the delta between `target` and the current vertex 0.

**Parameters** \
`target` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### FromRectangle(int, int, int, int)

```csharp
public static Polygon FromRectangle(int x, int y, int width, int height)
```

Creates a rectangular polygon (four corner vertices, clockwise from top-left) matching the given bounds.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### FromRectangle(IntRectangle)

```csharp
public static Polygon FromRectangle(IntRectangle rectangle)
```

Creates a rectangular polygon (four corner vertices, clockwise from top-left) matching `rectangle`.

**Parameters** \
`rectangle` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### RemoveVerticeAt(int)

```csharp
public Polygon RemoveVerticeAt(int index)
```

Returns a new polygon with the vertex at `index` removed.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### WithNewVerticeAt(int, Vector2)

```csharp
public Polygon WithNewVerticeAt(int index, Vector2 target)
```

Returns a new polygon with `target` inserted as a new vertex at `index`, shifting subsequent vertices. Used by the editor when a user adds a vertex to an existing polygon shape.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### WithVerticeAt(int, Vector2)

```csharp
public Polygon WithVerticeAt(int index, Vector2 target)
```

Returns a new polygon with the vertex at `index` replaced by `target`. Used by the editor's polygon-vertex-drag tooling.

**Parameters** \
`index` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \

#### GetBoundingBox()

```csharp
public Rectangle GetBoundingBox()
```

Returns the axis-aligned bounding box that encloses every vertex of this polygon, computing and caching it on first access. Used for cheap broad-phase culling before running the more expensive exact polygon tests.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### MergePolygons(Polygon, Polygon)

```csharp
public static Polygon? MergePolygons(Polygon a, Polygon b)
```

Attempts to merge two polygons that share one or more edges into a single outline polygon, by collecting every unique edge from both and walking them into a connected loop. Returns `EMPTY` if the edges don't form a single closed loop (e.g. the polygons don't actually share a boundary).

**Parameters** \
`a` [Polygon](../../../Murder/Core/Geometry/Polygon.html) \
`b` [Polygon](../../../Murder/Core/Geometry/Polygon.html) \

**Returns** \
[Polygon?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### ProjectOntoAxis(Vector2, Vector2)

```csharp
public ValueTuple<float, float> ProjectOntoAxis(Vector2 axis, Vector2 offset)
```

Projects every vertex (offset by `offset`) onto `axis` and returns the minimum and maximum dot-product values. This is the core building block of SAT (Separating Axis Theorem) overlap testing used by `Intersects(Polygon, Vector2, Vector2)`.

**Parameters** \
`axis` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[ValueTuple\<float, float\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### Draw(Batch2D, Vector2, bool, Color)

```csharp
public void Draw(Batch2D batch, Vector2 position, bool flip, Color color)
```

Draws this polygon's outline as a series of connected line segments, using `batch`. Mostly used by the editor and debug overlays to visualize collision/trigger shapes; when `flip` is set, every vertex is mirrored around the bounding box's centre first (matching how sprites are horizontally flipped).

**Parameters** \
`batch` [Batch2D](../../../Murder/Core/Graphics/Batch2D.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`flip` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`color` [Color](../../../Murder/Core/Graphics/Color.html) \

⚡
