# NextAvailablePositionFlags

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
[Flags]
public sealed enum NextAvailablePositionFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags that control the search strategy used by `PhysicsServices.FindNextAvailablePosition` (nested inside `PhysicsServices` as `PhysicsServices.NextAvailablePositionFlags`).

**Intent:** Configures which parts of the "find a free spot near a target" search are performed. Only `CheckNeighbours` and `CheckLineOfSight` are actually read by the current search algorithm; `CheckTarget` and `CheckRecursiveNeighbours` are defined bits that are included in the default flag combination but are not individually branched on by the implementation today (the algorithm always checks the target position first, and always expands recursively while `CheckNeighbours` is set, regardless of whether these two bits are present).

**Use-case:** Pass `NextAvailablePositionFlags.CheckNeighbours` (the default) to let the search fan out to adjacent grid cells when the exact target is occupied, or combine with `CheckLineOfSight` to reject candidate positions that aren't visible from the search's starting point (e.g. so a thrown item doesn't land somewhere the thrower can't see). Omit `CheckNeighbours` to restrict the search to the target position alone.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### CheckLineOfSight

```csharp
public static const NextAvailablePositionFlags CheckLineOfSight = 0b01;
```

When set, a candidate position is only accepted if it also has line of sight (`Map.HasLineOfSight`) back to the search's starting grid point. This is the one flag, besides `CheckNeighbours`, that the search algorithm actually checks.

**Returns** \
[NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \

#### CheckNeighbours

```csharp
public static const NextAvailablePositionFlags CheckNeighbours = 0b10;
```

When set, the search expands to the neighbouring grid cells of the target (and then their neighbours, breadth-first, up to an internal depth limit) if the target position itself is unavailable. This is the flag that actually enables the "find nearby free space" behavior; without it, the search only ever checks the exact target position.

**Returns** \
[NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \

#### CheckRecursiveNeighbours

```csharp
public static const NextAvailablePositionFlags CheckRecursiveNeighbours = 0b100;
```

Only meaningful if `CheckNeighbours` is set. Included in `FindNextAvailablePosition`'s default flags combination, but not currently read directly by the search implementation — the breadth-first neighbour expansion always happens (bounded by an internal depth limit) whenever `CheckNeighbours` is set, regardless of this bit.

**Returns** \
[NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \

#### CheckTarget

```csharp
public static const NextAvailablePositionFlags CheckTarget = 0b1000;
```

Included in `FindNextAvailablePosition`'s default flags combination. The search always evaluates the exact target position first regardless of this bit; it is not individually checked by the current implementation.

**Returns** \
[NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \

⚡
