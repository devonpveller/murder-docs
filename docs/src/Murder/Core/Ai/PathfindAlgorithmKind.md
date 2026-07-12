# PathfindAlgorithmKind

**Namespace:** Murder.Core.Ai \
**Assembly:** Murder.dll

```csharp
public sealed enum PathfindAlgorithmKind : Enum, IComparable, ISpanFormattable, IFormattable, IConvertible
```

Selects which pathfinding algorithm is used when requesting a path via `PathfindServices.FindPath`.

**Intent:** Enum that lets systems and components specify the desired pathfinding strategy.

**Use-case:** Set on the pathfinding component or pass directly to `PathfindServices.FindPath` to choose between standard A\* and the faster hierarchical HAAstar.

**Implements:** _[Enum](https://learn.microsoft.com/en-us/dotnet/api/System.Enum?view=net-7.0), [IComparable](https://learn.microsoft.com/en-us/dotnet/api/System.IComparable?view=net-7.0), [ISpanFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.ISpanFormattable?view=net-7.0), [IFormattable](https://learn.microsoft.com/en-us/dotnet/api/System.IFormattable?view=net-7.0), [IConvertible](https://learn.microsoft.com/en-us/dotnet/api/System.IConvertible?view=net-7.0)_

### ⭐ Properties

#### Astar

```csharp
public static const PathfindAlgorithmKind Astar;
```

Use the standard tile-by-tile A\* search. Always finds the optimal path but explores the whole map, so it is more expensive on large maps than `HAAstar`.

**Returns** \
[PathfindAlgorithmKind](../../../Murder/Core/Ai/PathfindAlgorithmKind.html) \

#### AstarStrict

```csharp
public static const PathfindAlgorithmKind AstarStrict;
```

Use standard A\* in "strict" mode, which disallows cutting diagonally between two blocked tiles. Useful when the agent's collider cannot squeeze through a diagonal gap.

**Returns** \
[PathfindAlgorithmKind](../../../Murder/Core/Ai/PathfindAlgorithmKind.html) \

#### HAAstar

```csharp
public static const PathfindAlgorithmKind HAAstar;
```

Use the hierarchical A\* search (`HAAStar`), which pre-builds a cluster graph so repeated long-distance queries are much cheaper. Preferred for most gameplay agents on large maps.

**Returns** \
[PathfindAlgorithmKind](../../../Murder/Core/Ai/PathfindAlgorithmKind.html) \

#### None

```csharp
public static const PathfindAlgorithmKind None;
```

Skip pathfinding entirely; `PathfindServices.FindPath` will fall back to a straight line between the two points instead of navigating around obstacles.

**Returns** \
[PathfindAlgorithmKind](../../../Murder/Core/Ai/PathfindAlgorithmKind.html) \

⚡
