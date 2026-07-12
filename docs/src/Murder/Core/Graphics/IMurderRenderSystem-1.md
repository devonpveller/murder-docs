# IMurderRenderSystem\<T\>

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public abstract IMurderRenderSystem<T> : IMurderRenderSystem, IRenderSystem, ISystem
```

Main render system. This is used to draw on the screen and should not
have any update logic. This one includes a converter for your own
[RenderContext](../../../Murder/Core/Graphics/RenderContext.html) that you extended.

**Intent:** Generic variant of `IMurderRenderSystem` that automatically downcasts the `RenderContext` to your custom subclass, eliminating manual casts in every `Draw` implementation. `T` is constrained to `RenderContext` (or a subclass of it) in source, even though that constraint isn't reflected in the signature shown above.

**Use-case:** Extend `RenderContext` for your game (e.g. to add extra render passes/targets) and implement `IMurderRenderSystem<YourRenderContext>` on your custom render systems so that `Draw(T, Context)` receives your typed render context directly, instead of the base `RenderContext` that plain `IMurderRenderSystem` implementations get. The default-interface-method forwarder (`IMurderRenderSystem.Draw(RenderContext, Context)`) casts to `T` and calls your typed `Draw` automatically, so the engine's render loop — which only knows about `IMurderRenderSystem` — can still call your system without any special-casing. No system in the base Murder engine implements this generic form; it exists specifically for games that need a specialized render context.

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
