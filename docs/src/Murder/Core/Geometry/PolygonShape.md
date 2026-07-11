# PolygonShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct PolygonShape : IShape
```

An `IShape` implementation wrapping a `Polygon` for use in convex polygon collision detection.

**Intent:** Wrap arbitrary polygon vertex data as a collision shape compatible with `ColliderComponent`.

**Use-case:** Use `PolygonShape` when your entity requires a non-rectangular hitbox. Build a `Polygon` from vertices and store it here; call `Cache()` after construction for best performance on repeated bounding-box queries.

**Implements:** _[IShape](../../../Murder/Core/Geometry/IShape.html)_

### ⭐ Constructors
```csharp
public PolygonShape()
```

```csharp
public PolygonShape(Polygon polygon)
```

**Parameters** \
`polygon` [Polygon](../../../Murder/Core/Geometry/Polygon.html) \

### ⭐ Properties
#### Polygon
```csharp
public readonly Polygon Polygon;
```

The underlying polygon data containing the shape's vertices.

**Returns** \
[Polygon](../../../Murder/Core/Geometry/Polygon.html) \
#### Rect
```csharp
public Rectangle Rect { get; }
```

The cached axis-aligned bounding rectangle of the polygon. Calls `Cache()` automatically on first access.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
### ⭐ Methods
#### GetCenter()
```csharp
public Point GetCenter()
```

Returns the integer centre point of the polygon's bounding rectangle.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### GetPolygon()
```csharp
public virtual PolygonShape GetPolygon()
```

Returns `this` — the shape is already a polygon.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()
```csharp
public virtual Rectangle GetBoundingBox()
```

Returns the cached bounding rectangle of this polygon shape.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Cache()
```csharp
public void Cache()
```

Pre-computes and caches the indices of the leftmost, rightmost, topmost, and bottommost vertices for fast bounding-box access.



⚡