# HAAStar

**Namespace:** Murder.Core.Ai \
**Assembly:** Murder.dll

```csharp
public class HAAStar
```

Hierarchical A\* (HAAstar) pathfinding implementation that divides the map into fixed-size clusters, finds the border "entrance" points between neighbouring clusters, and pre-computes a small abstract graph (`Node`/`Edge`) connecting them so long-distance queries only search that small graph instead of the whole map.

**Intent:** A faster alternative to plain A\* for large tile maps — it pre-builds a cluster-based hierarchy so searches avoid exploring the entire map. One instance is meant to be kept alive for the lifetime of a map and rebuilt whenever the map's collision geometry changes.

**Use-case:** Instantiate with map dimensions, call `Refresh` when the map changes, then call `Search` to find a path between two grid positions. Most gameplay code should go through `PathfindServices.FindPath` with `PathfindAlgorithmKind.HAAstar` rather than calling `Search` directly.

### ⭐ Constructors

```csharp
public HAAStar(int width, int height)
```

Creates an empty `HAAStar` sized to cover a map of `width` × `height` tiles, computing how many clusters fit along each axis. The abstract graph itself is not built until `Refresh` is called with the actual map.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties

#### CLUSTER_SIZE

```csharp
public static const int CLUSTER_SIZE;
```

Side length, in tiles, of each square cluster the map is divided into when building the abstract graph. Smaller values produce a finer, more accurate graph at the cost of more preprocessing and more abstract nodes; larger values are cheaper but coarser. Currently fixed at `5`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ClusterHeight

```csharp
public readonly int ClusterHeight;
```

The number of clusters along the vertical axis, derived from the map height passed to the constructor.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### ClusterWidth

```csharp
public readonly int ClusterWidth;
```

The number of clusters along the horizontal axis, derived from the map width passed to the constructor.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### DebugNodes

```csharp
public ImmutableDictionary<TKey, TValue> DebugNodes;
```

Snapshot of the abstract graph nodes built by the last `Refresh` call. Not consumed by the pathfinding logic itself — it exists purely so editor/debug tooling (`DebugRouteSystem`) can draw the cluster graph on screen.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

### ⭐ Methods

#### Search(Map, Point, Point, int)

```csharp
public ComplexDictionary<TKey, TValue> Search(Map map, Point initial, Point target, int collisionMask)
```

Finds a route from `initial` to `target` using the pre-built abstract cluster graph. Temporarily connects `initial` and `target` to their surrounding cluster border nodes (discarding those connections afterwards if the points were not already part of the graph), then searches the abstract graph and stitches together the cached intra-cluster paths for the final result. If a graph rebuild is currently in progress, this falls back to a plain A\* search instead, since the graph may be in an inconsistent state. This is normally called through `PathfindServices.FindPath` rather than directly.

**Parameters** \
`map` [Map](../../../Murder/Core/Map.html) \
`initial` [Point](../../../Murder/Core/Geometry/Point.html) \
`target` [Point](../../../Murder/Core/Geometry/Point.html) \
`collisionMask` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[ComplexDictionary\<TKey, TValue\>](../../../Murder/Serialization/ComplexDictionary-2.html) \

#### Refresh(Map)

```csharp
public void Refresh(Map map)
```

Rebuilds the abstract cluster graph from the current state of `map`. Cancels any preprocessing that is already in flight and kicks off a new asynchronous rebuild, publishing the result to `DebugNodes` when done. Call this any time the map's collision geometry changes; `PathfindServices.UpdatePathfind` is the usual entry point that does this for you.

**Parameters** \
`map` [Map](../../../Murder/Core/Map.html) \

⚡
