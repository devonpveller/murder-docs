# Direction

**Namespace:** Murder.Helpers \
**Assembly:** Murder.dll

```csharp
public sealed enum Direction : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

8 directions, enumerated clockwise, starting from right = 0:

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

**Intent:** Encodes facing direction as one of eight compass points for use in movement, animation selection, and spatial queries.

**Use-case:** Use `DirectionHelper.FromVector` to convert a velocity vector to a `Direction`, then use the direction to pick the correct animation row or determine flip state.

### ⭐ Properties

#### Down

```csharp
public static const Direction Down;
```

Facing directly downward (south), index 2 in clockwise order.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### DownLeft

```csharp
public static const Direction DownLeft;
```

Facing down-left (south-west), index 3 in clockwise order.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### DownRight

```csharp
public static const Direction DownRight;
```

Facing down-right (south-east), index 1 in clockwise order.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### Left

```csharp
public static const Direction Left;
```

Facing directly left (west), index 4 in clockwise order.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### Right

```csharp
public static const Direction Right;
```

Facing directly right (east), the default direction at index 0.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### Up

```csharp
public static const Direction Up;
```

Facing directly upward (north), index 6 in clockwise order.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### UpLeft

```csharp
public static const Direction UpLeft;
```

Facing up-left (north-west), index 5 in clockwise order.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

#### UpRight

```csharp
public static const Direction UpRight;
```

Facing up-right (north-east), index 7 in clockwise order.

**Returns** \
[Direction](../../Murder/Helpers/Direction.html) \

⚡
