# AnimationCompleteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationCompleteComponent : IComponent
```

The Aseprite component in this entity completed it's animation

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Signals that the entity's current sprite animation has finished playing its last frame. Marked `[DoNotPersistOnSave]` and `[RuntimeOnly]`, since it is purely a transient per-frame flag and must never be written to a save file.

**Use-case:** Systems that need to react to animation completion (e.g., destroying a one-shot effect, chaining to the next `AnimationOverloadComponent` clip, or transitioning a state machine) filter for this component being present on an entity, then typically remove it (or the entity) once handled so the signal is not processed again on the next frame.

### ⭐ Constructors

```csharp
public AnimationCompleteComponent()
```

⚡
