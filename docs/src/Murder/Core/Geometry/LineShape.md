# LineShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct LineShape : IShape
```

An `IShape` implementation that defines a line segment between two integer points, for use as a collision or trigger boundary.

**Intent:** Represent a one-dimensional line-segment collider.

**Use-case:** Add a `LineShape` to a `ColliderComponent` to create wall or boundary segments in a tilemap or level geometry.

**Implements:** _[IShape](../../../Murder/Core/Geometry/IShape.html)_

### ⭐ Constructors

```csharp
public LineShape(Point start, Point end)
```

**Parameters** \
`start` [Point](../../../Murder/Core/Geometry/Point.html) \
`end` [Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties

#### End

```csharp
public readonly Point End;
```

The end point of the line segment.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Line

```csharp
public Line2 Line { get; }
```

Returns a `Line2` built from `Start` and `End`.

**Returns** \
[Line2](../../../Murder/Core/Geometry/Line2.html) \

#### Start

```csharp
public readonly Point Start;
```

The start point of the line segment.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Methods

#### LineAtPosition(Point)

```csharp
public Line2 LineAtPosition(Point position)
```

Returns a `Line2` with both endpoints translated by `position`.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Line2](../../../Murder/Core/Geometry/Line2.html) \

#### GetPolygon()

```csharp
public virtual PolygonShape GetPolygon()
```

Returns a degenerate polygon built from the two endpoints of this line. Result is cached.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()

```csharp
public virtual Rectangle GetBoundingBox()
```

Returns the axis-aligned bounding rectangle enclosing this line segment.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

⚡
