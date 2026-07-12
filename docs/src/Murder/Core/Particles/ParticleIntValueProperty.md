# ParticleIntValueProperty

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed struct ParticleIntValueProperty
```

An integer-valued property that can be a constant, a random range, or a randomised range-of-ranges, used to drive integer particle attributes such as burst count.

**Intent:** Provide a flexible integer value source for particle system parameters.

**Use-case:** Use `ParticleIntValueProperty` in `Emitter.Burst` to specify how many particles fire at once — either always the same number, a random value in a range, or a randomly chosen range.

### ⭐ Constructors

```csharp
public ParticleIntValueProperty()
```

```csharp
public ParticleIntValueProperty(int constant)
```

Creates a property that always evaluates to the same fixed `constant` value.

**Parameters** \
`constant` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public ParticleIntValueProperty(int rangeStart, int rangeEnd)
```

Creates a property that samples a single uniform range: `GetValue` returns a random integer between `rangeStart` (inclusive) and `rangeEnd` (exclusive).

**Parameters** \
`rangeStart` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`rangeEnd` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public ParticleIntValueProperty(int rangeStartMin, int rangeStartMax, int rangeEndMin, int rangeEndMax)
```

Intended to build a property that randomly picks one of two sub-ranges (start-range or end-range) and returns a value from within that sub-range — i.e. a `ParticleValuePropertyKind.RangedStartAndRangedEnd` property. **In the current implementation this constructor sets `Kind` to `Range` instead of `RangedStartAndRangedEnd`**, so `GetValue` reads the unset (zero) `rangeStart`/`rangeEnd` fields rather than the four values passed in here — calling this overload currently produces a property that evaluates as a constant `0`, not the two-sub-range behaviour its parameters imply. The same issue exists on the equivalent `ParticleValueProperty` and `ParticleVectorValueProperty` constructors.

**Parameters** \
`rangeStartMin` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`rangeStartMax` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`rangeEndMin` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`rangeEndMax` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### Empty

```csharp
public static ParticleIntValueProperty Empty { get; }
```

A constant-1 property used as a default placeholder.

**Returns** \
[ParticleIntValueProperty](../../../Murder/Core/Particles/ParticleIntValueProperty.html) \

#### Kind

```csharp
public readonly ParticleValuePropertyKind Kind;
```

Determines whether this property is a constant value, a range, a curve, or a ranged-start/ranged-end.

**Returns** \
[ParticleValuePropertyKind](../../../Murder/Core/Particles/ParticleValuePropertyKind.html) \

### ⭐ Methods

#### CalculateMaxValue()

```csharp
public int CalculateMaxValue()
```

Returns the largest integer value this property could ever produce, without sampling any randomness — intended for pool-sizing calculations (e.g. estimating a worst-case burst size) rather than per-particle evaluation. Curve-kind properties are not yet implemented and currently throw `NotImplementedException`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetValue(Random)

```csharp
public int GetValue(Random random)
```

Samples this property once, returning a concrete integer value appropriate for spawn-time attributes such as `Emitter.Burst`. Curve-kind properties are not yet implemented and currently throw `NotImplementedException`.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
