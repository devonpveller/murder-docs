# IntRectangle

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct IntRectangle : IEquatable<T>
```

An integer-precision axis-aligned rectangle (X, Y, Width, Height). The integer counterpart of `Rectangle`.

**Intent:** Store and manipulate tile-aligned or pixel-aligned rectangular regions using integer coordinates.

**Use-case:** Use `IntRectangle` when working with grid coordinates, sprite source rectangles, or any region that must stay on integer boundaries. Implicitly converts to/from `Rectangle` and MonoGame's `Rectangle`.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public IntRectangle(Point p, int width, int height)
```

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public IntRectangle(Point position, Point size)
```

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \

```csharp
public IntRectangle(float x, float y, float width, float height)
```

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`width` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`height` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public IntRectangle(int x, int y, int width, int height)
```

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

A zero-sized rectangle at the origin.

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
public Point Size { get; public set; }
```

The width and height as a `Point`. Setting this updates `Width` and `Height`.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Top
```csharp
public int Top { get; }
```

The Y coordinate of the top edge (equal to `Y`).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
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

Returns `true` if `point` is inside this rectangle.

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

Returns `true` if the floating-point coordinate `(X, Y)` is inside this rectangle.

**Parameters** \
`X` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`Y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Contains(int, int)
```csharp
public bool Contains(int X, int Y)
```

Returns `true` if the integer coordinate `(X, Y)` is inside this rectangle.

**Parameters** \
`X` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`Y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Touches(Rectangle)
```csharp
public bool Touches(Rectangle other)
```

Gets whether or not the other [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) intersects with this rectangle.

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
\

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

#### TouchesInside(Rectangle)
```csharp
public bool TouchesInside(Rectangle other)
```

Gets whether or not the other [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) intersects with this rectangle.

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
\

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
\

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

#### CenterRectangle(Vector2, float, float)
```csharp
public IntRectangle CenterRectangle(Vector2 center, float width, float height)
```

Creates a rectangle of `width`×`height` centred at `center`.

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
public IntRectangle FromCoordinates(Point topLeft, Point bottomRight)
```

Creates a rectangle from explicit top-left and bottom-right corner points.

**Parameters** \
`topLeft` [Point](../../../Murder/Core/Geometry/Point.html) \
`bottomRight` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### FromCoordinates(int, int, int, int)
```csharp
public IntRectangle FromCoordinates(int top, int bottom, int left, int right)
```

Creates a rectangle from explicit edge coordinates.

**Parameters** \
`top` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`bottom` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`left` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`right` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

#### ClampPosition(IntRectangle)
```csharp
public Point ClampPosition(IntRectangle innerRect)
```

Clamps `innerRect`'s position so it stays fully within this rectangle.

**Parameters** \
`innerRect` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Clamp(Vector2)
```csharp
public Vector2 Clamp(Vector2 point)
```

Clamps `point` so it lies within this rectangle.

**Parameters** \
`point` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Equals(IntRectangle)
```csharp
public virtual bool Equals(IntRectangle other)
```

**Parameters** \
`other` [IntRectangle](../../../Murder/Core/Geometry/IntRectangle.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Object)
```csharp
public virtual bool Equals(Object obj)
```

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode()
```csharp
public virtual int GetHashCode()
```

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ToString()
```csharp
public virtual string ToString()
```

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \



⚡