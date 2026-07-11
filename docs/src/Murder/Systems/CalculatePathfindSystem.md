# CalculatePathfindSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class CalculatePathfindSystem : IStartupSystem, ISystem, IReactiveSystem
```

Initializes the world's `HAAStarPathfindComponent` on startup and recalculates a navigation path for any entity whose `PathfindComponent` is added or changed.

**Intent:** Creates and maintains HAAstar pathfinding data for each entity that requests navigation, reacting to target changes and map state.

**Use-case:** Include in any world that uses pathfinding; it must run alongside `MapInitializerSystem` so a valid map exists before paths are computed.

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)_

### ⭐ Constructors
```csharp
public CalculatePathfindSystem()
```

### ⭐ Properties
#### LineOfSightCollisionMask
```csharp
public static const int LineOfSightCollisionMask;
```

The combined collision layer mask used for line-of-sight checks during path calculation; defaults to BLOCK_VISION, SOLID, HOLE, and CARVE layers.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
### ⭐ Methods
#### OnAdded(World, ImmutableArray<T>)
```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Calculates an initial path for each newly added entity that has a `PathfindComponent`, using the current world map.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)
```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Re-calculates the path for each entity whose `PathfindComponent` has changed; skips recalculation if the target cell has not moved.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Clears the route component and resets friction on entities that no longer have a `PathfindComponent`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Start(Context)
```csharp
public virtual void Start(Context context)
```

Creates the world-unique `HAAStarPathfindComponent` entity and seeds it with the current map's dimensions and cell data.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡