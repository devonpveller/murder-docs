# PlayAnimationOnRuleComponent

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct PlayAnimationOnRuleComponent : IComponent
```

Component that stores an ordered list of animation/condition pairs evaluated each frame to select which animation to play.

**Intent:** Provides data-driven animation selection by matching blackboard criteria to named animations without requiring custom code per-entity.

**Use-case:** Attach to a sprite entity that also has a `RuleWatcherComponent`. `PlayAnimationOnRuleMatchSystem` is a reactive system that re-evaluates whenever the watched blackboard state changes (entity added/modified/removed with `RuleWatcherComponent`) rather than every frame: it walks `Rules` in order, matches each entry's `Requirements` against the save's `BlackboardTracker`, and calls `PlaySpriteAnimation` with the first matching entry's animation — tracking the match via `AnimationRuleMatchedComponent` so it doesn't restart the same animation redundantly on the next re-evaluation.

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
