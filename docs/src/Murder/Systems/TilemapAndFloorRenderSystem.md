# TilemapAndFloorRenderSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class TilemapAndFloorRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Generic and all-around tilemap rendering system. Draws all tilemaps and floor tiles that are visible to the camera.

**Intent:** Renders all visible tilemap layers and floor tiles in the camera viewport, in a single pass.

**Use-case:** Include in worlds that contain tile-based rooms to draw both decorative tilemap layers and walkable floor tiles together. Use [TilemapNoFloorRenderSystem](Graphics/TilemapNoFloorRenderSystem.html) instead when the floor needs to be drawn in a separate pass (e.g. behind other layers). It is marked with `[EditorSystem]`, so it also runs inside the level editor's preview stage.

**Implements:** _[IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public TilemapAndFloorRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

For each room entity with a `TileGridComponent`, iterates every grid cell within the camera's safe bounds and draws its tileset tiles (and any additional tiles layered on top, such as reflections), followed by the room's floor tile — unless the cell is occluded by a tile flagged to occlude ground and the floor asset does not force always-drawing. Floor tile variation is picked deterministically per cell via a noise function, so the same world position always renders the same floor frame. Does nothing if the world has no unique `TilesetComponent` configured.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
