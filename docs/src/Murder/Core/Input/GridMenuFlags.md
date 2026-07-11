# GridMenuFlags

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
sealed enum GridMenuFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags controlling edge-clamping behaviour for grid-based menu navigation.

**Intent:** Restrict cursor movement at the grid boundaries in `PlayerInput.GridMenu()`.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### ClampAll
```csharp
public static const GridMenuFlags ClampAll;
```

Prevents cursor movement beyond any edge of the grid.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \
#### ClampBottom
```csharp
public static const GridMenuFlags ClampBottom;
```

Prevents cursor movement past the bottom edge.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \
#### ClampLeft
```csharp
public static const GridMenuFlags ClampLeft;
```

Prevents cursor movement past the left edge.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \
#### ClampRight
```csharp
public static const GridMenuFlags ClampRight;
```

Prevents cursor movement past the right edge.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \
#### ClampTop
```csharp
public static const GridMenuFlags ClampTop;
```

Prevents cursor movement past the top edge.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \
#### None
```csharp
public static const GridMenuFlags None;
```

No clamping; cursor wraps around when moving past grid edges.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \


⚡