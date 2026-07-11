# SpriteThreeSliceRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class SpriteThreeSliceRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Renders entities with a `ThreeSliceComponent` using three-slice horizontal or vertical scaling.

**Intent:** Draws three-slice scaled sprites for entities with `ThreeSliceComponent`.

**Use-case:** Use for health bars, progress bars, and other one-axis-resizable UI or game elements.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public SpriteThreeSliceRenderSystem()
```

### ⭐ Methods
#### Draw(RenderContext, Context)
```csharp
public virtual void Draw(RenderContext render, Context context)
```

This draws an aseprite three slice component.
            TODO: Support animations?

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡