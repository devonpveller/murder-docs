# IntRectangle

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct IntRectangle : IEquatable<T>
```

An integer-precision axis-aligned rectangle (X, Y, Width, Height). The integer counterpart of `Rectangle`.

**Intent:** Store and manipulate tile-aligned or pixel-aligned rectangular regions using integer coordinates, avoiding the rounding artifacts that come from doing repeated float math on pixel-art bounds.

**Use-case:** Use `IntRectangle` when working with grid coordinates, sprite source rectangles, or any region that must stay on integer boundaries. It implicitly converts to/from `Rectangle` and MonoGame's `Microsoft.Xna.Framework.Rectangle`, so it can be passed directly wherever either of those is expected.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public IntRectangle(Point p, int width, int height)
```

Creates a rectangle from an integer top-left point and integer width/height.

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public IntRectangle(Point position, Point size)
```

Creates a rectangle from a top-left position and a size, both given as integer `Point`s.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \

```csharp
public IntRectangle(Point position, Point size, Vector2 anchor)
```

Creates a rectangle of `size` anchored so that a point at the normalised `anchor` (0-1 on each axis) lands on `position`.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \
`anchor` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public IntRectangle(float x, float y, float width, float height)
```

Creates a rectangle from floating-point coordinates, rounding each component to the nearest integer.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`width` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`height` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public IntRectangle(int x, int y, int width, int height)
```

Creates a rectangle at integer `(x, y)` with the given width/height.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Bottom

```csharp
public int Bottom { get; }
```

The Y coordinate of the bottom edge (`Y + Height`).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### BottomCenter

```csharp
public Point BottomCenter { get; }
```

The midpoint of the bottom edge.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### BottomLeft

```csharp
public Point BottomLeft { get; }
```

The bottom-left corner of the rectangle.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### BottomRight

```csharp
public Point BottomRight { get; }
```

The bottom-right corner of the rectangle.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Center

```csharp
public Vector2 Center { get; }
```

The centre of the rectangle as a floating-point vector.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### CenterPoint

```csharp
public Point CenterPoint { get; }
```

The centre of the rectangle rounded to an integer point.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Empty

```csharp
public static IntRectangle Empty { get; }
```

A zero-sized rectangle at the origin. Used as a default/sentinel value, e.g. the result of `Intersection(IntRectangle)` when two rectangles don't overlap.

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### Height

```csharp
public int Height;
```

The height of the rectangle in pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Left

```csharp
public int Left { get; }
```

The X coordinate of the left edge (equal to `X`).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### One

```csharp
public static IntRectangle One { get; }
```

A 1×1 rectangle at the origin.

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### Right

```csharp
public int Right { get; }
```

The X coordinate of the right edge (`X + Width`).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Size

```csharp
public Point Size { get; set; }
```

The width and height as a `Point`. Setting this updates `Width` and `Height` without moving the rectangle's position.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Top

```csharp
public int Top { get; }
```

The Y coordinate of the top edge (equal to `Y`).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### TopCenter

```csharp
public Vector2 TopCenter { get; }
```

The midpoint of the top edge.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### TopLeft

```csharp
public Point TopLeft { get; }
```

The top-left corner of the rectangle.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### TopRight

```csharp
public Point TopRight { get; }
```

The top-right corner of the rectangle.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Width

```csharp
public int Width;
```

The width of the rectangle in pixels.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### X

```csharp
public int X;
```

The X coordinate of the rectangle's top-left corner.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Y

```csharp
public int Y;
```

The Y coordinate of the rectangle's top-left corner.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Methods

#### Contains(Point)

```csharp
public bool Contains(Point point)
```

Returns `true` if `point` lies inside this rectangle (top/left edges inclusive, bottom/right edges exclusive — the usual tile/grid containment convention).

**Parameters** \
`point` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(Rectangle)

```csharp
public bool Contains(Rectangle other)
```

Returns `true` if `other` is fully contained within this rectangle.

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(float, float)

```csharp
public bool Contains(float X, float Y)
```

Returns `true` if the floating-point coordinate `(X, Y)` lies inside this rectangle, after rounding it to the nearest integer.

**Parameters** \
`X` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`Y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(int, int)

```csharp
public bool Contains(int X, int Y)
```

Returns `true` if the integer coordinate `(X, Y)` lies inside this rectangle (top/left edges inclusive, bottom/right edges exclusive).

**Parameters** \
`X` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`Y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Touches(Rectangle)

```csharp
public bool Touches(Rectangle other)
```

Gets whether or not the other [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) intersects with this rectangle (edges touching counts as intersecting).

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### TouchesInside(Rectangle)

```csharp
public bool TouchesInside(Rectangle other)
```

Gets whether or not the other [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) intersects with this rectangle. Just touching the edges is not enough, they need to overlap by a non-zero amount.

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### AddPadding(float, float, float, float)

```csharp
public IntRectangle AddPadding(float left, float top, float right, float bottom)
```

Returns a rectangle expanded outward by an independent amount on each side. Note that despite the declared return type, this internally builds and implicitly converts from a floating-point `Rectangle` since the padding amounts are floats.

**Parameters** \
`left` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`top` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`right` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bottom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### AddPosition(int, int)

```csharp
public IntRectangle AddPosition(int x, int y)
```

Returns a copy of this rectangle moved by `x`/`y`. Size is unchanged.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### AddPosition(Point)

```csharp
public IntRectangle AddPosition(Point position)
```

Returns a new rectangle translated by the given `Point`.

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### AddPosition(Vector2)

```csharp
public IntRectangle AddPosition(Vector2 position)
```

Returns a new rectangle translated by the given `Vector2` (rounded to integers).

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### AtZero()

```csharp
public Rectangle AtZero()
```

Returns a `Rectangle` with the same size as this rectangle but repositioned to the origin `(0, 0)`. Useful when only the dimensions matter and the position should be discarded, such as computing a local-space source rectangle.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### CenterRectangle(Vector2, float, float)

```csharp
public static IntRectangle CenterRectangle(Vector2 center, float width, float height)
```

Creates a `width`×`height` rectangle centred at `center`, rounding the result to integer coordinates.

**Parameters** \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`width` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`height` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### Expand(float)

```csharp
public IntRectangle Expand(float value)
```

Returns a new rectangle expanded symmetrically by `value` on all sides.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### Expand(int)

```csharp
public IntRectangle Expand(int value)
```

Returns a new rectangle expanded symmetrically by `value` pixels on all sides.

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### Expand(int, int)

```csharp
public IntRectangle Expand(int x, int y)
```

Returns a new rectangle expanded by `x` pixels horizontally and `y` pixels vertically on each side.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### FromCoordinates(Point, Point)

```csharp
public static IntRectangle FromCoordinates(Point topLeft, Point bottomRight)
```

Creates a rectangle from explicit top-left and bottom-right corner points.

**Parameters** \
`topLeft` [Point](../../../Murder/Core/Geometry/Point.html) \
`bottomRight` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### FromCoordinates(int, int, int, int)

```csharp
public static IntRectangle FromCoordinates(int top, int bottom, int left, int right)
```

Creates a rectangle from explicit edge coordinates.

**Parameters** \
`top` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`bottom` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`left` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`right` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### FromAbsolute(float, float, float, float)

```csharp
public static IntRectangle FromAbsolute(float left, float top, float right, float bottom)
```

Creates a rectangle from absolute edge coordinates (left, top, right, bottom), rounding to integers.

**Parameters** \
`left` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`top` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`right` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bottom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### Intersection(IntRectangle)

```csharp
public IntRectangle Intersection(IntRectangle other)
```

Returns the overlapping region between this rectangle and `other`, or `Empty` if they do not overlap.

**Parameters** \
`other` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### Union(IntRectangle, IntRectangle)

```csharp
public static IntRectangle Union(IntRectangle startBox, IntRectangle endBox)
```

Creates a new `IntRectangle` that is the union of the two given rectangles. The resulting rectangle will be the smallest rectangle that contains both input rectangles.

**Parameters** \
`startBox` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \
`endBox` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### ClampPosition(IntRectangle)

```csharp
public Point ClampPosition(IntRectangle innerRect)
```

Clamps the position of `innerRect` so that it stays fully within this rectangle's bounds, without changing its size. Useful for keeping a UI window or a camera's view rectangle inside a larger bounding area.

**Parameters** \
`innerRect` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Clamp(Vector2)

```csharp
public Vector2 Clamp(Vector2 point)
```

Clamps `point` so that it lies within this rectangle's bounds. Used to keep a free-moving position (e.g. a dragged cursor or camera target) from leaving a defined area.

**Parameters** \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
