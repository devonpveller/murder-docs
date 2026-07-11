# CustomDrawRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class CustomDrawRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Renders entities with a `CustomDrawComponent` by calling `ICustomDraw.Draw()` on their custom draw implementation.

**Intent:** Invokes custom-draw callbacks on entities that implement `ICustomDraw`.

**Use-case:** Use when an entity needs fully arbitrary rendering logic that doesn't fit a standard sprite or shape component.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors
```csharp
public CustomDrawRenderSystem()
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