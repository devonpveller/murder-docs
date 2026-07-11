# SoundParameterKind

**Namespace:** Murder.Utilities.Attributes \
**Assembly:** Murder.dll

```csharp
public sealed enum SoundParameterKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Specifies the scope of a sound parameter reference.

**Intent:** Specifies the scope of a sound parameter reference.

**Use-case:** Pass to `SoundParameterAttribute` to indicate whether the field should show local event parameters, global parameters, or both.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### All
```csharp
public static const SoundParameterKind All;
```

Includes both local and global sound parameters.

**Returns** \
[SoundParameterKind](../../../Murder/Utilities/Attributes/SoundParameterKind.html) \
#### Global
```csharp
public static const SoundParameterKind Global;
```

Restricts to globally-scoped sound parameters.

**Returns** \
[SoundParameterKind](../../../Murder/Utilities/Attributes/SoundParameterKind.html) \
#### Local
```csharp
public static const SoundParameterKind Local;
```

Restricts to parameters local to a specific sound event.

**Returns** \
[SoundParameterKind](../../../Murder/Utilities/Attributes/SoundParameterKind.html) \


⚡