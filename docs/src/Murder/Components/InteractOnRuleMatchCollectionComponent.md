# InteractOnRuleMatchCollectionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractOnRuleMatchCollectionComponent : IComponent
```

Holds an ordered list of `InteractOnRuleMatchComponent` rules; when blackboard conditions are met, the matching rules trigger their interactions in sequence.

**Intent:** Support multiple independent rule-based interactions on a single entity, each with its own criteria and trigger condition.

**Use-case:** Add to a story entity with multiple conditional outcomes (e.g. different dialogue branches depending on quest state); each entry in `Requirements` is evaluated independently by the rule-match system.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public InteractOnRuleMatchCollectionComponent()
```

Creates a component with an empty requirement list.

```csharp
public InteractOnRuleMatchCollectionComponent(ImmutableArray<InteractOnRuleMatchComponent> requirements)
```

Creates a component with the given set of independent rules.

**Parameters** \
`requirements` [ImmutableArray\<InteractOnRuleMatchComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties

#### Requirements

```csharp
public readonly ImmutableArray<InteractOnRuleMatchComponent> Requirements;
```

List of interactions that will be triggered.

**Returns** \
[ImmutableArray\<InteractOnRuleMatchComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
