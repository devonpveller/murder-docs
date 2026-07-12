# GridMenuFlags

**Namespace:** Murder.Core.Input \
**Assembly:** Murder.dll

```csharp
[Flags]
public sealed enum GridMenuFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags controlling how cursor navigation behaves at the edges of a grid or list menu.

**Intent:** By default (`None`) navigation wraps around to the opposite edge; the `Clamp*` flags instead stop the cursor at that edge, which is typically what you want for paginated or non-looping menus.

**Use-case:** Pass a combination of these flags to `PlayerInput.GridMenu<T>(ref GenericMenuInfo<T>, int, int, GridMenuFlags)` or the `MenuInfo` overload to control wrapping, disabled-option selection, and rotated navigation for a grid-based menu.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### ClampAllDirections

```csharp
public static const GridMenuFlags ClampAllDirections;
```

Combines `ClampRight`, `ClampLeft`, `ClampTop` and `ClampBottom` to disable wrapping on every edge.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

#### ClampBottom

```csharp
public static const GridMenuFlags ClampBottom;
```

Prevents cursor movement past the bottom edge instead of wrapping to the first row.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

#### ClampLeft

```csharp
public static const GridMenuFlags ClampLeft;
```

Prevents cursor movement past the left edge instead of wrapping to the rightmost column.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

#### ClampRight

```csharp
public static const GridMenuFlags ClampRight;
```

Prevents cursor movement past the right edge instead of wrapping to the leftmost column.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

#### ClampSize

```csharp
public static const GridMenuFlags ClampSize;
```

Clamps the computed selected index to the valid range instead of letting grid-position math land outside the option array (e.g. on a ragged last row).

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

#### ClampTop

```csharp
public static const GridMenuFlags ClampTop;
```

Prevents cursor movement past the top edge instead of wrapping to the last row.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

#### None

```csharp
public static const GridMenuFlags None;
```

No clamping; the cursor wraps around to the opposite edge/row/column when moving past any side of the grid.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

#### Rotate

```csharp
public static const GridMenuFlags Rotate;
```

Swaps the horizontal/vertical axis mapping used for grid navigation, for grids whose visual layout is rotated 90 degrees relative to the logical row/column order.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

#### SelectDisabled

```csharp
public static const GridMenuFlags SelectDisabled;
```

Allows the cursor to land on disabled options instead of skipping over them.

**Returns** \
[GridMenuFlags](../../../Murder/Core/Input/GridMenuFlags.html) \

⚡
