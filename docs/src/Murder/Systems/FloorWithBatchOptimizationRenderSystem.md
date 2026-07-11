# FloorWithBatchOptimizationRenderSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class FloorWithBatchOptimizationRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem, IExitSystem
```

Much, much faster than the regular Tilemap system, especially when you have many layers of tiles.
            Be careful because this WILL fail at higher resolutions!

**Intent:** Provides high-performance tilemap floor rendering by pre-baking tile chunks into a runtime atlas and drawing them in a single batch per visible region.

**Use-case:** Use instead of `TilemapAndFloorRenderSystem` when you have many tile layers and performance is a concern; note the resolution limitation documented in the source.

**Implements:** _[IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IExitSystem](../../Bang/Systems/IExitSystem.html)_

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



⚡