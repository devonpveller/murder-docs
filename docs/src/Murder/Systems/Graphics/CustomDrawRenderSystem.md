# CustomDrawRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class CustomDrawRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Renders every entity that carries a [CustomDrawComponent](../../../Murder/Components/CustomDrawComponent.html) by invoking that component's `Draw` delegate with the current [RenderContext](../../../Murder/Core/Graphics/RenderContext.html). `CustomDrawComponent` is a runtime-only component (never persisted to save data) that holds an `Action<RenderContext>`, so this system is the escape hatch for visuals that don't fit a sprite, rectangle, or tilemap component — gizmos, procedural debug shapes, or any other code-driven drawing that would otherwise need a dedicated system.

**Intent:** Lets code attach arbitrary, per-frame drawing logic to an entity without writing a bespoke render system.

**Use-case:** Use when an entity needs fully custom rendering — e.g., editor gizmos, debug visualizations, or procedurally generated visuals — that cannot be expressed with `SpriteComponent`, `DrawRectangleComponent`, or the other standard render components. It is marked with `[EditorSystem]`, so it also runs inside the level editor's preview stage, not just in normal gameplay.

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

Calls `CustomDrawComponent.Draw` on every filtered entity, passing along the active render context so each delegate can submit draws to whichever batch it needs.

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
