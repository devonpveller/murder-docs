# AdvancedBlackboardInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct AdvancedBlackboardInteraction : IInteraction
```

Executes a list of conditional [BlackboardAction](../../Murder/Interactions/BlackboardAction.html) entries on interaction, each with its own requirement checks.

**Intent:** Applies multiple conditional blackboard mutations in a single interaction.

**Use-case:** Use when an interaction needs to evaluate and apply several independent sets of blackboard conditions and actions, such as branching story state changes triggered by a single in-world event.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public AdvancedBlackboardInteraction()
```

### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Iterates over all configured blackboard actions and invokes each one that passes its requirement checks.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡