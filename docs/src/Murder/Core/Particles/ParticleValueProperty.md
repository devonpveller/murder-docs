# ParticleValueProperty

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct ParticleValueProperty
```

A float-valued property that can be a constant, a random range, a range-of-ranges, or a curve, used to drive scalar particle attributes over their lifetime.

**Intent:** Provide a flexible, designer-friendly float value source for particle system parameters.

**Use-case:** Assign a `ParticleValueProperty` to fields such as `Particle.Alpha`, `Particle.LifeTime`, or `Emitter.Speed`. Use the range constructors to randomise values per particle, or `GetValueAt(delta)` to sample a curve over the particle's lifetime.

### ⭐ Constructors

```csharp
public ParticleValueProperty()
```

```csharp
public ParticleValueProperty(float constant)
```

Creates a property that always evaluates to the same fixed `constant` value.

**Parameters** \
`constant` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public ParticleValueProperty(float rangeStart, float rangeEnd)
```

Creates a property that samples a single uniform range: `GetRandomValue` returns a random value between `rangeStart` and `rangeEnd`, and `GetValueAt` linearly interpolates between them by lifetime delta.

**Parameters** \
`rangeStart` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rangeEnd` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public ParticleValueProperty(float rangeStartMin, float rangeStartMax, float rangeEndMin, float rangeEndMax)
```

Intended to build a property that randomly picks one of two sub-ranges (start-range or end-range) and returns a value from within that sub-range — i.e. a `ParticleValuePropertyKind.RangedStartAndRangedEnd` property. **In the current implementation this constructor sets `Kind` to `Range` instead of `RangedStartAndRangedEnd`**, so `GetRandomValue`/`GetValueAt` read the unset (zero) `rangeStart`/`rangeEnd` fields rather than the four values passed in here — calling this overload currently produces a property that evaluates as a constant `0`, not the two-sub-range behaviour its parameters imply. The same issue exists on the equivalent `ParticleIntValueProperty` and `ParticleVectorValueProperty` constructors.

**Parameters** \
`rangeStartMin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rangeStartMax` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rangeEndMin` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`rangeEndMax` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Empty

```csharp
public static ParticleValueProperty Empty { get; }
```

A constant-1 property used as a default placeholder.

**Returns** \
[ParticleValueProperty](../../../Murder/Core/Particles/ParticleValueProperty.html) \

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
public float GetRandomValue(Random random)
```

Samples this property once, returning a concrete float value appropriate for spawn-time attributes (e.g. an emitter's `Speed` or a particle's `StartVelocity`). Curve-kind properties are not yet implemented and currently fall back to `1`.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### GetValueAt(float)

```csharp
public float GetValueAt(float delta)
```

Get the value of this property over a delta lifetime.

**Parameters** \
`delta` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
\

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
