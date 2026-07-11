# PathfindComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PathfindComponent : IComponent
```

Requests that the pathfinding system calculate a route from the entity's current position to `Target` using the specified algorithm.

**Intent:** Initiate pathfinding for an agent by specifying the destination and the algorithm to use (e.g. A* or HA*).

**Use-case:** Add to an agent entity with the desired `Target` world-space position and `Algorithm`; the `CalculatePathfindSystem` processes this component and replaces it with a waypoint route component once a path is found.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public PathfindComponent(Vector2& target, PathfindAlgorithmKind algorithm)
```

**Parameters** \
`target` [Vector2&](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`algorithm` [PathfindAlgorithmKind](../../Murder/Core/Ai/PathfindAlgorithmKind.html) \

### ⭐ Properties
#### Algorithm
```csharp
public readonly PathfindAlgorithmKind Algorithm;
```

Pathfinding algorithm to use when computing the route to `Target`.

**Returns** \
[PathfindAlgorithmKind](../../Murder/Core/Ai/PathfindAlgorithmKind.html) \
#### Target
```csharp
public readonly Vector2 Target;
```

World-space destination position the pathfinding algorithm should find a route to.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \


⚡