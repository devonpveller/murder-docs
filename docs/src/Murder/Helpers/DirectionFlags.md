# DirectionFlags

**Namespace:** Murder.Helpers \
**Assembly:** Murder.dll

```csharp
[Flags]
public sealed enum DirectionFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

A coarse, combinable (bit-flag) version of `Direction` with only the four cardinal directions — used when code cares about "is this generally up/down/left/right" rather than the precise octant.

**Intent:** Lets callers collapse any of the eight `Direction` values down to one of four broad flags via `DirectionHelper.ToDirectionFlag`, and — because it is a `[Flags]` enum — combine multiple directions with bitwise OR where that's meaningful (e.g. tracking which cardinal directions are currently blocked or pressed).

**Use-case:** Call `direction.ToDirectionFlag()` to bucket a precise `Direction` (including diagonals) into `Up`, `Down`, `Left`, or `Right` for coarse-grained logic such as picking a 4-directional animation set or checking simple directional input state.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Down

```csharp
public static const DirectionFlags Down;
```

Flag bit (`0x10`) representing any downward-facing direction (`Direction.Down`, `Direction.DownLeft`, or `Direction.DownRight`).

**Returns** \
[DirectionFlags](../../Murder/Helpers/DirectionFlags.html) \

#### Left

```csharp
public static const DirectionFlags Left;
```

Flag bit (`0x100`) representing `Direction.Left`.

**Returns** \
[DirectionFlags](../../Murder/Helpers/DirectionFlags.html) \

#### Right

```csharp
public static const DirectionFlags Right;
```

Flag bit (`0x1`) representing any rightward-or-unresolved direction; this is also the value produced for `Direction.Right` and is the `default`/fallback case of `ToDirectionFlag`.

**Returns** \
[DirectionFlags](../../Murder/Helpers/DirectionFlags.html) \

#### Up

```csharp
public static const DirectionFlags Up;
```

Flag bit (`0x1000`) representing any upward-facing direction (`Direction.Up`, `Direction.UpLeft`, or `Direction.UpRight`).

**Returns** \
[DirectionFlags](../../Murder/Helpers/DirectionFlags.html) \

⚡
