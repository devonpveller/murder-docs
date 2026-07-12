# PathfindServices

**Namespace:** Murder.Core.Ai \
**Assembly:** Murder.dll

```csharp
public static class PathfindServices
```

Static utility methods for running pathfinding queries against the current map and managing cached pathfind state.

**Intent:** Central API for requesting navigation paths and refreshing the cached pathfind graph when the map changes.

**Use-case:** Call `FindPath` from AI systems to get a route between two grid points, and `UpdatePathfind` whenever map geometry changes to keep the `HAAStar` graph consistent.

### ⭐ Methods

#### FindPath(Map, World, Point, Point, PathfindAlgorithmKind, int, out PathfindStatusFlags&)

```csharp
public ComplexDictionary<TKey, TValue> FindPath(Map map, World world, Point initial, Point target, PathfindAlgorithmKind kind, int collisionMask, PathfindStatusFlags& statusFlags)
```

Main entry point for gameplay/AI code that needs to move an entity from `initial` to `target`. Picks the concrete algorithm based on `kind`, but first takes a couple of cheap shortcuts: if `map` is `null` or there is a clear line of sight between the two points, it returns a straight line instead of running a full search. The result is a dictionary mapping each step of the route to the next step, suitable for a "walk to next tile" style of consumption. This method is an extension method on `Map` — call it as `map.FindPath(...)`.

**Parameters** \
`map` [Map](../../../Murder/Core/Map.html) \
`world` [World](../../../Bang/World.html) \
`initial` [Point](../../../Murder/Core/Geometry/Point.html) \
`target` [Point](../../../Murder/Core/Geometry/Point.html) \
`kind` [PathfindAlgorithmKind](../../../Murder/Core/Ai/PathfindAlgorithmKind.html) \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`statusFlags` [PathfindStatusFlags&](../../../Murder/Components/PathfindStatusFlags.html) \

**Returns** \
[ComplexDictionary\<TKey, TValue\>](../../../Murder/Serialization/ComplexDictionary-2.html) \

#### StraightLine(Point, Point)

```csharp
public ComplexDictionary<TKey, TValue> StraightLine(Point initial, Point target)
```

Builds a trivial single-step route directly from `initial` to `target`, skipping any obstacle avoidance. Used as the fast path by `FindPath` whenever there is a clear line of sight (or no map to navigate against), and by `HAAStar` when connecting a query point straight to a border node.

**Parameters** \
`initial` [Point](../../../Murder/Core/Geometry/Point.html) \
`target` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[ComplexDictionary\<TKey, TValue\>](../../../Murder/Serialization/ComplexDictionary-2.html) \

#### UpdatePathfind(World)

```csharp
public void UpdatePathfind(World world)
```

Refreshes the cached hierarchical pathfind graph after the map's collision geometry changes (e.g. a door opens, a wall is carved). Looks up the world's unique `HAAStar` instance and calls `Refresh` on it; does nothing if no map or no HAAstar graph exists yet. Systems that mutate the map (carving, procedural generation, etc.) should call this once they're done.

**Parameters** \
`world` [World](../../../Bang/World.html) \

⚡
