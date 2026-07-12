# MapInitializerSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class MapInitializerSystem : IStartupSystem, ISystem
```

Filtered to entities with a `TileGridComponent`. Calculates map bounds from every `TileGridComponent`/`RoomComponent` pair found in the world at startup, creates the world-unique map entity, stamps down floor and tileset collision data for each grid, and marks every cell outside of a known room as permanently solid.

**Intent:** Bootstraps the world's `Map` on scene load: it works out how large the map needs to be from the tile grids placed in the scene, creates the `MapComponent` entity that every other grid-aware system (`MapPathfindInitializerSystem`, `MapCarveCollisionSystem`, `CalculatePathfindSystem`, `QuadtreeCalculatorSystem`, ...) depends on, and burns each room's floor/tileset collision layers into the map so static collision and pathfinding data is ready before gameplay systems run. The two protected hooks (`InitializeRoom`, `InitializeTile`) exist purely so a game can subclass this system and layer in extra per-room or per-tile setup (e.g. spawning decorations, registering custom gameplay data keyed by tile) without having to reimplement the bounds/collision logic.

**Use-case:** Include exactly once per scene that uses tile maps (`TileGridComponent` entities); it must run before any system that reads `MapComponent`. If a game needs extra per-tile or per-room initialization, subclass `MapInitializerSystem` and override `InitializeRoom`/`InitializeTile` rather than writing a second startup system.

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public MapInitializerSystem()
```

### ⭐ Methods

#### InitializeRoom(Entity, TileGrid, RoomComponent)

```csharp
protected virtual void InitializeRoom(Entity e, TileGrid grid, RoomComponent room)
```

No-op hook called once per grid entity after its tiles have been stamped into the map. Override this to run per-room setup, such as tagging the room entity with extra gameplay components derived from its `RoomComponent` (e.g. its floor asset or ambient lighting).

**Parameters** \
`e` [Entity](../../Bang/Entities/Entity.html) \
`grid` [TileGrid](../../Murder/Core/TileGrid.html) \
`room` [RoomComponent](../../Murder/Components/RoomComponent.html) \

#### InitializeTile(Map, int, int, ITileProperties?)

```csharp
protected virtual void InitializeTile(Map map, int x, int y, ITileProperties? iProperties)
```

No-op hook called for each cell that has resolved `ITileProperties` (from either the room's `FloorAsset` or a solid tileset asset) while the map is being populated. Override to apply custom per-cell data — for example, converting tile properties into gameplay flags, hazards, or triggers stored elsewhere in the map/world.

**Parameters** \
`map` [Map](../../Murder/Core/Map.html) \
`x` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`y` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`iProperties` [ITileProperties](../../Murder/Core/ITileProperties.html) \

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

Computes the map's origin and dimensions from the bounds of every `TileGridComponent` in the world (defaulting to a minimum 25x25 area), creates the map entity via `Entity.SetMap`, then — if a unique tileset asset is registered — walks every grid's cells, marking solid tiles as statically occupied with the matching `TilesetAsset.CollisionLayer` and invoking `InitializeTile`/`InitializeRoom` for each cell/grid. Finally, any map cell that does not fall inside any known grid's bounds is marked solid, so pathfinding and physics treat the area outside authored rooms as an impassable wall.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
