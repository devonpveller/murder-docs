# TilemapAndFloorRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class TilemapAndFloorRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Generic and all-around tilemap rendering system. Draws all tilesmaps and floor tiles that are visible to the camera.

**Intent:** Renders all visible tilemap layers and floor tiles in the camera viewport.

**Use-case:** Include in worlds that contain tile-based rooms to draw both decorative tilemap layers and walkable floor tiles.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public TilemapAndFloorRenderSystem()
```

### ⭐ Methods
#### Draw(RenderContext, Context)
```csharp
public virtual void Draw(RenderContext render, Context context)
```

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡