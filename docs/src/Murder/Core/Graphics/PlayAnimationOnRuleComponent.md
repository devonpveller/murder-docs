# PlayAnimationOnRuleComponent

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct PlayAnimationOnRuleComponent : IComponent
```

Component that stores an ordered list of animation/condition pairs evaluated each frame to select which animation to play.

**Intent:** Provides data-driven animation selection by matching blackboard criteria to named animations without requiring custom code per-entity.

**Use-case:** Attach to a sprite entity; `PlayAnimationOnRuleMatchSystem` iterates `Rules` and activates the first animation whose requirements are satisfied.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public PlayAnimationOnRuleComponent()
```

### ⭐ Properties
#### Rules
```csharp
public readonly ImmutableArray<T> Rules;
```

Ordered list of `AnimationAndRule` entries; the first entry whose criteria are satisfied determines the animation to play.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡