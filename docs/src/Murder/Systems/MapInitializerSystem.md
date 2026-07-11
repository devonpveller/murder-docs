# MapInitializerSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class MapInitializerSystem : IStartupSystem, ISystem
```

Calculates map bounds from all `TileGridComponent` entities at startup, creates the `MapComponent` entity, and initializes per-cell tile properties.

**Intent:** Bootstraps the world map on scene load by collecting tile-grid extents and populating the map entity used by physics and pathfinding.

**Use-case:** Include once per scene that uses tile maps; must run before systems that read `MapComponent` (e.g., `CalculatePathfindSystem`, `MapCarveCollisionSystem`).

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public MapInitializerSystem()
```

### ⭐ Methods
#### InitializeTile(Map, int, int, ITileProperties)
```csharp
protected virtual void InitializeTile(Map map, int x, int y, ITileProperties iProperties)
```

Called for each tile cell during startup; override to apply custom collision masks or data properties to individual tiles based on their `ITileProperties`.

**Parameters** \
`map` [Map](../../Murder/Core/Map.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`iProperties` [ITileProperties](../../Murder/Core/ITileProperties.html) \

#### Start(Context)
```csharp
public virtual void Start(Context context)
```

Calculates the bounding rectangle from all tile grids, creates the `MapComponent` entity, and calls `InitializeTile` for each occupied cell.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡