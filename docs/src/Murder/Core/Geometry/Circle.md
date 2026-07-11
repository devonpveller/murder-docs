# Circle

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct Circle
```

A 2D circle defined by a centre position and radius.

**Intent:** Represent a circle for overlap tests, collision queries, and particle emission shapes.

**Use-case:** Use `Circle` directly when you need to test whether a point or another circle overlaps a circular region. Pass a `CircleShape` (which wraps a `Circle`) to a `ColliderComponent` for physics-based collision.

### ⭐ Constructors
```csharp
public Circle(float radius)
```

Creates a circle centred at the origin with the given radius.

**Parameters** \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public Circle(float x, float y, float radius)
```

Creates a circle at position `(x, y)` with the given radius.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Radius
```csharp
public readonly float Radius;
```

The radius of the circle.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### X
```csharp
public readonly float X;
```

Horizontal position of the circle's centre.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Y
```csharp
public readonly float Y;
```

Vertical position of the circle's centre.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
### ⭐ Methods
#### Contains(Point)
```csharp
public bool Contains(Point point)
```

Returns `true` if `point` lies strictly inside this circle.

**Parameters** \
`point` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(Vector2)
```csharp
public bool Contains(Vector2 vector2)
```

Returns `true` if `vector2` lies strictly inside this circle.

**Parameters** \
`vector2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AddPosition(PositionComponent)
```csharp
public Circle AddPosition(PositionComponent position)
```

Returns a new circle translated by the given `PositionComponent`.

**Parameters** \
`position` [PositionComponent](../../../Murder/Components/PositionComponent.html) \

**Returns** \
[Circle](../../../Murder/Core/Geometry/Circle.html) \

#### AddPosition(Point)
```csharp
public Circle AddPosition(Point position)
```

Returns a new circle translated by the given `Point`.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Circle](../../../Murder/Core/Geometry/Circle.html) \

#### AddPosition(Vector2)
```csharp
public Circle AddPosition(Vector2 position)
```

Returns a new circle translated by the given `Vector2`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Circle](../../../Murder/Core/Geometry/Circle.html) \

#### EstipulateSidesFromRadius(float)
```csharp
public int EstipulateSidesFromRadius(float radius)
```

Calculates the recommended polygon vertex count for approximating a circle with the given radius.

**Parameters** \
`radius` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡