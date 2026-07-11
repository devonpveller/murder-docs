# RouteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RouteComponent : IComponent
```

Holds the computed A* pathfinding route for an agent, represented as a dictionary of grid-cell waypoints.

**Intent:** Store the result of a pathfinding calculation so movement systems can follow the route step by step.

**Use-case:** Added by `CalculatePathfindSystem` when an agent needs to reach a target; movement systems read `Nodes`, `Initial`, and `Target` each frame to advance the agent along the path.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public RouteComponent(ImmutableDictionary<TKey, TValue> route, Point initial, Point target)
```

**Parameters** \
`route` [ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
`initial` [Point](../../Murder/Core/Geometry/Point.html) \
`target` [Point](../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties
#### Initial
```csharp
public readonly Point Initial;
```

Initial position cell.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \
#### Nodes
```csharp
public readonly ImmutableDictionary<TKey, TValue> Nodes;
```

Nodes path that the agent will make.

**Returns** \
[ImmutableDictionary\<TKey, TValue\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableDictionary-2?view=net-7.0) \
#### Target
```csharp
public readonly Point Target;
```

Goal position cell.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \


⚡