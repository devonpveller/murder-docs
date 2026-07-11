# SpriteRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class SpriteRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem, IFixedUpdateSystem
```

The main sprite renderer — renders `SpriteComponent` entities with support for animations, flipping, and draw order.

**Intent:** Renders all standard sprite entities each frame.

**Use-case:** The primary rendering system for game entities; include in every world that displays sprite-based characters, objects, or effects.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html), [IFixedUpdateSystem](../../../Bang/Systems/IFixedUpdateSystem.html)_

### ⭐ Constructors
```csharp
public SpriteRenderSystem()
```

### ⭐ Methods
#### Draw(RenderContext, Context)
```csharp
public virtual void Draw(RenderContext render, Context context)
```

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \

#### FixedUpdate(Context)
```csharp
public virtual void FixedUpdate(Context context)
```

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡