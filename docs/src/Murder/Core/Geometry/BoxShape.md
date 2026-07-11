# BoxShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct BoxShape : IShape
```

An axis-aligned rectangular collision shape defined by a width, height, pivot origin, and optional offset.

**Intent:** Represent a box-shaped collider for use in a `ColliderComponent`.

**Use-case:** Attach a `BoxShape` to an entity's `ColliderComponent` when you need a simple rectangular hitbox. Use `Origin` to control the pivot point (e.g., `Vector2.Zero` for top-left, `new Vector2(0.5f, 0.5f)` for center) and `Offset` to shift the box relative to the entity's position.

**Implements:** _[IShape](../../../Murder/Core/Geometry/IShape.html)_

### ⭐ Constructors
```csharp
public BoxShape()
```

Creates a default 16×16 box shape with zero origin and offset.

```csharp
public BoxShape(Rectangle rectangle)
```

Creates a box shape from an existing rectangle, using its top-left corner as the offset and its size as width/height.

**Parameters** \
`rectangle` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

```csharp
public BoxShape(Vector2 origin, Point offset, int width, int height)
```

**Parameters** \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`offset` [Point](../../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Height
```csharp
public readonly int Height;
```

Height of the box in pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Offset
```csharp
public readonly Point Offset;
```

Pixel offset applied to the box position relative to the entity's world position.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Origin
```csharp
public readonly Vector2 Origin;
```

Pivot point of the box as a normalised (0–1) vector. `(0,0)` is top-left; `(0.5,0.5)` is centre.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Rectangle
```csharp
public Rectangle Rectangle { get; }
```

Simple shape getter

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### Size
```csharp
public Point Size { get; }
```

Returns the width and height as a `Point`.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Width
```csharp
public readonly int Width;
```

Width of the box in pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### ResizeBottomRight(Vector2)
```csharp
public BoxShape ResizeBottomRight(Vector2 newBottomRight)
```

Returns a new `BoxShape` with its bottom-right corner moved to `newBottomRight`, adjusting width and height accordingly.

**Parameters** \
`newBottomRight` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[BoxShape](../../../Murder/Core/Geometry/BoxShape.html) \

#### ResizeTopLeft(Vector2)
```csharp
public BoxShape ResizeTopLeft(Vector2 newTopLeft)
```

Returns a new `BoxShape` with its top-left corner moved to `newTopLeft`, adjusting the offset and dimensions.

**Parameters** \
`newTopLeft` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[BoxShape](../../../Murder/Core/Geometry/BoxShape.html) \

#### GetPolygon()
```csharp
public virtual PolygonShape GetPolygon()
```

Converts this box to a `PolygonShape` with four corner vertices. Result is cached after the first call.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()
```csharp
public virtual Rectangle GetBoundingBox()
```

Returns the axis-aligned bounding rectangle of this box shape.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \



⚡