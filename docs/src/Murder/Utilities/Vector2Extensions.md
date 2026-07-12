# Vector2Extensions

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class Vector2Extensions
```

Extension methods on `System.Numerics.Vector2` covering the game-specific operations that come up constantly in physics, animation and rendering code: angle/heading math, grid conversion, perpendicular/rotation helpers, and treating a vector as a "size" (`Width`/`Height`) rather than a position.

**Intent:** Complements the constants and less-common math in [Vector2Helper](../../Murder/Utilities/Vector2Helper.html).

**Use-case:** Use `Angle` to get a heading, `Manhattan` for grid distance checks, `Rotate`/`SnapAngle` for orientation math, `Perpendicular`/`PerpendicularClockwise`/`PerpendicularCounterClockwise` for collision/steering math, and `Width`/`Height` to treat a vector as a size.

### ⭐ Methods

#### HasValue(Vector2)

```csharp
public bool HasValue(Vector2 vector)
```

Returns `true` if the vector is not exactly (0, 0). Useful for checking whether an optional direction/offset field was actually set.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### IsSameCell(Vector2, Vector2)

```csharp
public bool IsSameCell(Vector2 this, Vector2 other)
```

Returns `true` if both world-space vectors fall in the same tile-grid cell.

**Parameters** \
`this` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`other` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Angle(Vector2)

```csharp
public float Angle(Vector2 vector)
```

Returns the angle of the vector in radians, measured from the positive X axis.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Height(Vector2)

```csharp
public float Height(Vector2 vector)
```

A quick shorthand for when using a vector as a "size"

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Manhattan(Vector2)

```csharp
public float Manhattan(Vector2 vector)
```

Returns the Manhattan (L1/taxicab) distance of the vector from the origin: |X| + |Y|. Cheaper than Euclidean length; useful for grid-based distance heuristics.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### PerpendicularCounterClockwise(Vector2, Vector2)

```csharp
public float PerpendicularCounterClockwise(Vector2 vector, Vector2 other)
```

Despite the name (a leftover from copy/pasting the unary `PerpendicularCounterClockwise(Vector2)`'s signature), this does **not** compute a perpendicular or cross product. It returns the same normalized directional-deviation measure as `Vector2Helper.Deviation(Vector2, Vector2)`: a value in `[0, 1]` where 0 means the two vectors point in the same direction and 1 means they point in exactly opposite directions. Prefer calling `Vector2Helper.Deviation` directly for clarity; this overload exists for source compatibility.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`other` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Width(Vector2)

```csharp
public float Width(Vector2 vector)
```

A quick shorthand for when using a vector as a "size"

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Ceiling(Vector2)

```csharp
public Point Ceiling(Vector2 vector)
```

Rounds each component up (towards positive infinity) to an integer `Point`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Floor(Vector2)

```csharp
public Point Floor(Vector2 vector)
```

Rounds each component down (towards negative infinity) to an integer `Point`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Point(Vector2)

```csharp
public Point Point(Vector2 vector)
```

Converts the vector to an integer `Point` by rounding each component to the nearest integer.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Round(Vector2)

```csharp
public Point Round(Vector2 vector)
```

Rounds each component to the nearest integer `Point`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToGridPoint(Vector2)

```csharp
public Point ToGridPoint(Vector2 vector)
```

Converts a world-space vector to the tile-grid cell coordinate it falls in.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### XY(Vector2)

```csharp
public ValueTuple<float, float> XY(Vector2 vector)
```

Deconstructs the vector into a plain tuple of its components, for pattern matching or tuple-based APIs.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[ValueTuple\<float, float\>](https://learn.microsoft.com/en-us/dotnet/api/System.ValueTuple-2?view=net-7.0) \

#### Abs(Vector2)

```csharp
public Vector2 Abs(Vector2 vector)
```

Returns a vector with the absolute value of each component.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Add(Vector2, float)

```csharp
public Vector2 Add(Vector2 a, float b)
```

Adds the scalar `b` to both components of `a`.

**Parameters** \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`b` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Approach(Vector2, Vector2, float)

```csharp
public Vector2 Approach(Vector2 a, Vector2 b, float amount)
```

Moves each component of `a` towards the matching component of `b` by up to `amount`, component-wise, via `Calculator.Approach`. Note the Y component approaches from `b` towards `a` (reversed argument order versus X) — this is how the source implements it; verify it matches your intent before relying on symmetric X/Y behavior.

**Parameters** \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`b` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ClampLength(Vector2, float)

```csharp
public Vector2 ClampLength(Vector2 vector, float length)
```

Returns the vector unchanged if its length is at most `length`, otherwise scales it down to exactly that length while preserving direction.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`length` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Mirror(Vector2, Vector2)

```csharp
public Vector2 Mirror(Vector2 vector, Vector2 center)
```

Reflects the vector horizontally around `center`'s X coordinate, leaving Y unchanged. Useful for flipping a position when an entity's sprite is horizontally mirrored.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`center` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Multiply(Vector2, Vector2)

```csharp
public Vector2 Multiply(Vector2 a, Vector2 b)
```

Component-wise multiplies a `System.Numerics.Vector2` by an XNA `Vector2`, returning a `System.Numerics.Vector2`.

**Parameters** \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`b` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Normalized(Vector2)

```csharp
public Vector2 Normalized(Vector2 vector)
```

Returns a unit-length vector in the same direction. Divides by zero (producing NaN) if the vector's length is 0 — use `NormalizedWithSanity` if that input is possible.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### NormalizedWithSanity(Vector2)

```csharp
public Vector2 NormalizedWithSanity(Vector2 vector)
```

Like `Normalized`, but returns `Vector2.Zero` instead of NaN when the input vector has zero length.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Perpendicular(Vector2)

```csharp
public Vector2 Perpendicular(Vector2 vector)
```

Returns the perpendicular vector to the given vector (rotated 90° counter-clockwise).

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### PerpendicularClockwise(Vector2)

```csharp
public Vector2 PerpendicularClockwise(Vector2 vector)
```

Returns the vector rotated 90° clockwise. Same result as `PerpendicularRight`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### PerpendicularCounterClockwise(Vector2)

```csharp
public Vector2 PerpendicularCounterClockwise(Vector2 vector)
```

Returns the vector rotated 90° counter-clockwise. Same result as `Perpendicular`/`PerpendicularLeft`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### PerpendicularLeft(Vector2)

```csharp
public Vector2 PerpendicularLeft(Vector2 vector)
```

Same as `Perpendicular`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### PerpendicularRight(Vector2)

```csharp
public Vector2 PerpendicularRight(Vector2 vector)
```

Returns the perpendicular right vector to the given vector.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Reverse(Vector2)

```csharp
public Vector2 Reverse(Vector2 vector)
```

Returns the vector negated (pointing in the opposite direction), same as unary `-vector`.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Rotate(Vector2, float)

```csharp
public Vector2 Rotate(Vector2 vector, float angle)
```

Returns a new vector, rotated by the given angle. In radians.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) — The vector to rotate. \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — The angle to rotate by. \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### SnapAngle(Vector2, int)

```csharp
public Vector2 SnapAngle(Vector2 vector, int steps)
```

Snap the angel to the nearest angle, based on the number of steps in a circle.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`steps` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToVector3(Vector2)

```csharp
public Vector3 ToVector3(Vector2 vector)
```

Converts to an XNA `Vector3` with Z set to 0, e.g. for feeding into shader parameters or MonoGame APIs that need a 3D vector.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector3](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector3.html) \

⚡
