# ParticleValuePropertyKind

**Namespace:** Murder.Core.Particles \
**Assembly:** Murder.dll

```csharp
public sealed enum ParticleValuePropertyKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies the evaluation strategy for a `ParticleValueProperty` or related property.

**Intent:** Control how a particle property value is computed.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Constant
```csharp
public static const ParticleValuePropertyKind Constant;
```

Always returns the same fixed value.

**Returns** \
[ParticleValuePropertyKind](../../../Murder/Core/Particles/ParticleValuePropertyKind.html) \
#### Curve
```csharp
public static const ParticleValuePropertyKind Curve;
```

Evaluates a curve over the particle's lifetime delta (0–1). Not yet fully implemented.

**Returns** \
[ParticleValuePropertyKind](../../../Murder/Core/Particles/ParticleValuePropertyKind.html) \
#### Range
```csharp
public static const ParticleValuePropertyKind Range;
```

Returns a value randomly chosen from a fixed start–end range at spawn time.

**Returns** \
[ParticleValuePropertyKind](../../../Murder/Core/Particles/ParticleValuePropertyKind.html) \
#### RangedStartAndRangedEnd
```csharp
public static const ParticleValuePropertyKind RangedStartAndRangedEnd;
```

Randomly picks one of two sub-ranges and then returns a value from within that sub-range.

**Returns** \
[ParticleValuePropertyKind](../../../Murder/Core/Particles/ParticleValuePropertyKind.html) \


⚡