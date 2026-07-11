# GridCacheRenderSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class GridCacheRenderSystem : IReactiveSystem, ISystem
```

Listens for changes to `TileGridComponent` entities and rebuilds the per-tile render and collision cache for all tile grids in the world.

**Intent:** Keeps tile-grid cache data synchronized whenever a grid is added or modified, so that rendering and physics systems always read correct tile data.

**Use-case:** Must be included in any world with tile maps; it runs reactively so the cache is always current without requiring manual invalidation.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public GridCacheRenderSystem()
```

### ⭐ Methods
#### OnAdded(World, ImmutableArray<T>)
```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```
Called when new `TileGridComponent` entities are added; currently triggers no action (cache is rebuilt on modification).
**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)
```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```
Triggered when any watched `TileGridComponent` is modified; calls `OnTileGridModified` to rebuild all grid caches.
**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)
```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```
Called when `TileGridComponent` entities are removed; currently triggers no action.
**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnTileGridModified(World)
```csharp
public void OnTileGridModified(World world)
```

Static helper that walks all `TileGridComponent` entities in the world and rebuilds their internal `TileGrid` cache; can be called externally when tiles change outside the normal reactive flow.

**Parameters** \
`world` [World](../../Bang/World.html) \



⚡