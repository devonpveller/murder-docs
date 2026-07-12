# FloorWithBatchOptimizationRenderSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class FloorWithBatchOptimizationRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem, IExitSystem, IReactiveSystem
```

Much, much faster than the regular Tilemap system, especially when you have many layers of tiles.
Be careful because this WILL fail at higher resolutions!

**Intent:** Provides high-performance tilemap floor rendering by pre-baking `TileGridComponent` chunks (tiles + `FloorAsset` ground textures) into a static-size runtime atlas (`RuntimeAtlas`) and redrawing already-baked chunks as single textured quads, instead of re-issuing per-tile draw calls every frame like `TilemapAndFloorRenderSystem` does.

**Use-case:** Use instead of `TilemapAndFloorRenderSystem` when you have many tile layers and performance is a concern; note the resolution limitation documented in the source (the fixed-size 4096px atlas can run out of room at very high output resolutions / very large visible areas). The atlas and chunk cache are process-wide `static` state shared by all instances, and are cleared whenever a watched `TileGridComponent` is modified or the world exits.

**Implements:** _[IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html), [IReactiveSystem](../../Bang/Systems/IReactiveSystem.html)_

### ⭐ Constructors

```csharp
public FloorWithBatchOptimizationRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

Determines which tile chunks fall within the camera bounds and renders each visible chunk from the cached runtime atlas.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

#### Exit(Context)

```csharp
public virtual void Exit(Context context)
```

Clears the chunk cache and the tileset asset cache when the world exits so they are rebuilt fresh on the next load.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

No-op; newly added `TileGridComponent` entities are simply picked up the next time `Draw` rebuilds a chunk that covers them, no reactive work is needed on add.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Invalidates every cached chunk and the tileset asset cache whenever a watched `TileGridComponent` changes (e.g. a tile is painted or a room's floor asset changes), forcing all visible chunks to be re-baked into the atlas on the next `Draw`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

No-op; a removed `TileGridComponent` simply stops contributing to future chunk rebuilds, and stale baked chunks are cleared the next time something changes rather than on removal itself.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
