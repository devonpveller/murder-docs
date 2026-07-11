# NextAvailablePositionFlags

**Namespace:** Murder.Services \
**Assembly:** Murder.dll

```csharp
sealed enum NextAvailablePositionFlags : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Flags that control the search strategy used by `PhysicsServices.FindNextAvailablePosition`.

**Intent:** Configures which additional checks are performed when searching for a free grid position near an entity.

**Use-case:** Pass `CheckNeighbours` to allow the search to scan adjacent tiles, or combine with `CheckLineOfSight` to ensure the found position is also visible from the origin.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### CheckLineOfSight
```csharp
public static const NextAvailablePositionFlags CheckLineOfSight;
```
Also verifies that the candidate position has line of sight to the origin.

**Returns** \
[NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \
#### CheckNeighbours
```csharp
public static const NextAvailablePositionFlags CheckNeighbours;
```
Expands the search to include cells adjacent to the target position.

**Returns** \
[NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \
#### CheckRecursiveNeighbours
```csharp
public static const NextAvailablePositionFlags CheckRecursiveNeighbours;
```
Expands the search recursively through neighbouring cells until a free position is found.

**Returns** \
[NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \
#### CheckTarget
```csharp
public static const NextAvailablePositionFlags CheckTarget;
```
Checks the exact target position first before expanding the search.

**Returns** \
[NextAvailablePositionFlags](../../Murder/Services/NextAvailablePositionFlags.html) \


⚡