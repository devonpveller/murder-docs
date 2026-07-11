# AnimationRuleMatchedComponent

**Namespace:** Murder.Core.Graphics \
**Assembly:** Murder.dll

```csharp
public sealed struct AnimationRuleMatchedComponent : IComponent
```

A runtime-only component that records which `AnimationAndRule` index was last matched on an entity.

**Intent:** Caches the previously matched rule index so the system can skip redundant animation restarts when the same rule still applies on the next tick.

**Use-case:** Added and updated automatically by `PlayAnimationOnRuleMatchSystem`; gameplay code should not need to set this component directly.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public AnimationRuleMatchedComponent(int ruleIndex)
```

Creates the component, recording that the rule at `ruleIndex` is the current match.

**Parameters** \
`ruleIndex` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

### ⭐ Properties
#### RuleIndex
```csharp
public readonly int RuleIndex;
```

Zero-based index into the `PlayAnimationOnRuleComponent.Rules` array for the rule that is currently matched.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡