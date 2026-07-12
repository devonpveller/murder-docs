# TilemapNoFloorRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class TilemapNoFloorRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Draws only the tilemap and not the floor. Will still draw additional tiles layered on top of floor tiles, like reflections.

**Intent:** Renders all visible tilemap layers within the camera viewport, skipping the plain floor-tile pass while still drawing floor-tile extras such as reflections.

**Use-case:** Use instead of [TilemapAndFloorRenderSystem](../TilemapAndFloorRenderSystem.html) when the floor tile geometry needs to be rendered separately, e.g. behind other layers via a different draw pass. Both systems read from the world's unique `TilesetComponent` and the room entity's `TileGridComponent`, and do nothing if either is missing.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public TilemapNoFloorRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

For each room entity with a `TileGridComponent`, draws every tileset layer within the camera's safe grid bounds except the plain floor layer itself (a layer that targets the floor batch and has no additional tiles is skipped entirely), plus any additional tiles layered on top such as reflections.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
