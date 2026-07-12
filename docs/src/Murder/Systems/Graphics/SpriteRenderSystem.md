# SpriteRenderSystem

**Namespace:** Murder.Systems.Graphics \
**Assembly:** Murder.dll

```csharp
public class SpriteRenderSystem : IMurderRenderSystem, IRenderSystem, ISystem
```

The main sprite renderer: draws every on-camera entity with a [SpriteComponent](../../../Murder/Components/SpriteComponent.html) (skipping ones flagged invisible, three-sliced, or force-drawn-at-ratio, since those are handled by dedicated systems) applying flipping, parallax, rotation from facing/`RotationComponent`, inherited alpha/tint, flash-blend, sprite-batch targeting, animation overloads, clipping, offsets, outline highlighting, and Y-sorting. It also advances the sprite's animation state each frame, triggers any Aseprite animation events for the frame drawn, chains to the next animation in a sequence when one completes, and dispatches animation-complete handling (looping, destruction, etc.).

**Intent:** Renders all standard on-camera sprite entities each frame, including their animation, flipping, tinting, and draw-order logic.

**Use-case:** The primary rendering system for game entities; include in every world that displays sprite-based characters, objects, or effects. Entities are filtered on [InCameraComponent](../../../Murder/Components/InCameraComponent.html) so only what the camera can currently see is processed — a companion system (e.g. `DynamicInCameraSystem`) is responsible for keeping that component up to date.

**Implements:** _[IMurderRenderSystem](../../../Murder/Core/Graphics/IMurderRenderSystem.html), [IRenderSystem](../../../Bang/Systems/IRenderSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public SpriteRenderSystem()
```

### ⭐ Methods

#### Draw(RenderContext, Context)

```csharp
public virtual void Draw(RenderContext render, Context context)
```

Resolves and draws the current animation frame for every filtered entity: computes its final render position (parallax, clip/offset adjustments, vertical position), rotation, flip, inherited tint/alpha, blend mode and target sprite batch, then submits the frame to the batch with Y-sorting. Afterwards, triggers any animation events for the frame, caches the rendered sprite state for other systems to query, and handles what happens when the animation completes (chaining to a baked-in next animation, applying an animation overload's completion, or the entity's normal complete-animation behavior).

**Parameters** \
`render` [RenderContext](../../../Murder/Core/Graphics/RenderContext.html) \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
