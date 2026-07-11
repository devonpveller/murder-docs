# Rectangle

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct Rectangle : IEquatable<T>
```

A floating-point axis-aligned rectangle (X, Y, Width, Height). The primary rectangle type in Murder.

**Intent:** Store and manipulate rectangular regions with sub-pixel precision for rendering, collision, and layout.

**Use-case:** Use `Rectangle` for world-space bounds, camera viewports, sprite source rectangles, and overlap tests. Convert to `IntRectangle` when integer coordinates are required.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors
```csharp
public Rectangle(Point p, int width, int height)
```

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public Rectangle(Point position, Point size)
```

**Parameters** \
`position` [Point](../../../Murder/Core/Geometry/Point.html) \
`size` [Point](../../../Murder/Core/Geometry/Point.html) \

```csharp
public Rectangle(float x, float y, float width, float height)
```

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`width` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`height` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public Rectangle(int x, int y, int width, int height)
```

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public Rectangle(Vector2 position, Vector2 size)
```

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties
#### Bottom
```csharp
public float Bottom { get; public set; }
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### BottomCenter
```csharp
public Vector2 BottomCenter { get; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### BottomLeft
```csharp
public Vector2 BottomLeft { get; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### BottomRight
```csharp
public Vector2 BottomRight { get; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Center
```csharp
public Vector2 Center { get; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### CenterLeft
```csharp
public Vector2 CenterLeft { get; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### CenterPoint
```csharp
public Point CenterPoint { get; }
```

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Empty
```csharp
public static Rectangle Empty { get; }
```

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### Height
```csharp
public float Height;
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### HeightRound
```csharp
public int HeightRound { get; }
```

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### IsEmpty
```csharp
public bool IsEmpty { get; }
```

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
#### Left
```csharp
public float Left { get; public set; }
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### One
```csharp
public static Rectangle One { get; }
```

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
#### Right
```csharp
public float Right { get; public set; }
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Size
```csharp
public Vector2 Size { get; public set; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Top
```csharp
public float Top { get; public set; }
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### TopCenter
```csharp
public Vector2 TopCenter { get; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### TopLeft
```csharp
public Vector2 TopLeft { get; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### TopRight
```csharp
public Vector2 TopRight { get; }
```

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Width
```csharp
public float Width;
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### WidthRound
```csharp
public int WidthRound { get; }
```

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### X
```csharp
public float X;
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### XRound
```csharp
public int XRound { get; }
```

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Y
```csharp
public float Y;
```

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### YRound
```csharp
public int YRound { get; }
```

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

#### Contains(Vector2)
```csharp
public bool Contains(Vector2 vector)
```

Returns `true` if `vector` lies inside this rectangle.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

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

#### TouchesWithMaxRotationCheck(Vector2, Vector2, Vector2)
```csharp
public bool TouchesWithMaxRotationCheck(Vector2 position, Vector2 size, Vector2 offset)
```

Whether an object within bounds intersects with this rectangle.
            This takes into account the "maximum" height and length given any rotation.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`size` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### SubtractRectangles(Rectangle, Rectangle)
```csharp
public IEnumerable<T> SubtractRectangles(Rectangle main, Rectangle subtract)
```

Returns up to four sub-rectangles that represent `main` minus the area covered by `subtract`.

**Parameters** \
`main` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`subtract` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### AddPadding(float, float, float, float)
```csharp
public Rectangle AddPadding(float left, float top, float right, float bottom)
```

Returns a new rectangle expanded outward by the specified padding amounts on each side.

**Parameters** \
`left` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`top` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`right` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bottom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

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

Returns a new rectangle translated by the given `Vector2`.

**Parameters** \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### CenterRectangle(Point, int, int)
```csharp
public Rectangle CenterRectangle(Point center, int width, int height)
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

Returns this rectangle moved so its centre is at `(x, y)`.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### CenterRectangle(Vector2, float, float)
```csharp
public Rectangle CenterRectangle(Vector2 center, float width, float height)
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

Returns a new rectangle expanded symmetrically by `value` on all sides.

**Parameters** \
`value` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Expand(int)
```csharp
public Rectangle Expand(int value)
```

Returns a new rectangle expanded symmetrically by `value` pixels on all sides.

**Parameters** \
`value` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### FromCoordinates(float, float, float, float)
```csharp
public Rectangle FromCoordinates(float top, float bottom, float left, float right)
```

Constructor for a rectangle from a set of coordinates.

**Parameters** \
`top` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`bottom` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`left` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`right` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### FromCoordinates(Vector2, Vector2)
```csharp
public Rectangle FromCoordinates(Vector2 topLeft, Vector2 bottomRight)
```

Constructor for a rectangle from a set of coordinates.

**Parameters** \
`topLeft` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`bottomRight` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Intersection(Rectangle, Rectangle)
```csharp
public Rectangle Intersection(Rectangle a, Rectangle b)
```

Returns the overlapping region of two rectangles, or an empty rectangle if they do not intersect.

**Parameters** \
`a` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`b` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

#### Lerp(Rectangle, Rectangle, float)
```csharp
public Rectangle Lerp(Rectangle a, Rectangle b, float v)
```

Linearly interpolates between rectangles `a` and `b` by factor `v`.

**Parameters** \
`a` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`b` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`v` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

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

#### Equals(Rectangle)
```csharp
public virtual bool Equals(Rectangle other)
```

**Parameters** \
`other` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

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



⚡