# AgentSpriteSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class AgentSpriteSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

Renders the sprite for agent entities by selecting the correct directional animation prefix (idle vs. walk) based on the agent's impulse and facing angle, with support for animation overloads, tint/alpha/scale modifiers, sprite blending, y-sorting, and walk-particle triggering.

**Intent:** Drives the visual representation of agent entities by picking and drawing the correct directional Aseprite animation each frame, translating movement state (`AgentImpulseComponent`), facing (`FacingComponent`) and any active `AnimationOverloadComponent` into a concrete sprite frame, position, flip and blend to hand off to `RenderServices.DrawSprite`.

**Use-case:** Required in any world with `AgentSpriteComponent` entities that also carry `PositionComponent`, `FacingComponent` and `InCameraComponent` (only entities currently in the camera view are drawn). It automatically switches between idle and walk animation prefixes, applies animation overrides set by other systems (e.g. one-shot spell-cast animations via `AnimationOverloadComponent`), toggles the entity's walk particle child on and off, and skips entities carrying `InvisibleComponent`.

**Implements:** _[IMurderRenderSystem](../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../Bang/Systems/IRenderSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public AgentSpriteSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

The main per-frame entry point. For every matching entity it resolves the `SpriteAsset` referenced by `AgentSpriteComponent`, computes the render position (accounting for `VerticalPositionComponent`, sprite offset/clipping), picks the idle or walk prefix, resolves the directional suffix from the facing angle, applies any active `AnimationOverloadComponent`/`AnimationSpeedOverload`, computes color/blend/scale from `AlphaComponent`, `TintComponent`, `SpriteBlendComponent` and `ScaleComponent`, then draws the sprite via `RenderServices.DrawSprite`, fires animation events, updates the entity's `RenderedSpriteCache`, and calls `AfterDraw` and `SetParticleWalk` as part of the pipeline.

**Parameters** \
`render` [RenderContext](../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../Bang/Contexts/Context.html) \

#### AfterDraw(Batch2D, Entity, Vector2, float, DrawInfo, AnimationInfo, SpriteAsset)

```csharp
protected virtual void AfterDraw(Batch2D batch, Entity e, Vector2 position, float ySortOffsetRaw, DrawInfo drawInfo, AnimationInfo animationInfo, SpriteAsset spriteAsset)
```

Empty extension hook called immediately after the agent's sprite has been drawn each frame, with the exact batch, position, draw parameters and resolved animation/sprite that were used. Override it in a derived render system to layer extra drawing on top of the base agent sprite (e.g. equipment overlays, status icons) without duplicating the selection logic in `Draw`.

**Parameters** \
`batch` [Batch2D](../../Murder/Core/Graphics/Batch2D.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`position` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`ySortOffsetRaw` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`drawInfo` [DrawInfo](../../Murder/Core/Graphics/DrawInfo.html) \
`animationInfo` [AnimationInfo](../../Murder/Core/Graphics/AnimationInfo.html) \
`spriteAsset` [SpriteAsset](../../Murder/Assets/Graphics/SpriteAsset.html) \

#### SetParticleWalk(World, Entity, bool)

```csharp
protected virtual void SetParticleWalk(World world, Entity e, bool isWalking)
```

Looks up the entity's child named `"Particle"` and enables or disables its particle system component so that a walk-dust/footstep effect only plays while the agent is actually moving. Called once per frame from `Draw` with the result of the movement check.

**Parameters** \
`world` [World](../../Bang/World.html) \
`e` [Entity](../../Bang/Entities/Entity.html) \
`isWalking` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

⚡
