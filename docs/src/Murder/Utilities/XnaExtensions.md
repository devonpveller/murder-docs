# XnaExtensions

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class XnaExtensions
```

Conversion extension methods between MonoGame/XNA types (`Microsoft.Xna.Framework.*`, used by the rendering backend) and the `System.Numerics`/engine types (`System.Numerics.Vector2`, `Point`, `Rectangle`) used everywhere else in Murder's own code.

**Intent:** Prefer these over manual field-by-field construction so conversions stay consistent (e.g. rounding rules) across the codebase.

**Use-case:** Use when passing data between MonoGame API calls and engine math code; prefer these helpers over manual component assignment.

### ⭐ Methods

#### ToSysVector4(Color)

```csharp
public Vector4 ToSysVector4(Color color)
```

Converts a MonoGame `Color` to a `System.Numerics.Vector4` RGBA value (each channel in [0, 1]), via XNA's own `ToVector4`.

**Parameters** \
`color` [Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \

**Returns** \
[Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

#### ToXnaColor(Vector4)

```csharp
public Color ToXnaColor(Vector4 color)
```

Converts a `System.Numerics.Vector4` RGBA value (each channel in [0, 1]) to a MonoGame `Color`.

**Parameters** \
`color` [Vector4](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector4?view=net-7.0) \

**Returns** \
[Color](https://docs.monogame.net/api/Microsoft.Xna.Framework.Color.html) \

#### ToXnaPoint(Vector2)

```csharp
public Point ToXnaPoint(Vector2 vector2)
```

Converts a `System.Numerics.Vector2` to a MonoGame `Point` by rounding each component to the nearest integer.

**Parameters** \
`vector2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](https://docs.monogame.net/api/Microsoft.Xna.Framework.Point.html) \

#### ToRectangle(float, float, float, float)

```csharp
public Rectangle ToRectangle(float x, float y, float width, float height)
```

Builds an engine `Rectangle` from float bounds, rounding each value to the nearest integer.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`width` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`height` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

**Returns** \
[Rectangle](../../Murder/Core/Geometry/Rectangle.html) \

#### ToVector2(Vector2)

```csharp
public Vector2 ToVector2(Vector2 v)
```

Converts a `System.Numerics.Vector2` to a MonoGame `Vector2` for passing into XNA/MonoGame APIs.

**Parameters** \
`v` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### Size(Rectangle)

```csharp
public Point Size(Rectangle this)
```

Returns the width/height of a MonoGame `Rectangle` as an engine `Point`.

**Parameters** \
`this` [Rectangle](https://docs.monogame.net/api/Microsoft.Xna.Framework.Rectangle.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### XnaSize(Rectangle)

```csharp
public Vector2 XnaSize(Rectangle this)
```

Returns the width/height of a MonoGame `Rectangle` as a MonoGame `Vector2`.

**Parameters** \
`this` [Rectangle](https://docs.monogame.net/api/Microsoft.Xna.Framework.Rectangle.html) \

**Returns** \
[Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### ToPoint(Vector2) — `System.Numerics.Vector2`

```csharp
public Point ToPoint(Vector2 vector)
```

Converts a `System.Numerics.Vector2` to an engine `Point` by rounding each component to the nearest integer.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToPoint(Vector2) — `Microsoft.Xna.Framework.Vector2`

```csharp
public Point ToPoint(Vector2 vector)
```

Converts a MonoGame `Vector2` to an engine `Point` by rounding each component to the nearest integer.

**Parameters** \
`vector` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### ToSysVector2(Point)

```csharp
public Vector2 ToSysVector2(Point point)
```

Converts a MonoGame `Point` to a `System.Numerics.Vector2`.

**Parameters** \
`point` [Point](https://docs.monogame.net/api/Microsoft.Xna.Framework.Point.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToSysVector2(Vector2)

```csharp
public Vector2 ToSysVector2(Vector2 vector)
```

Converts a MonoGame `Vector2` to a `System.Numerics.Vector2`.

**Parameters** \
`vector` [Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### ToXnaVector2(Vector2)

```csharp
public Vector2 ToXnaVector2(Vector2 vector)
```

Converts a `System.Numerics.Vector2` to a MonoGame `Vector2`. Equivalent to `ToVector2(Vector2)` but usable as an instance-style extension.

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://docs.monogame.net/api/Microsoft.Xna.Framework.Vector2.html) \

#### ToCore(Vector2)

```csharp
public Vector2 ToCore(Vector2 vector)
```

Returns a copy of the `System.Numerics.Vector2`. A no-op conversion kept for symmetry with the other `To*` helpers (e.g. when a generic call site needs "convert to the engine's own vector type" regardless of the source type).

**Parameters** \
`vector` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
