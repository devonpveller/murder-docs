# RoundingMode

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed enum RoundingMode : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Selects how a floating-point value should be converted to an integer, e.g. when snapping a world-space position to a pixel or grid coordinate.

**Intent:** Lets a coordinate/rounding helper take the desired snapping strategy as a parameter instead of hardcoding a call to `Math.Round`/`Math.Floor`/`Math.Ceiling`.

**Use-case:** Pass to a coordinate-conversion helper to control whether a value snaps to the nearest, floors, ceils, or is left unrounded. As of this writing this enum is not yet consumed anywhere in the engine's own code — it exists as a reusable rounding-strategy vocabulary for game code and future coordinate helpers to opt into.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Ceiling

```csharp
public static const RoundingMode Ceiling;
```

Always round up (towards positive infinity).

**Returns** \
[RoundingMode](../../Murder/Core/RoundingMode.html) \

#### Floor

```csharp
public static const RoundingMode Floor;
```

Always round down (towards negative infinity).

**Returns** \
[RoundingMode](../../Murder/Core/RoundingMode.html) \

#### None

```csharp
public static const RoundingMode None;
```

Do not round; keep the value as a float/truncate only when a hard integer conversion is unavoidable.

**Returns** \
[RoundingMode](../../Murder/Core/RoundingMode.html) \

#### Round

```csharp
public static const RoundingMode Round;
```

Round to the nearest integer (ties follow standard .NET rounding rules).

**Returns** \
[RoundingMode](../../Murder/Core/RoundingMode.html) \

⚡
