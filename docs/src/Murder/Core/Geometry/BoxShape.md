# BoxShape

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct BoxShape : IShape
```

An axis-aligned rectangular collision shape defined by a width, height, pivot origin, and pixel offset.

**Intent:** Represent a box-shaped collider for use in a `ColliderComponent`. This is the most common and cheapest `IShape` implementation, since its bounding box computation is trivial and its polygon form is just its four corners.

**Use-case:** Attach a `BoxShape` to an entity's `ColliderComponent` when you need a simple rectangular hitbox. Use `Origin` to control the pivot point (e.g., `Vector2.Zero` for top-left, `new Vector2(0.5f, 0.5f)` for center) and `Offset` to shift the box relative to the entity's position. Use `ResizeTopLeft`/`ResizeBottomRight` when interactively resizing a box from one corner (e.g. in the editor) while keeping the opposite corner fixed.

**Implements:** _[IShape](../../../Murder/Core/Geometry/IShape.html)_

### ⭐ Constructors

```csharp
public BoxShape()
```

Creates a default 16×16 box shape with zero origin and offset.

```csharp
public BoxShape(Rectangle rectangle)
```

Creates a box shape from an existing rectangle, using its top-left corner as the offset and its size as width/height (origin is zero).

**Parameters** \
`rectangle` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

```csharp
public BoxShape(Vector2 origin, Point offset, int width, int height)
```

Creates a box shape with explicit origin, offset, and dimensions.

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

The height of the box, in pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Offset

```csharp
public Point Offset { get; init; }
```

A pixel offset applied to the box position, on top of the pivot adjustment from `Origin`.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Origin

```csharp
public readonly Vector2 Origin;
```

The pivot point of the box as a normalised (0-1) vector, e.g. `(0, 0)` for top-left or `(0.5, 0.5)` for centre. Controls which point of the box lands on the entity's position.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Rectangle

```csharp
public Rectangle Rectangle { get; }
```

The box's local-space rectangle, accounting for `Origin` and `Offset`.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Size

```csharp
public Point Size { get; }
```

The width and height of the box as a `Point`.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Width

```csharp
public readonly int Width;
```

The width of the box, in pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### ResizeBottomRight(Vector2)

```csharp
public BoxShape ResizeBottomRight(Vector2 newBottomRight)
```

Returns a new `BoxShape` with its bottom-right corner moved to `newBottomRight`, adjusting width and height while keeping the top-left corner fixed. Used by the editor's box-resize gizmo when dragging the bottom-right handle.

**Parameters** \
`newBottomRight` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[BoxShape](../../../Murder/Core/Geometry/BoxShape.html) \

#### ResizeTopLeft(Vector2)

```csharp
public BoxShape ResizeTopLeft(Vector2 newTopLeft)
```

Returns a new `BoxShape` with its top-left corner moved to `newTopLeft`, adjusting the offset and dimensions so the bottom-right corner stays fixed. Used by the editor's box-resize gizmo when dragging the top-left handle.

**Parameters** \
`newTopLeft` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[BoxShape](../../../Murder/Core/Geometry/BoxShape.html) \

#### GetPolygon()

```csharp
public PolygonShape GetPolygon()
```

Converts this box to a `PolygonShape` with four corner vertices. Result is cached after the first call.

**Returns** \
[PolygonShape](../../../Murder/Core/Geometry/PolygonShape.html) \

#### GetBoundingBox()

```csharp
public Rectangle GetBoundingBox()
```

Returns the axis-aligned bounding rectangle of this box shape.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

⚡
