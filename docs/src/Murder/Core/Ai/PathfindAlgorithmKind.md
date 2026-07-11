# PathfindAlgorithmKind

**Namespace:** Murder.Core.Ai \
**Assembly:** Murder.dll

```csharp
public sealed enum PathfindAlgorithmKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Selects which pathfinding algorithm is used when requesting a path via `PathfindServices.FindPath`.

**Intent:** Enum that lets systems and components specify the desired pathfinding strategy.

**Use-case:** Set on the pathfinding component or pass directly to `PathfindServices.FindPath` to choose between standard A* and the faster hierarchical HAAstar.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties
#### Astar
```csharp
public static const PathfindAlgorithmKind Astar;
```

Use standard A* to find the path. Accurate but slower on large maps.

**Returns** \
[PathfindAlgorithmKind](../../../Murder/Core/Ai/PathfindAlgorithmKind.html) \
#### HAAstar
```csharp
public static const PathfindAlgorithmKind HAAstar;
```

Use Hierarchical A* (HAAstar) for faster path queries on large maps.

**Returns** \
[PathfindAlgorithmKind](../../../Murder/Core/Ai/PathfindAlgorithmKind.html) \
#### None
```csharp
public static const PathfindAlgorithmKind None;
```

No pathfinding algorithm is applied; the entity will not attempt to navigate.

**Returns** \
[PathfindAlgorithmKind](../../../Murder/Core/Ai/PathfindAlgorithmKind.html) \


⚡