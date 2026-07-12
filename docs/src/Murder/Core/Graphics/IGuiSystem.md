# IGuiSystem

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public abstract IGuiSystem : IRenderSystem, ISystem
```

System for rendering Gui entities.

**Intent:** Marks an ECS system as an ImGui overlay renderer, letting it draw windows/widgets/gizmos in a dedicated pass that runs after (and independently of) world-space rendering.

**Use-case:** Implement this on a system that needs to draw ImGui content — most implementers are editor tools (inspectors, gizmos, selection outlines), but it is also used by runtime diagnostics such as `ConsoleSystem`'s in-game debug console. `MonoWorld.DrawGui(RenderContext)` calls `DrawGui` on every active `IGuiSystem` in render order; this is only actually invoked when the running `Game` overrides `DrawImGui` to call `Scene.DrawGui()` (the editor's `Architect` does this every frame — a shipped game only gets this pass if its own `Game` subclass does the same).

**Implements:** _[IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Methods

#### DrawGui(RenderContext, Context)

```csharp
public abstract void DrawGui(RenderContext render, Context context)
```

Called once per GUI pass (see `MonoWorld.DrawGui`) so this system can submit ImGui draw calls for its filtered entities; implementations typically call into `ImGui.*` APIs here rather than drawing sprites via `render`.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
