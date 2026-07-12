# Rectangle

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct Rectangle : IEquatable<T>
```

A floating-point axis-aligned rectangle (X, Y, Width, Height). The primary rectangle type in Murder.

**Intent:** Store and manipulate rectangular regions with sub-pixel precision for rendering, collision, and layout.

**Use-case:** Use `Rectangle` for world-space bounds, camera viewports, sprite source rectangles, and overlap tests. It implicitly converts to/from `IntRectangle` and MonoGame's `Microsoft.Xna.Framework.Rectangle`, so it can usually be passed directly wherever either of those is expected.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public Rectangle(Point p, int width, int height)
```

Creates a rectangle from an integer top-left point and float width/height.

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public Rectangle(Point position, Point size)
```

Creates a rectangle from a top-left position and a size, both given as integer `Point`s.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \

```csharp
public Rectangle(float x, float y, float width, float height)
```

Creates a rectangle at `(x, y)` with the given width/height.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`width` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`height` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public Rectangle(int x, int y, int width, int height)
```

Creates a rectangle at integer `(x, y)` with the given width/height.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public Rectangle(Vector2 position, Vector2 size)
```

Creates a rectangle from a top-left `position` and a `size`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public Rectangle(Vector2 position, Vector2 size, Vector2 origin)
```

Creates a rectangle of `size` anchored so that a point at the normalised `origin` (0-1 on each axis, e.g. `(0.5, 0.5)` for centre) lands on `position`. This mirrors how sprites are positioned relative to their pivot.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### Bottom

```csharp
public float Bottom { get; set; }
```

The Y coordinate of the bottom edge (`Y + Height`). Setting it recomputes `Height` so the top edge stays fixed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### BottomCenter

```csharp
public Vector2 BottomCenter { get; }
```

The midpoint of the bottom edge.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### BottomLeft

```csharp
public Vector2 BottomLeft { get; }
```

The bottom-left corner of the rectangle.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### BottomRight

```csharp
public Vector2 BottomRight { get; }
```

The bottom-right corner of the rectangle.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Center

```csharp
public Vector2 Center { get; }
```

The centre of the rectangle as a floating-point vector.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### CenterLeft

```csharp
public Vector2 CenterLeft { get; }
```

The midpoint of the left edge.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### CenterPoint

```csharp
public Point CenterPoint { get; }
```

The centre of the rectangle rounded to an integer `Point`. Prefer this over `Center` when the result is going to be used as a tile/grid coordinate.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### CenterRight

```csharp
public Vector2 CenterRight { get; }
```

The midpoint of the right edge.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Empty

```csharp
public static Rectangle Empty { get; }
```

A rectangle with all fields set to zero. Used as a default/sentinel value, e.g. by `Polygon`'s bounding-box cache to detect "not yet computed".

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Height

```csharp
public float Height;
```

The height of the rectangle, in world/pixel units.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### HeightRound

```csharp
public int HeightRound { get; }
```

`Height` rounded to the nearest integer.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### IsEmpty

```csharp
public bool IsEmpty { get; }
```

Whether this rectangle is exactly the zero rectangle (position and size both zero). This is a stricter check than "has no area" — a rectangle at a non-zero position with zero width/height still returns `false`.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Left

```csharp
public float Left { get; set; }
```

The X coordinate of the left edge. Getting returns `X`; setting mutates `X` directly without adjusting `Width`, so use it with care if you want to preserve the right edge — prefer reconstructing the rectangle for that.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### One

```csharp
public static Rectangle One { get; }
```

A 1×1 rectangle at the origin. Useful as a minimal non-empty placeholder.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Right

```csharp
public float Right { get; set; }
```

The X coordinate of the right edge (`X + Width`). Setting it recomputes `Width` so the left edge stays fixed.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Size

```csharp
public Vector2 Size { get; set; }
```

The width/height of the rectangle as a `Vector2`. Setting this updates `Width` and `Height` without moving the rectangle's position.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Top

```csharp
public float Top { get; set; }
```

The Y coordinate of the top edge. Equivalent to `Y`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### TopCenter

```csharp
public Vector2 TopCenter { get; }
```

The midpoint of the top edge.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### TopLeft

```csharp
public Vector2 TopLeft { get; }
```

The top-left corner of the rectangle, i.e. `(X, Y)`.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### TopRight

```csharp
public Vector2 TopRight { get; }
```

The top-right corner of the rectangle.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Width

```csharp
public float Width;
```

The width of the rectangle, in world/pixel units.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### WidthRound

```csharp
public int WidthRound { get; }
```

`Width` rounded to the nearest integer.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### X

```csharp
public float X;
```

The X coordinate of the rectangle's top-left corner.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### XRound

```csharp
public int XRound { get; }
```

`X` rounded to the nearest integer.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Y

```csharp
public float Y;
```

The Y coordinate of the rectangle's top-left corner.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### YRound

```csharp
public int YRound { get; }
```

`Y` rounded to the nearest integer.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### Contains(Point)

```csharp
public bool Contains(Point point)
```

Returns `true` if `point` lies strictly inside this rectangle (edges excluded).

**Parameters** \
`point` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(float, float)

```csharp
public bool Contains(float X, float Y)
```

Returns `true` if the floating-point coordinate `(X, Y)` lies strictly inside this rectangle.

**Parameters** \
`X` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`Y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(int, int)

```csharp
public bool Contains(int X, int Y)
```

Returns `true` if the integer coordinate `(X, Y)` lies strictly inside this rectangle.

**Parameters** \
`X` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`Y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(Vector2)

```csharp
public bool Contains(Vector2 vector)
```

Returns `true` if `vector` lies strictly inside this rectangle.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Touches(Rectangle)

```csharp
public bool Touches(Rectangle other)
```

Gets whether or not the other [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) intersects with this rectangle (edges touching counts as intersecting). This is the standard AABB overlap test used throughout collision and culling code.

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TouchesInside(Rectangle)

```csharp
public bool TouchesInside(Rectangle other)
```

Gets whether or not the other [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) intersects with this rectangle. Just touching the edges is not enough — they need to overlap by a non-zero amount.

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsInside(Rectangle)

```csharp
public bool IsInside(Rectangle other)
```

Checks if this rectangle is completely contained within `other`, i.e. all four of this rectangle's edges lie within `other`'s bounds.

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TouchesWithMaxRotationCheck(Vector2, Vector2, Vector2)

```csharp
public bool TouchesWithMaxRotationCheck(Vector2 position, Vector2 size, Vector2 offset)
```

Whether an object within bounds intersects with this rectangle. This takes into account the "maximum" height and length given any rotation, by inflating the tested area to the largest square that could contain the rotated object at any angle. Useful for a cheap, rotation-safe broad-phase check before a more precise (and expensive) rotated-shape test.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AddPadding(float, float, float, float)

```csharp
public Rectangle AddPadding(float left, float top, float right, float bottom)
```

Returns a new rectangle expanded outward by an independent amount on each side. Unlike `Expand(float)`, each edge can grow (or, with a negative value, shrink) by a different amount — useful for asymmetric UI insets. See also `Padding` for a reusable value type covering the same use case.

**Parameters** \
`left` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`top` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`right` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bottom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### AddPosition(float, float)

```csharp
public Rectangle AddPosition(float x, float y)
```

Returns a copy of this rectangle moved by `x`/`y`, rounded to the nearest integer. Size is unchanged.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### AddPosition(Point)

```csharp
public Rectangle AddPosition(Point position)
```

Returns a new rectangle translated by the given `Point`.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### AddPosition(Vector2)

```csharp
public Rectangle AddPosition(Vector2 position)
```

Returns a new rectangle translated by the given `Vector2`, rounded to the nearest integer.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### AtPosition(Vector2)

```csharp
public Rectangle AtPosition(Vector2 position)
```

Returns a copy of this rectangle with its top-left corner set to `position`. Unlike `AddPosition(Vector2)` this is an absolute move rather than a relative one, and the value is not rounded. `SetPosition(Vector2)` is an identical alias for this method.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### SetPosition(Vector2)

```csharp
public Rectangle SetPosition(Vector2 position)
```

Returns a new rectangle with `X` and `Y` set to `position`, preserving size.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### CenterRectangle(Point, int, int)

```csharp
public static Rectangle CenterRectangle(Point center, int width, int height)
```

Creates a `width`×`height` rectangle centred at `center`.

**Parameters** \
`center` [Point](../../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### CenterRectangle(float, float)

```csharp
public Rectangle CenterRectangle(float x, float y)
```

Returns a new `x`×`y` rectangle centred on this rectangle's centre.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### CenterRectangle(Vector2, float, float)

```csharp
public static Rectangle CenterRectangle(Vector2 center, float width, float height)
```

Creates a `width`×`height` rectangle centred at `center`.

**Parameters** \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`width` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`height` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### CenterRectangle(Vector2)

```csharp
public Rectangle CenterRectangle(Vector2 size)
```

Returns a rectangle of the given `size` centred at this rectangle's centre point.

**Parameters** \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Expand(float)

```csharp
public Rectangle Expand(float value)
```

Returns a new rectangle expanded symmetrically by `value` on all sides, keeping the same centre.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Expand(int)

```csharp
public Rectangle Expand(int value)
```

Returns a new rectangle expanded symmetrically by `value` pixels on all sides, keeping the same centre.

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### FromCoordinates(float, float, float, float)

```csharp
public static Rectangle FromCoordinates(float top, float bottom, float left, float right)
```

Constructor for a rectangle from a set of edge coordinates, rather than position and size.

**Parameters** \
`top` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bottom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`left` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`right` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### FromCoordinates(Vector2, Vector2)

```csharp
public static Rectangle FromCoordinates(Vector2 topLeft, Vector2 bottomRight)
```

Constructor for a rectangle from its top-left and bottom-right corners.

**Parameters** \
`topLeft` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`bottomRight` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### GetRotatedBounds(float, Vector2)

```csharp
public Rectangle GetRotatedBounds(float angle, Vector2 origin)
```

Locally rotates this rectangle by `angle` (in radians) around `origin` and returns the smallest rectangle that fully contains the rotated result. Used by the editor's selection/gizmo systems to compute an accurate AABB for a rotated sprite.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Intersection(Rectangle, Rectangle)

```csharp
public static Rectangle Intersection(Rectangle a, Rectangle b)
```

Returns the overlapping region of two rectangles. If the two rectangles do not overlap, the result will have a negative width and/or height — callers that only need a yes/no answer should use `Touches(Rectangle)` instead.

**Parameters** \
`a` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`b` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Lerp(Rectangle, Rectangle, float)

```csharp
public static Rectangle Lerp(Rectangle a, Rectangle b, float v)
```

Linearly interpolates the position and size between rectangles `a` and `b` by factor `v` (0 = `a`, 1 = `b`). Commonly used to animate a bounding box or camera viewport smoothly between two states.

**Parameters** \
`a` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`b` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### TrimTop(float)

```csharp
public Rectangle TrimTop(float down)
```

Returns a copy of this rectangle with its top edge pushed down by `down` pixels, shrinking the height by the same amount while keeping the bottom edge fixed. Useful for peeling off a header/margin strip from the top of a UI panel rectangle.

**Parameters** \
`down` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Equals(Rectangle)

```csharp
public bool Equals(Rectangle other)
```

Compares whether `other` has the same position and size as this rectangle.

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)

```csharp
public override bool Equals(Object obj)
```

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode()

```csharp
public override int GetHashCode()
```

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
