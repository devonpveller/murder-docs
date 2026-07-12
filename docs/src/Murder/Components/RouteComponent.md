# RouteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RouteComponent : IComponent
```

Holds the computed pathfinding route for an agent, mapping each grid cell along the way to the next cell it should step into.

**Intent:** Store the result of a pathfinding calculation (produced by `Map.FindPath`) so movement systems can advance the agent one cell at a time without recomputing the path every frame.

**Use-case:** `CalculatePathfindSystem` computes a path whenever a `PathfindComponent` is added or its target changes, then attaches `RouteComponent` to the entity via `Entity.SetRoute`. `PathfindRouteSystem` (filtering on `RouteComponent`) reads `Nodes` each fixed update to look up the next cell from the agent's current cell and issues a `MoveToComponent` toward it; if the agent ever falls off the recorded route, it falls back to the closest known node. The type carries `[Requires(typeof(PathfindComponent))]`, so it can only be attached to entities that also have a `PathfindComponent`, and `[DoNotPersistOnSave(exceptIfComponentIsPresent: typeof(PersistPathfindComponent))]`, so by default an in-progress route is *not* written to save files — it is only persisted when the entity also carries `PersistPathfindComponent`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public RouteComponent(ComplexDictionary<TKey, TValue> route, Point initial, Point target)
```

Wraps an already-computed route (as returned by `Map.FindPath`) together with the initial and target cells it connects.

**Parameters** \
`route` [ComplexDictionary\<TKey, TValue\>](../../Murder/Serialization/ComplexDictionary-2.html) \
`initial` [Point](../../Murder/Core/Geometry/Point.html) \
`target` [Point](../../Murder/Core/Geometry/Point.html) \

### ⭐ Properties

#### Initial

```csharp
public readonly Point Initial;
```

Grid cell the agent started this route from. `PathfindRouteSystem` uses it as the lookup key into `Nodes` right after the route is (re)computed, to find the first cell to move toward.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

#### Nodes

```csharp
public readonly ComplexDictionary<TKey, TValue> Nodes;
```

Maps each grid cell on the path to the next cell the agent should move into on its way to `Target`. `PathfindRouteSystem` walks this dictionary one cell at a time each fixed update, using the entity's current cell as the key, until it reaches `Target`.

**Returns** \
[ComplexDictionary\<TKey, TValue\>](../../Murder/Serialization/ComplexDictionary-2.html) \

#### Target

```csharp
public readonly Point Target;
```

Goal position cell.

**Returns** \
[Point](../../Murder/Core/Geometry/Point.html) \

⚡
