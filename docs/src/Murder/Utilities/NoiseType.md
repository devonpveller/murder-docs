# NoiseType

**Namespace:** Murder.Utilities \
**Assembly:** Murder.dll

```csharp
public sealed enum NoiseType : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Identifies which simplex noise algorithm implementation to use when sampling noise.

**Intent:** Allows callers to select between available noise implementations by name rather than instantiating different classes.

**Use-case:** Pass to `NoiseHelper` methods or noise-generating components to choose the desired algorithm.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Carmody
#### Carmody
#### Carmody
```csharp
public static const NoiseType Carmody;
```

Use Carmody's 3D Simplex Noise implementation.

**Returns** \
[NoiseType](../../Murder/Utilities/NoiseType.html) \
#### Gustavson
#### Gustavson
#### Gustavson
```csharp
public static const NoiseType Gustavson;
```

Use Gustavson's 2D Simplex Noise implementation.

**Returns** \
[NoiseType](../../Murder/Utilities/NoiseType.html) \


⚡