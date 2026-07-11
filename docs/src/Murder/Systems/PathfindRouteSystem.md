# PathfindRouteSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class PathfindRouteSystem : IFixedUpdateSystem, ISystem, IReactiveSystem
```

Consumes the `RouteComponent` produced by `CalculatePathfindSystem` and issues step-by-step `MoveToComponent` targets so the agent walks the pre-computed path node by node.

**Intent:** Translates a static route graph into sequential per-cell movement targets so an agent follows the calculated pathfinding route at runtime.

**Use-case:** Include together with `CalculatePathfindSystem` in AI worlds; this system handles movement execution once a route has been computed.

**Implements:** _[IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)_

### ⭐ Constructors
```csharp
public PathfindRouteSystem()
```

### ⭐ Methods
#### FixedUpdate(Context)
```csharp
public virtual void FixedUpdate(Context context)
```
Checks each entity's current cell against its pre-computed route and issues the next `MoveToComponent` waypoint; clears the route when the destination is reached.
**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

No-op stub; route following begins in the next `FixedUpdate` tick.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

No-op stub; route changes are consumed in `FixedUpdate`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Called when a route is removed; no action needed as the entity has already arrived or been rerouted.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \



⚡