# Edge

**Namespace:** Murder.Core.Ai \
**Assembly:** Murder.dll

```csharp
sealed struct Edge : IEquatable<T>
```

**Implements:** _[IEquatable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.IEquatable-1?view=net-7.0)_

A pair of tile positions used as the key when caching the entrance segments and pre-computed paths between two neighbouring clusters in the `HAAStar` abstract graph.

**Intent:** Identifies a border connection between two clusters. Equality is undirected — an edge from `A` to `B` is considered equal to the edge from `B` to `A`, since the underlying connection between the two clusters is the same either way it is traversed.

**Use-case:** Not used directly in gameplay; `HAAStar` uses `Edge` internally as a dictionary key while abstracting the maze into clusters and while building the graph of nodes and their connecting paths.

### ⭐ Constructors

```csharp
public Edge(Point a, Point b)
```

Creates an edge connecting tile positions `a` and `b`.

**Parameters** \
`a` [Point](../../../Murder/Core/Geometry/Point.html) \
`b` [Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties

#### A

```csharp
public readonly Point A;
```

One endpoint of the edge.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

#### B

```csharp
public readonly Point B;
```

The other endpoint of the edge.

**Returns** \
[Point](../../../Murder/Core/Geometry/Point.html) \

### ⭐ Methods

#### Equals(Object)

```csharp
public virtual bool Equals(Object obj)
```

Returns `true` if `obj` is an `Edge` connecting the same two points, regardless of direction.

**Parameters** \
`obj` [Object](https://learn.microsoft.com/en-us/dotnet/api/System.Object?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Equals(Edge)

```csharp
public bool Equals(Edge other)
```

Returns `true` if both edges connect the same two points, regardless of direction.

**Parameters** \
`other` [Edge](../../../Murder/Core/Ai/Edge.html) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### GetHashCode()

```csharp
public virtual int GetHashCode()
```

Returns a hash code derived from both endpoints, consistent with the undirected equality of `Equals`.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

⚡
