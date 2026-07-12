# LazyShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct LazyShape : IShape
```

An efficient, approximate circular collision shape represented as an elongated octagon.

**Intent:** Provide a fast collision shape for entities where exact circle or box accuracy is not needed.

**Use-case:** Use `LazyShape` in a `ColliderComponent` when performance matters more than shape precision, such as for large numbers of small projectiles or crowds. Its bounding area is slightly wider than tall to account for diagonal movement.

**Implements:** _[IShape](../../../Murder/Core/Geometry/IShape.html)_

### ⭐ Constructors

```csharp
public LazyShape(float radius, Point offset)
```

**Parameters** \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`offset` [Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties

#### Offset

```csharp
public readonly Point Offset;
```

Pixel offset of the shape centre relative to the entity's world position.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Radius

```csharp
public readonly float Radius;
```

The effective radius of the lazy shape in pixels.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SQUARE_ROOT_OF_TWO

```csharp
public static const float SQUARE_ROOT_OF_TWO;
```

Pre-computed value of √2, used when constructing the octagonal polygon approximation.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Methods

#### Rectangle(Vector2)

```csharp
public Rectangle Rectangle(Vector2 addPosition)
```

Returns the bounding rectangle of this shape translated by `addPosition`.

**Parameters** \
`addPosition` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Rectangle()

```csharp
public Rectangle Rectangle()
```

Returns the local-space bounding rectangle of this shape. Equivalent to `GetBoundingBox()`.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### GetPolygon()

```csharp
public virtual PolygonShape GetPolygon()
```

Returns an octagonal polygon approximation of this shape. Result is cached after the first call.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()

```csharp
public virtual Rectangle GetBoundingBox()
```

Returns the axis-aligned bounding rectangle for this lazy shape.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

⚡
