# HAAStar

**Namespace:** Murder.Core.Ai \
**Assembly:** Murder.dll

```csharp
public class HAAStar
```

Hierarchical A* (HAAstar) pathfinding implementation that divides the map into clusters and builds an abstract graph for fast long-distance path queries.

**Intent:** A faster alternative to plain A* for large tile maps — it pre-builds a cluster-based hierarchy so searches avoid exploring the entire map.

**Use-case:** Instantiate with map dimensions, call `Refresh` when the map changes, then call `Search` to find a path between two grid positions.

### ⭐ Constructors
```csharp
public HAAStar(int width, int height)
```

Creates an `HAAStar` instance sized for a map of `width` × `height` tiles.

**Parameters** \
`width` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`height` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### CLUSTER_SIZE
```csharp
public static const int CLUSTER_SIZE;
```

The side length (in tiles) of each cluster used by the hierarchical search.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### ClusterHeight
```csharp
public readonly int ClusterHeight;
```

The number of clusters along the vertical axis.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### ClusterWidth
```csharp
public readonly int ClusterWidth;
```

The number of clusters along the horizontal axis.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### DebugNodes
```csharp
public ImmutableDictionary<TKey, TValue> DebugNodes;
```

The abstract graph nodes built by the last `Refresh` call, exposed for editor visualization and debugging.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
### ⭐ Methods
#### Search(Map, Point, Point)
```csharp
public ImmutableDictionary<TKey, TValue> Search(Map map, Point initial, Point target)
```

Searches for a path from `initial` to `target` using the pre-built cluster graph. Returns a dictionary mapping each step to the next point on the path.

**Parameters** \
`map` [Map](../../../Murder/Core/Map.html) \
`initial` [Point](../../../Murder/Core/Geometry/Point.html) \
`target` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### Refresh(Map)
```csharp
public void Refresh(Map map)
```

Rebuilds the cluster graph and abstract nodes from the current state of `map`. Call this whenever the map changes.

**Parameters** \
`map` [Map](../../../Murder/Core/Map.html) \



⚡