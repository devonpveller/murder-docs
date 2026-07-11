# SpriteNineSliceRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class SpriteNineSliceRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Renders entities with a `NineSliceComponent` using nine-slice scaling.

**Intent:** Draws nine-slice scaled sprites for entities with `NineSliceComponent`.

**Use-case:** Use for UI panels, dialogue boxes, and other resizable elements that must scale without distorting corners.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public SpriteNineSliceRenderSystem()
```

### ⭐ Methods
#### Draw(RenderContext, Context)
```csharp
public virtual void Draw(RenderContext render, Context context)
```

This draws an sprite nine slice component.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡