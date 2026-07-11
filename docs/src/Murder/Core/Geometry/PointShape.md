# PointShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct PointShape : IShape
```

An `IShape` implementation that represents a single point as a degenerate collision shape.

**Intent:** Mark a precise world-space point as a collision or trigger location.

**Use-case:** Use `PointShape` in a `ColliderComponent` for pixel-accurate hit detection, such as a cursor, a bullet impact point, or a single-tile trigger.

**Implements:** _[IShape](../../../Murder/Core/Geometry/IShape.html)_

### ⭐ Constructors
```csharp
public PointShape(Point point)
```

**Parameters** \
`point` [Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties
#### Point
```csharp
public readonly Point Point;
```

The single point that defines this shape's position.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
### ⭐ Methods
#### GetPolygon()
```csharp
public virtual PolygonShape GetPolygon()
```

Returns a minimal degenerate triangle polygon centred on this point. Result is cached.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()
```csharp
public virtual Rectangle GetBoundingBox()
```

Returns a 1×1 bounding rectangle at this point's position.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \



⚡