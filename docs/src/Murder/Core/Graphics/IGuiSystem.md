# IGuiSystem

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public abstract IGuiSystem : IRenderSystem, ISystem
```

System for rendering Gui entities.

**Intent:** Marks an ECS system as an ImGui overlay renderer so the engine calls it during the editor's GUI pass.

**Use-case:** Implement this interface in editor-tool systems that need to draw ImGui windows, widgets, or gizmos on top of the game viewport.

**Implements:** _[IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### DrawGui(RenderContext, Context)
```csharp
public abstract void DrawGui(RenderContext render, Context context)
```

Called each editor frame to submit ImGui draw commands for this system's entities.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡