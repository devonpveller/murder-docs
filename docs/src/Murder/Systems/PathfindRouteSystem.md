# PathfindRouteSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class PathfindRouteSystem : IFixedUpdateSystem, ISystem, IReactiveSystem
```

Filtered and watched on `RouteComponent`. Consumes the route produced by `CalculatePathfindSystem` and issues step-by-step `MoveToComponent` waypoints, so the agent walks the pre-computed path node by node instead of aiming straight at the final destination.

**Intent:** Translates a static route graph (a dictionary of grid-cell nodes) into sequential per-cell movement targets so an agent follows the calculated pathfinding route one waypoint at a time. It also detects when the agent has fully reached the pathfind target and cleans up the pathfinding-related components.

**Use-case:** Include together with `CalculatePathfindSystem` in AI worlds; this system handles movement execution once a route has been computed, by driving the same `MoveToComponent` that agent-movement systems consume.

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

For each routed entity, checks whether it has reached the cell it was last aimed at. If so: when that cell is the final `PathfindComponent.Target`, it snaps the entity's `MoveToComponent` to the exact target, removes `PathfindComponent`/`RouteComponent`, and marks `PathfindStatusFlags.PathComplete`; otherwise it looks up the next node in the route for the entity's current cell (falling back to the closest known route node if the entity drifted off-route) and issues a `MoveToComponent` targeting that node's cell center.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

When a `RouteComponent` is added to an entity, immediately issues a `MoveToComponent` targeting the route's initial node, so the entity starts moving toward the first waypoint right away instead of waiting for the next `FixedUpdate` pass to notice the new route.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

When an entity's `RouteComponent` is replaced with a new route (e.g. because the pathfind target changed), re-targets the entity's `MoveToComponent` to the new route's initial node, exactly as `OnAdded` does.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

No-op; when `RouteComponent` is removed, the entity has either already arrived at its destination (handled in `FixedUpdate`) or been rerouted by `CalculatePathfindSystem`, so no extra cleanup is needed here.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
