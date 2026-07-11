# Vector2Helper

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public static class Vector2Helper
```

Static helpers and well-known direction constants for `System.Numerics.Vector2`.

**Intent:** Provides a set of named direction vectors and utility extension methods that supplement the `System.Numerics.Vector2` API for game use.

**Use-case:** Use `Up`, `Down`, `Left`, `Right`, and `Center` as direction/anchor constants, and the extension methods for smooth lerping, snapping, and projection math.

### ⭐ Properties
#### Center
```csharp
public static Vector2 Center { get; }
```

Returns (0.5, 0.5) — useful as a normalized center anchor for sprites.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### Down
```csharp
public static Vector2 Down { get; }
```

Returns (0, 1) — the downward direction in screen space.

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

Returns (0, -1) — the upward direction in screen space.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
### ⭐ Methods
#### CalculateAngle(Vector2, Vector2, Vector2)
```csharp
public float CalculateAngle(Vector2 a, Vector2 b, Vector2 c)
```

Calculates the internal angle of a triangle.

**Parameters** \
`a` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`b` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\
`c` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

#### Deviation(Vector2, Vector2)
```csharp
public float Deviation(Vector2 vec1, Vector2 vec2)
```

Returns the angular deviation (in radians) between two direction vectors.

**Parameters** \
`vec1` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`vec2` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### FromAngle(float)
```csharp
public Vector2 FromAngle(float angle)
```

Creates a vector from an angle in radians.

**Parameters** \
`angle` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
\

#### LerpSmooth(Vector2, Vector2, float, float)
```csharp
public Vector2 LerpSmooth(Vector2 from, Vector2 to, float deltaTime, float halfLife)
```

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

**Parameters** \
`first` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`second` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Min(Vector2, Vector2)
```csharp
public Vector2 Min(Vector2 first, Vector2 second)
```

**Parameters** \
`first` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`second` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### RoundTowards(Vector2, Vector2)
```csharp
public Vector2 RoundTowards(Vector2 value, Vector2 towards)
```

**Parameters** \
`value` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`towards` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Squish(float)
```csharp
public Vector2 Squish(float ammount)
```

Returns a one unit vector, squished by <paramref name="ammount" />.
            A positive number increases the X, a negative number increases the Y

**Parameters** \
`ammount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \



⚡