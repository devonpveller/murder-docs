# RectangleRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class RectangleRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Draws a filled or outlined rectangle for every entity with a [DrawRectangleComponent](../../../Murder/Components/DrawRectangleComponent.html), sized to the entity's [ColliderComponent](../../../Murder/Components/ColliderComponent.html) bounding box when present, or a single grid cell otherwise.

**Intent:** Draws flat-colored boxes for entities that don't need a full sprite.

**Use-case:** Use for debug overlays, placeholder visuals, or any entity that just needs a simple filled or outlined rectangle at its position — `DrawRectangleComponent.SmoothingLayers`/`SmoothSize` can add a soft faded edge to filled rectangles for a glow-like effect. It is marked with `[EditorSystem]`, so it also runs inside the level editor's preview stage.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public RectangleRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

Draws each filtered entity's rectangle at its global position, applying the entity's [AlphaComponent](../../../Murder/Components/AlphaComponent.html) (skipping fully-transparent entities), and either filling it — with optional soft smoothing layers — or drawing just its outline, depending on `DrawRectangleComponent.Fill`.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
