# DoNotLoopComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct DoNotLoopComponent : IComponent
```

Marker component that instructs `SpriteRenderSystem` to play the entity's current animation only once instead of looping.

**Intent:** Prevent an animation from repeating after it completes its final frame. `SpriteRenderSystem` factors `!e.HasDoNotLoop()` directly into the `AnimationInfo.Loop` flag it builds every frame, so as long as this component is present the animation holds on its last frame instead of restarting from frame zero.

**Use-case:** You rarely need to add this by hand — `EntityServices.PlaySpriteAnimationOnce(entity, animation)` is the standard entry point: it plays the given animation and calls `entity.SetDoNotLoop()` for you, while `EntityServices.TryPlaySpriteAnimation` removes it again before queuing a new (looping) sequence. Use it directly only if you're driving `SpriteComponent` manually and want a one-shot animation (e.g. a death or hit animation) that should hold on its final frame rather than loop.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

⚡
