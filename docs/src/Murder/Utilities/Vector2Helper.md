# Vector2Helper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class Vector2Helper
```

Named direction constants and lower-level math helpers for `System.Numerics.Vector2` (projection, smoothing/snapping interpolation, angle construction) that don't fit as instance extension methods in [Vector2Extensions](../../Murder/Utilities/Vector2Extensions.html).

**Intent:** Provides a set of named direction vectors and utility methods that supplement the `System.Numerics.Vector2` API for game use.

**Use-case:** Prefer the direction constants (`Up`, `Down`, `Left`, `Right`, `Center`) over hand-writing vector literals so intent stays readable at call sites, and use the extension methods for smooth lerping, snapping, and projection math.

### ⭐ Properties

#### Center

```csharp
public static Vector2 Center { get; }
```

Returns (0.5, 0.5) — a normalized center anchor, e.g. for sprite draw origins.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Down

```csharp
public static Vector2 Down { get; }
```

Returns (0, 1) — the downward direction in screen space (Y increases downward).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Left

```csharp
public static Vector2 Left { get; }
```

Returns (-1, 0) — the leftward direction.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Right

```csharp
public static Vector2 Right { get; }
```

Returns (1, 0) — the rightward direction.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Up

```csharp
public static Vector2 Up { get; }
```

Returns (0, -1) — the upward direction in screen space (Y increases downward, so up is negative Y).

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Methods

#### CalculateAngle(Vector2, Vector2, Vector2)

```csharp
public float CalculateAngle(Vector2 a, Vector2 b, Vector2 c)
```

Calculates the internal angle of a triangle (the angle at vertex `a`, between rays `a`→`b` and `a`→`c`), in radians.

**Parameters** \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`b` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`c` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Deviation(Vector2, Vector2)

```csharp
public float Deviation(Vector2 vec1, Vector2 vec2)
```

Returns a normalized directional-deviation measure between two vectors, in the range `[0, 1]` — **not** an angle in radians. It normalizes both inputs, takes their dot product (cosine of the angle between them, in `[-1, 1]`) and remaps it so 0 means the vectors point in the same direction and 1 means they point in exactly opposite directions. Useful as a cheap "how aligned are these two directions" score (e.g. for AI facing checks) without computing an actual angle via `Atan2`.

**Parameters** \
`vec1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`vec2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FromAngle(float)

```csharp
public Vector2 FromAngle(float angle)
```

Creates a unit vector from an angle in radians.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — Angle in radians. \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### LerpSmooth(Vector2, Vector2, float, float)

```csharp
public Vector2 LerpSmooth(Vector2 from, Vector2 to, float deltaTime, float halfLife)
```

Smoothly interpolates each component from `from` towards `to` using an exponential decay with the given `halfLife` (time to cover half the remaining distance), via `Calculator.LerpSmooth`. Frame-rate independent, unlike a fixed-factor lerp — call every frame with the real `deltaTime` for smooth camera/UI follow behavior.

**Parameters** \
`from` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`to` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`deltaTime` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`halfLife` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### LerpSnap(Vector2, Vector2, double, float)

```csharp
public Vector2 LerpSnap(Vector2 origin, Vector2 target, double factor, float threshold)
```

Double-precision overload of `LerpSnap(Vector2, Vector2, float, float)`; see that overload for behavior.

**Parameters** \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`factor` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \
`threshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### LerpSnap(Vector2, Vector2, float, float)

```csharp
public Vector2 LerpSnap(Vector2 origin, Vector2 target, float factor, float threshold)
```

Linearly interpolates from `origin` to `target` by `factor`, but snaps directly to `target` once the remaining distance drops below `threshold`, avoiding the infinite asymptotic tail of a plain lerp.

**Parameters** \
`origin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`target` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`factor` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`threshold` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Max(Vector2, Vector2)

```csharp
public Vector2 Max(Vector2 first, Vector2 second)
```

Returns the component-wise maximum of the two vectors.

**Parameters** \
`first` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`second` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Min(Vector2, Vector2)

```csharp
public Vector2 Min(Vector2 first, Vector2 second)
```

Intended to return the component-wise minimum of the two vectors, matching `Max`. **Note:** the current implementation has a bug — the Y component compares `first.X` against `second.Y` instead of `first.Y` against `second.Y`. Verify results before relying on this for Y-axis comparisons.

**Parameters** \
`first` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`second` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Project(Vector2, Vector2)

```csharp
public Vector2 Project(Vector2 vector, Vector2 onNormal)
```

Returns the vector projection of `vector` onto `onNormal` — the component of `vector` that points along `onNormal`'s direction.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`onNormal` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Rejection(Vector2, Vector2)

```csharp
public Vector2 Rejection(Vector2 vector, Vector2 onNormal)
```

Returns the component of `vector` perpendicular to `onNormal` (i.e. `vector` minus its `Project` onto `onNormal`). Useful for splitting a velocity into along-surface and away-from-surface parts.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`onNormal` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### RoundTowards(Vector2, Vector2)

```csharp
public Vector2 RoundTowards(Vector2 value, Vector2 towards)
```

Rounds each component of `value` towards `towards` (ceiling if below, floor if above), rather than always rounding towards zero or a fixed direction.

**Parameters** \
`value` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`towards` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Squish(float)

```csharp
public Vector2 Squish(float ammount)
```

Returns a one unit vector, squished by `ammount`. A positive number increases the X, a negative number increases the Y.

**Parameters** \
`ammount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
