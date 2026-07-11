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

**Parameters** \
`constant` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public ParticleIntValueProperty(int rangeStart, int rangeEnd)
```

**Parameters** \
`rangeStart` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`rangeEnd` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

```csharp
public ParticleIntValueProperty(int rangeStartMin, int rangeStartMax, int rangeEndMin, int rangeEndMax)
```

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

Returns the maximum possible value this property can produce, used for pool-size calculations.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### GetValue(Random)
```csharp
public int GetValue(Random random)
```

Samples the property and returns a concrete integer value using `random` for range evaluation.

**Parameters** \
`random` [Random](https://learn.microsoft.com/en-us/dotnet/api/System.Random?view=net-7.0) \

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \



⚡