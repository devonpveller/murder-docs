# AgentSpriteSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class AgentSpriteSystem : IMurderRenderSystem, IRenderSystem, ISystem, IFixedUpdateSystem
```

Renders the sprite for agent entities by selecting the correct directional animation prefix (idle vs. walk) based on the agent's impulse and facing angle, with support for animation overloads.

**Intent:** Drives the visual representation of agent entities by picking and drawing the correct directional Aseprite animation each frame.

**Use-case:** Required in any world with `AgentSpriteComponent` entities; it automatically switches between idle and walk animations and applies animation overrides set by other systems.

**Implements:** _[IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html), [IFixedUpdateSystem](../../Bang/Systems/IFixedUpdateSystem.html)_

### ⭐ Constructors
```csharp
public AgentSpriteSystem()
```

### ⭐ Methods
#### SetParticleWalk(World, Entity, bool)
```csharp
protected virtual void SetParticleWalk(World world, Entity e, bool isWalking)
```

Notifies the particle system to activate or deactivate the walk-particle effect on the given entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`isWalking` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### Draw(RenderContext, Context)
```csharp
public virtual void Draw(RenderContext render, Context context)
```

Selects the appropriate animation prefix from facing direction and movement state, then draws the agent sprite with y-sorting and any active animation overload.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

#### FixedUpdate(Context)
```csharp
public virtual void FixedUpdate(Context context)
```

Reserved for physics-tick processing on agent sprites; override to add per-physics-step logic.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \



⚡