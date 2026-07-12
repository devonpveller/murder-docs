# ParticleVectorValueProperty

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct ParticleVectorValueProperty
```

A `Vector2`-valued property that can be a constant, a random range, or a range-of-ranges, used to drive directional particle attributes such as gravity.

**Intent:** Provide a flexible, designer-friendly 2D vector value source for particle system parameters.

**Use-case:** Assign a `ParticleVectorValueProperty` to fields such as `Particle.Gravity` to set a constant downward pull, or use the range constructors to randomise the direction at spawn time.

### ⭐ Constructors

```csharp
public ParticleVectorValueProperty()
```

```csharp
public ParticleVectorValueProperty(Vector2 constant)
```

Creates a property that always evaluates to the same fixed `constant` vector.

**Parameters** \
`constant` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public ParticleVectorValueProperty(Vector2 rangeStart, Vector2 rangeEnd)
```

Creates a property that samples a single uniform range: `GetRandomValue` returns a random point linearly interpolated between `rangeStart` and `rangeEnd`.

**Parameters** \
`rangeStart` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`rangeEnd` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public ParticleVectorValueProperty(Vector2 rangeStartMin, Vector2 rangeStartMax, Vector2 rangeEndMin, Vector2 rangeEndMax)
```

Intended to build a property that randomly picks one of two sub-ranges (start-range or end-range) and returns a vector from within that sub-range — i.e. a `ParticleValuePropertyKind.RangedStartAndRangedEnd` property. **In the current implementation this constructor sets `Kind` to `Range` instead of `RangedStartAndRangedEnd`**, so `GetRandomValue` reads the unset (zero) `rangeStart`/`rangeEnd` fields rather than the four values passed in here — calling this overload currently produces a property that evaluates as a constant `Vector2.Zero`, not the two-sub-range behaviour its parameters imply. The same issue exists on the equivalent `ParticleValueProperty` and `ParticleIntValueProperty` constructors.

**Parameters** \
`rangeStartMin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`rangeStartMax` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`rangeEndMin` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`rangeEndMax` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### Empty

```csharp
public static ParticleVectorValueProperty Empty { get; }
```

A constant `Vector2.Zero` property used as a default placeholder.

**Returns** \
[ParticleVectorValueProperty](../../../Murder/Core/Particles/ParticleVectorValueProperty.html) \

#### Kind

```csharp
public readonly ParticleValuePropertyKind Kind;
```

Determines whether this property is a constant, a range, a curve, or a ranged-start/ranged-end.

**Returns** \
[ParticleValuePropertyKind](../../../Murder/Core/Particles/ParticleValuePropertyKind.html) \

### ⭐ Methods

#### GetRandomValue(Random)

```csharp
public Vector2 GetRandomValue(Random random)
```

Samples this property once, returning a concrete `Vector2` appropriate for spawn-time attributes such as `Particle.Gravity`. Curve-kind properties are not yet implemented and currently fall back to `Vector2.Zero`.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### GetValueAt(float)

```csharp
public Vector2 GetValueAt(float delta)
```

Get the value of this property over a delta lifetime.

**Parameters** \
`delta` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
