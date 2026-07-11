# InteractOnRuleMatchComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractOnRuleMatchComponent : IComponent
```

Defines a set of blackboard criterion rules that, when matched, trigger the entity's interactive components.

**Intent:** Fire an interaction automatically whenever a specific combination of blackboard/game-state conditions becomes true.

**Use-case:** Add to a story entity with a list of `Requirements` (criterion nodes); the `InteractOnRuleMatchSystem` evaluates these each frame and calls the interaction when all criteria pass.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public InteractOnRuleMatchComponent()
```

```csharp
public InteractOnRuleMatchComponent(AfterInteractRule after, bool triggered, ImmutableArray<T> requirements)
```

**Parameters** \
`after` [AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \
`triggered` [bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
`requirements` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public InteractOnRuleMatchComponent(InteractOn interactOn, AfterInteractRule after, ImmutableArray<T> requirements)
```

**Parameters** \
`interactOn` [InteractOn](../../Murder/Components/InteractOn.html) \
`after` [AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \
`requirements` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public InteractOnRuleMatchComponent(CriterionNode[] criteria)
```

**Parameters** \
`criteria` [CriterionNode[]](../../Murder/Core/Dialogs/CriterionNode.html) \

### ⭐ Properties
#### AfterInteraction
```csharp
public readonly AfterInteractRule AfterInteraction;
```

Defines what happens to this component after the interaction triggers (e.g. remove it, keep it, or allow re-triggering).

**Returns** \
[AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \
#### InteractOn
```csharp
public readonly InteractOn InteractOn;
```

Specifies whether the rule evaluates on the first set of a blackboard value, on subsequent modifications, or both.

**Returns** \
[InteractOn](../../Murder/Components/InteractOn.html) \
#### Requirements
```csharp
public readonly ImmutableArray<T> Requirements;
```

List of requirements which will trigger the interactive component within the same entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Triggered
```csharp
public readonly bool Triggered;
```

This will only be triggered once the component has been interacted with.
            Used if [AfterInteractRule.InteractOnReload](../../Murder/Components/AfterInteractRule.html#interactonreload) is set.

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \
### ⭐ Methods
#### Disable()
```csharp
public InteractOnRuleMatchComponent Disable()
```

Returns a copy of this component with `Triggered` set to `true`, effectively disabling re-triggering for rules that use `AfterInteractRule.InteractOnReload`.

**Returns** \

**Returns** \
[InteractOnRuleMatchComponent](../../Murder/Components/InteractOnRuleMatchComponent.html) \



⚡