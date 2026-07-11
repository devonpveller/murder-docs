# DoNotLoopComponent

**Namespace:** Murder.Components.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct DoNotLoopComponent : IComponent
```

Marker component that instructs the animation system to play the entity's current animation only once instead of looping.

**Intent:** Prevent an animation from repeating after it completes its final frame.

**Use-case:** Attach to an entity (e.g. a one-shot explosion or death animation) before starting the animation so the sprite freezes on the last frame or triggers a completion callback instead of restarting.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_



⚡