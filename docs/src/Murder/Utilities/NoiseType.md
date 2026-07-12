# NoiseType

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed enum NoiseType : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies which simplex noise implementation a caller wants: Carmody's (3D, based on Stephen Carmody's implementation) or Gustavson's (2D/3D, based on Stefan Gustavson's implementation).

**Intent:** Lets internal helpers such as `NoiseHelper`'s private `FractionalBrownianMotion` overloads select an algorithm by value instead of duplicating the octave-summing logic per implementation.

**Use-case:** This enum is currently consumed only by `NoiseHelper`'s private fractional Brownian motion helpers; public callers instead call `NoiseHelper.CarmodyNoise` / `NoiseHelper.GustavsonNoise` directly.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Carmody

```csharp
public static const NoiseType Carmody;
```

Use Carmody's simplex noise implementation (see `NoiseHelper.CarmodyNoise`).

**Returns** \
[NoiseType](../../Murder/Utilities/NoiseType.html) \

#### Gustavson

```csharp
public static const NoiseType Gustavson;
```

Use Gustavson's simplex noise implementation (see `NoiseHelper.GustavsonNoise`).

**Returns** \
[NoiseType](../../Murder/Utilities/NoiseType.html) \

⚡
