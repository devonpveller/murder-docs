# IMurderRenderSystem\<T\>

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public abstract IMurderRenderSystem<T> : IMurderRenderSystem, IRenderSystem, ISystem
```

Main render system. This is used to draw on the screen and should not 
            have any update logic. This one includes a converter for your own
            [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) that you extended.

**Intent:** Generic variant of `IMurderRenderSystem` that automatically downcasts the `RenderContext` to your custom subclass, eliminating manual casts in every `Draw` implementation.

**Use-case:** Extend `RenderContext` for your game and implement `IMurderRenderSystem<YourRenderContext>` so that `Draw(T, Context)` receives your typed render context directly.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### Draw(T, Context)
```csharp
public abstract void Draw(T render, Context context)
```

Called each frame with the typed `RenderContext` subclass `T` and the component query context; implement this to issue draw calls for the system's entities.

**Parameters** \
`render` [T](../../../) \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡