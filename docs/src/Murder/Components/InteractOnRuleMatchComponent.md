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

Creates a component with no requirements, default `InteractOn` (`AddedOrModified`) and default `AfterInteraction` (`RemoveComponent`). Used by the editor/serializer as the blank starting state.

```csharp
public InteractOnRuleMatchComponent(InteractOn interactOn, AfterInteractRule after, ImmutableArray<CriterionNode> requirements)
```

Creates a fully configured rule, explicitly specifying when it is evaluated.

**Parameters** \
`interactOn` [InteractOn](../../Murder/Components/InteractOn.html) \
`after` [AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \
`requirements` [ImmutableArray\<CriterionNode\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public InteractOnRuleMatchComponent(AfterInteractRule after, ImmutableArray<CriterionNode> requirements)
```

Creates a rule using the default `InteractOn` (`AddedOrModified`), only specifying the post-interaction behavior and the requirements.

**Parameters** \
`after` [AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \
`requirements` [ImmutableArray\<CriterionNode\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

```csharp
public InteractOnRuleMatchComponent(params CriterionNode[] criteria)
```

Creates a rule from a params list of criteria, using every other setting's default value. The most convenient constructor for building simple rules in code.

**Parameters** \
`criteria` [CriterionNode[]](../../Murder/Core/Dialogs/CriterionNode.html) \

### ⭐ Properties

#### AfterInteraction

```csharp
public readonly AfterInteractRule AfterInteraction;
```

What to do with this component/entity once `Requirements` are satisfied and the interaction fires. See [AfterInteractRule](../../Murder/Components/AfterInteractRule.html) for the available behaviors (interact once, always interact, remove this component, or destroy the entity).

**Returns** \
[AfterInteractRule](../../Murder/Components/AfterInteractRule.html) \

#### InteractOn

```csharp
public readonly InteractOn InteractOn;
```

Controls whether the rule is checked on the first set of the watched blackboard value, on subsequent modifications only, or both.

**Returns** \
[InteractOn](../../Murder/Components/InteractOn.html) \

#### Requirements

```csharp
public readonly ImmutableArray<CriterionNode> Requirements;
```

List of requirements which will trigger the interactive component within the same entity.

**Returns** \
[ImmutableArray\<CriterionNode\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
