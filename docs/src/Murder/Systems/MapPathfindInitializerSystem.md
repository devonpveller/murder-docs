# MapPathfindInitializerSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class MapPathfindInitializerSystem : IStartupSystem, ISystem
```

Reads per-cell properties from a `PathfindGridComponent` entity at startup and applies occupancy and weight data to the world's `MapComponent`.

**Intent:** Seeds the navigation map with hand-authored cell weights and collision masks defined in a `PathfindGridComponent` asset.

**Use-case:** Place a `PathfindGridComponent` entity in a scene to control per-cell pathfinding cost or to block specific cells from navigation.

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