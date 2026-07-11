# IMurderRenderSystem

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public abstract IMurderRenderSystem : IRenderSystem, ISystem
```

Main render system. This is used to draw on the screen and should not 
            have any update logic.

**Intent:** The primary interface for ECS systems that render game entities; provides access to the full `RenderContext` and the component query `Context`.

**Use-case:** Implement `Draw(RenderContext, Context)` in any system that needs to issue sprite or primitive draw calls each frame; the engine calls all `IMurderRenderSystem` implementations once per frame after simulation.

**Implements:** _[IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### Draw(RenderContext, Context)
```csharp
public abstract void Draw(RenderContext render, Context context)
```

Called on rendering.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡