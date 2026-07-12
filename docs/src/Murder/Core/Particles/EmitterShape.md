# EmitterShape

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct EmitterShape
```

Defines the geometric area from which particles are spawned, along with the shape-specific data (rectangle, line, or circle).

**Intent:** Describe the spatial origin of a particle emitter.

**Use-case:** Set `Kind` to the desired `EmitterShapeKind` and populate the corresponding geometry field (`Rectangle`, `Line`, or `Circle`) on the emitter asset (typically via `Emitter.WithShape` or an object initializer on `Emitter.Shape`). `ParticleSystemTracker.CreateParticle` calls `GetRandomPosition()` at spawn time to pick each new particle's local starting offset, and `Emitter.BoundingBoxSize()` reads the same geometry fields to compute the emitter's bounds for camera culling.

### ⭐ Constructors

```csharp
public EmitterShape()
```

The only constructor. Leaves `Kind` at `EmitterShapeKind.Point` (all particles fire from a single origin) with the `Rectangle`/`Line`/`Circle` fields at their unit-sized defaults, so a bare `new EmitterShape()` is a valid, minimal shape. Since every field is `readonly` with a default, callers build a customised shape with an object initializer, e.g. `new EmitterShape() { Kind = EmitterShapeKind.Circle, Circle = new Circle(32) }`.

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

Returns a random spawn position within or along this shape, relative to the emitter's own position: the exact centre for `Point`, a random point along `Line`, a random interior point for `Circle` (or a point exactly on its perimeter for `CircleOutline`), or a random point within `Rectangle`. Called once per particle by `ParticleSystemTracker` when it creates a new `ParticleRuntime`.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
