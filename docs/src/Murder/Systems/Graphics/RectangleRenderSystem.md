# RectangleRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class RectangleRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Renders entities with a `DrawRectangleComponent` as solid or outlined rectangles.

**Intent:** Draws filled or outlined rectangles for entities with `DrawRectangleComponent`.

**Use-case:** Use for debug overlays, UI panels, or any entity that needs a simple rectangle drawn at its position.

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

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡