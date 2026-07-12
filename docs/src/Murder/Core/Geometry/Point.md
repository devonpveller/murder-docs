# Point

**Namespace:** Murder.Core.Geometry \
**Assembly:** Murder.dll

```csharp
public sealed struct Point : IEquatable<T>
```

Represents a single point with coordinates [Point.Y](../../../Murder/Core/Geometry/Point.html#y).
Points are also often used to store sizes, with X marking the right of an object and Y marking its bottom.

**Intent:** Murder's integer 2D point type, serving as the primary coordinate type for grid and tile operations.

**Use-case:** Use for tile positions, grid indices, and any integer-coordinate math; arithmetic operators and conversion helpers to `Vector2` are provided.

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

### ⭐ Constructors

```csharp
public Point(float x, float y)
```

Creates a point by rounding the x and y parameters.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public Point(int v)
```

Creates a point where both x and y and equal to v.

**Parameters** \
`v` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public Point(int x, int y)
```

Creates a point.

**Parameters** \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Down

```csharp
public static Point Down { get; }
```

Point with coordinates X = 0 and Y = 1.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Flipped

```csharp
public static Point Flipped { get; }
```

Point with coordinates X = -1 and Y = 1 (multiply your point by this and you get its mirror).

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### HalfCell

```csharp
public static Point HalfCell { get; }
```

Represents half a cell on the current [Grid](../../../Murder/Core/Grid.html).

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### One

```csharp
public static Point One { get; }
```

Point with coordinates X = 1 and Y = 1.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### X

```csharp
public int X;
```

The value of X in this point.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### XY

```csharp
public ValueTuple<T1, T2> XY { get; }
```

Destructuring helper for obtaining a tuple from this point.

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### Y

```csharp
public int Y;
```

The value of Y in this point.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Zero

```csharp
public static Point Zero { get; }
```

Point with coordinates X = 0 and Y = 0.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Methods

#### Length()

```csharp
public float Length()
```

Calculates the length of this point.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

#### LengthSquared()

```csharp
public int LengthSquared()
```

Returns the length of this point, squared (IOW: X _ X + Y _ Y).

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### Max(Point)

```csharp
public Point Max(Point other)
```

**Parameters** \
`other` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Min(Point)

```csharp
public Point Min(Point other)
```

**Parameters** \
`other` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Mirror(Point)

```csharp
public Point Mirror(Point center)
```

Returns the mirror of this point across the X axis relative to the center point <paramref name="center" />

**Parameters** \
`center` [Point](../../../Murder/Core/Geometry/Point.html) \
\

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Scale(Point)

```csharp
public Point Scale(Point other)
```

Equivalent to this \* other.

**Parameters** \
`other` [Point](../../../Murder/Core/Geometry/Point.html) \
\

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### ToWorldPosition()

```csharp
public Point ToWorldPosition()
```

Converts this point into a world position by multiplying it by the cell size.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### BreakInTwo()

```csharp
public ValueTuple<T1, T2> BreakInTwo()
```

Deconstruction helper for obtaining a tuple from this point.

**Returns** \
[ValueTuple\<T1, T2\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### ToVector2()

```csharp
public Vector2 ToVector2()
```

Converts this point into a [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) with the same X and Y values.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToXnaVector2()

```csharp
public Vector2 ToXnaVector2()
```

Converts this point into a MonoGame [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) with the same X and Y values.

**Returns** \
[Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### ToVector3()

```csharp
public Vector3 ToVector3()
```

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

#### Clamp(int, int, int, int)

```csharp
public Point Clamp(int minX, int minY, int maxX, int maxY)
```

Calculates a new point based on this point that is within the specified constraints.

**Parameters** \
`minX` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`minY` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`maxX` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`maxY` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Clamp(Point, Point)

```csharp
public Point Clamp(Point min, Point max)
```

Restricts the current point's coordinates to be within the specified minimum and maximum bounds.

**Parameters** \
`min` [Point](../../../Murder/Core/Geometry/Point.html) \
`max` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Half()

```csharp
public Point Half()
```

Returns a new point with both `X` and `Y` divided by two (rounded to the nearest integer). Handy for quickly finding the midpoint of a size, e.g. half of a sprite's dimensions to get its centre offset.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Lerp(Point, Point, float)

```csharp
public static Point Lerp(Point point1, Point point2, float endFraction)
```

Linearly interpolates between `point1` and `point2` by `endFraction` (0 = `point1`, 1 = `point2`), rounding the result to integer coordinates.

**Parameters** \
`point1` [Point](../../../Murder/Core/Geometry/Point.html) \
`point2` [Point](../../../Murder/Core/Geometry/Point.html) \
`endFraction` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Lerp(Vector2, Vector2, float)

```csharp
public static Point Lerp(Vector2 point1, Vector2 point2, float endFraction)
```

Linearly interpolates between `point1` and `point2` by `endFraction`, rounding the result to integer coordinates.

**Parameters** \
`point1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`point2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`endFraction` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### Equals(Point)

```csharp
public virtual bool Equals(Point other)
```

Compares whether the point <paramref name="other" /> has the same X and Y value as this point.

**Parameters** \
`other` [Point](../../../Murder/Core/Geometry/Point.html) \

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

#### Deconstruct(out Int32&, out Int32&)

```csharp
public void Deconstruct(Int32& x, Int32& y)
```

**Parameters** \
`x` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int&](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
