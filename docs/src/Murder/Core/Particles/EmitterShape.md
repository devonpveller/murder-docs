# EmitterShape

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct EmitterShape
```

Defines the geometric area from which particles are spawned, along with the shape-specific data (rectangle, line, or circle).

**Intent:** Describe the spatial origin of a particle emitter.

**Use-case:** Set `Kind` to the desired `EmitterShapeKind` and populate the corresponding geometry field (`Rectangle`, `Line`, or `Circle`) on the emitter asset. Call `GetRandomPosition()` at runtime to obtain a spawn origin for each particle.

### ⭐ Constructors
```csharp
public EmitterShape()
```

### ⭐ Properties
#### Circle
```csharp
public readonly Circle Circle;
```

The circle used when `Kind` is `EmitterShapeKind.Circle` or `EmitterShapeKind.CircleOutline`.

**Returns** \
[Circle](../../../Murder/Core/Geometry/Circle.html) \
#### Kind
```csharp
public readonly EmitterShapeKind Kind;
```

The type of shape from which particles originate.

**Returns** \
[EmitterShapeKind](../../../Murder/Core/Particles/EmitterShapeKind.html) \
#### Line
```csharp
public readonly Line2 Line;
```

The line segment used when `Kind` is `EmitterShapeKind.Line`.

**Returns** \
[Line2](../../../Murder/Core/Geometry/Line2.html) \
#### Rectangle
```csharp
public readonly Rectangle Rectangle;
```

The rectangle used when `Kind` is `EmitterShapeKind.Rectangle`.

**Returns** \
[Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
### ⭐ Methods
#### GetRandomPosition(Random)
```csharp
public Vector2 GetRandomPosition(Random random)
```

Returns a random spawn position within or along this emitter shape.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \



⚡