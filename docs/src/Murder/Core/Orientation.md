# Orientation

**Namespace:** Murder.Core \
**Assembly:** Murder.dll

```csharp
public sealed enum Orientation : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Enumerates the two primary spatial orientations used for movement, collision, and sprite-facing logic.

**Intent:** A simple two-value enum that encodes whether something operates along the horizontal or vertical axis, or either.

**Use-case:** Pass to `OrientationHelper` methods to extract the dominant axis of a movement vector, or store on a component to indicate which axis an entity is currently facing.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Any
```csharp
public static const Orientation Any;
```

Matches either horizontal or vertical orientation; used as a wildcard in queries.

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \
#### Horizontal
```csharp
public static const Orientation Horizontal;
```

The entity or movement is oriented along the X axis.

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \
#### Vertical
```csharp
public static const Orientation Vertical;
```

The entity or movement is oriented along the Y axis.

**Returns** \
[Orientation](../../Murder/Core/Orientation.html) \


⚡