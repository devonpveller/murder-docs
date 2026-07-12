# MapPathfindInitializerSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class MapPathfindInitializerSystem : IStartupSystem, ISystem
```

Filtered to entities with a `PathfindGridComponent` (a world-unique component). Reads every per-cell override from it at startup and applies the corresponding occupancy/collision mask and pathfinding weight to the world's `MapComponent`.

**Intent:** Seeds the navigation map with hand-authored cell weights and collision masks defined in a `PathfindGridComponent`, letting level designers fine-tune specific cells (mark difficult terrain as more costly, or block particular tiles from navigation) without editing the underlying tileset.

**Use-case:** Place a `PathfindGridComponent` entity in a scene (typically authored through the level editor) to control per-cell pathfinding cost or to block specific cells from navigation. This system must run after `MapInitializerSystem`, since it writes into a `MapComponent` that is expected to already exist; if no map exists yet, or no `PathfindGridComponent` entity is present, `Start` does nothing.

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public MapPathfindInitializerSystem()
```

### ⭐ Methods

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

Reads the cell properties from the scene's `PathfindGridComponent` and writes occupancy and weight values into the world map.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
