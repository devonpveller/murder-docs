# DestroyOnBlackboardConditionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DestroyOnBlackboardConditionComponent : IComponent
```

Schedules this entity for destruction when a set of blackboard conditions evaluate to true.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Allows data-driven lifetime control so entities are automatically removed when the game world reaches certain state (e.g., a quest flag is set).

**Use-case:** Attach to an entity and configure `Rules` with `CriterionNode` conditions; `DestroyOnBlackboardConditionSystem` monitors blackboard changes and destroys the entity when all rules are satisfied.

### ⭐ Constructors

```csharp
public DestroyOnBlackboardConditionComponent()
```

```csharp
public DestroyOnBlackboardConditionComponent(CriterionNode node)
```

**Parameters** \
`node` [CriterionNode](../../Murder/Core/Dialogs/CriterionNode.html) \

### ⭐ Properties

#### Rules

```csharp
public readonly ImmutableArray<T> Rules;
```

List of requirements for destroying this object.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
