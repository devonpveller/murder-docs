# CircleShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct CircleShape : IShape
```

An `IShape` implementation that wraps a `Circle` for use as a circular collision shape in a `ColliderComponent`.

**Intent:** Provide a circle-shaped collider attachable to an entity's collision component.

**Use-case:** Add a `CircleShape` to a `ColliderComponent` when an entity needs a round hitbox. Set `Radius` to the desired collision radius and `Offset` to shift the circle relative to the entity's origin.

**Implements:** _[IShape](../../../Murder/Core/Geometry/IShape.html)_

### ⭐ Constructors

```csharp
public CircleShape(float radius, Point offset)
```

**Parameters** \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`offset` [Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties

#### Circle

```csharp
public Circle Circle { get; }
```

Returns a `Circle` at this shape's offset position with the configured radius.

**Returns** \
[Circle](../../../Murder/Core/Geometry/Circle.html) \

#### Offset

```csharp
public readonly Point Offset;
```

Pixel offset of the circle centre relative to the entity's world position.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Radius

```csharp
public readonly float Radius;
```

Radius of the circle in pixels.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### GetPolygon()

```csharp
public PolygonShape GetPolygon()
```

Approximates this circle as a 12-sided polygon. Note that, unlike other `IShape` implementations, this always builds a fresh `PolygonShape` on every call rather than returning the cached instance — despite the presence of an internal cache field, callers should not assume the returned instance is reused across calls.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()

```csharp
public Rectangle GetBoundingBox()
```

Returns the axis-aligned bounding rectangle that fully encloses this circle.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

⚡
