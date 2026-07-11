# RoundingMode

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed enum RoundingMode : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies how a floating-point value should be rounded when converted to an integer grid coordinate.

**Intent:** Selects the rounding strategy used by grid coordinate conversions so callers can control snapping behavior.

**Use-case:** Pass to coordinate-helper methods to control whether a world position snaps to the floor, ceiling, or nearest grid cell.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Ceiling
```csharp
public static const RoundingMode Ceiling;
```

Round up to the next integer grid cell.

**Returns** \
[RoundingMode](../../Murder/Core/RoundingMode.html) \
#### Floor
```csharp
public static const RoundingMode Floor;
```

Round down to the previous integer grid cell.

**Returns** \
[RoundingMode](../../Murder/Core/RoundingMode.html) \
#### None
```csharp
public static const RoundingMode None;
```

No rounding is applied; the raw float value is used as-is.

**Returns** \
[RoundingMode](../../Murder/Core/RoundingMode.html) \
#### Round
```csharp
public static const RoundingMode Round;
```

Round to the nearest integer grid cell.

**Returns** \
[RoundingMode](../../Murder/Core/RoundingMode.html) \


⚡