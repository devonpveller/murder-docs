# ParticleRendererSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class ParticleRendererSystem : IStartupSystem, ISystem, IMurderRenderSystem, IRenderSystem, IUpdateSystem
```

Manages the world-unique `ParticleSystemWorldTrackerComponent`, advances all particle simulations each update, and renders every active particle to its designated sprite batch.

**Intent:** The central system for particle effects — it owns the tracker singleton, steps all simulations, and issues draw calls for every visible particle each frame.

**Use-case:** Required in any world that uses particle systems; include once and configure individual emitters via `ParticleSystemComponent` on entities.

**Implements:** _[IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [IUpdateSystem](../../Bang/Systems/IUpdateSystem.html)_

### ⭐ Constructors

```csharp
public ParticleRendererSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

Iterates all active particle trackers and draws each particle's texture, color, scale, and rotation to the appropriate sprite batch.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

Creates the world-unique `ParticleSystemWorldTrackerComponent` entity that all particle systems register with, guarding against double-initialization if the entity was somehow already added.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### Update(Context)

```csharp
public virtual void Update(Context context)
```

Advances all tracked particle simulations by one game tick, applying lifetime, velocity, and fade curves to each particle.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

⚡
