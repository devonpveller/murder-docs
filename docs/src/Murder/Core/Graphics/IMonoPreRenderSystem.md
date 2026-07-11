# IMonoPreRenderSystem

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public abstract IMonoPreRenderSystem : IRenderSystem, ISystem
```

System called right before rendering.

**Intent:** Marks an ECS system as a pre-render hook that runs before any `SpriteBatch.Begin()` call so it can set up render targets, clear buffers, or update shader parameters.

**Use-case:** Implement this interface when your system needs to manipulate GPU state (e.g., switch render targets, update shared uniform buffers) before the sprite-batch render pass begins.

**Implements:** _[IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Methods
#### BeforeDraw(Context)
```csharp
public abstract void BeforeDraw(Context context)
```

Called before rendering starts.
            This gets called before the SpriteBatch.Begin() and SpriteBatch.End() starts.

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \



⚡