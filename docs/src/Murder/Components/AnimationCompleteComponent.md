# AnimationCompleteComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationCompleteComponent : IComponent
```

The Aseprite component in this entity completed it's animation

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Signals that the entity's current sprite animation has finished playing its last frame.

**Use-case:** Systems that need to react to animation completion (e.g., destroying a one-shot effect or transitioning to the next state) watch for this component being added to an entity.

### ⭐ Constructors
```csharp
public AnimationCompleteComponent()
```



⚡