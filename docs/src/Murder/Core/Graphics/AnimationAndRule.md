# AnimationAndRule

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationAndRule
```

Pairs one or more animation clip names with the blackboard conditions that must all be true before those clips are eligible to play.

**Intent:** Associates a set of animation clips with a list of `CriterionNode` requirements so the rule-based animation system can pick the right clip automatically.

**Use-case:** Add `AnimationAndRule` entries to a `PlayAnimationOnRuleComponent` on an entity; the system evaluates each rule in order and plays the first one whose requirements are satisfied.

### ⭐ Constructors
```csharp
public AnimationAndRule()
```

Creates an empty rule with no animation clips and no requirements.

### ⭐ Properties
#### Animation
```csharp
public readonly ImmutableArray<T> Animation;
```

The animation clip names (as defined in the sprite asset) that will play when all `Requirements` are met.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Requirements
```csharp
public readonly ImmutableArray<T> Requirements;
```

The blackboard criterion nodes that must all evaluate to true for this rule to match.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \


⚡