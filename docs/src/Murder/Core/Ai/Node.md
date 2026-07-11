# Node

**Namespace:** Murder.Core.Ai \
**Assembly:** Murder.dll

```csharp
class Node
```

A node in the `HAAStar` abstract graph, representing a border point between two clusters along with its neighbours and traversal cost.

**Intent:** Graph vertex used internally by `HAAStar` to represent navigable transition points between clusters.

**Use-case:** Not used directly in gameplay; `HAAStar.Refresh` creates and links nodes, and `HAAStar.Search` traverses them to build paths.

### ⭐ Constructors
```csharp
public Node(Point p, Point c, int weight)
```

Creates a node at tile position `p` belonging to cluster `c` with the given traversal `weight`.

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \
`c` [Point](../../../Murder/Core/Geometry/Point.html) \
`weight` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### Cluster
```csharp
public readonly Point Cluster;
```

The cluster this node belongs to, identified by cluster grid coordinates.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Neighbours
```csharp
public readonly Dictionary<TKey, TValue> Neighbours;
```

Adjacent nodes reachable from this node, keyed by their grid position.

**Returns** \
[Dictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.Dictionary-2?view=net-7.0) \
#### P
```csharp
public readonly Point P;
```

The tile-space grid position of this node.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \
#### Weight
```csharp
public readonly int Weight;
```

Traversal cost of this node; higher values make paths through it less preferred.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### X
```csharp
public int X { get; }
```

The X tile coordinate of this node.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
#### Y
```csharp
public int Y { get; }
```

The Y tile coordinate of this node.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### HasNeighbour(Point)
```csharp
public bool HasNeighbour(Point p)
```

Returns `true` when this node has a direct edge to the node at position `p`.

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### PathTo(Point)
```csharp
public ImmutableDictionary<TKey, TValue> PathTo(Point p)
```

Returns the cached intra-cluster path from this node to node `p`.

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \

#### AddEdge(Point, ImmutableDictionary<TKey, TValue>, double)
```csharp
public void AddEdge(Point p, ImmutableDictionary<TKey, TValue> path, double cost)
```

Adds a directed edge to node `p` with the given intra-cluster path and traversal cost.

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \
`path` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
`cost` [double](https://learn.microsoft.com/en-us/dotnet/api/System.Double?view=net-7.0) \

#### RemoveEdge(Point)
```csharp
public void RemoveEdge(Point p)
```

Removes the edge from this node to node `p`.

**Parameters** \
`p` [Point](../../../Murder/Core/Geometry/Point.html) \



⚡