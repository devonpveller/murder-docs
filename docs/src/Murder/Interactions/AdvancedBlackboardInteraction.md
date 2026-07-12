# AdvancedBlackboardInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct AdvancedBlackboardInteraction : IInteraction
```

Evaluates a list of [BlackboardAction](../../Murder/Interactions/BlackboardAction.html) bundles, in order, and invokes each one whose criteria currently match.

**Intent:** Applies multiple conditional blackboard mutations/sub-interactions in a single interaction, branching on the current save state.

**Use-case:** Use instead of a plain [BlackboardActionInteraction](../../Murder/Interactions/BlackboardActionInteraction.html) when a single trigger needs to apply a different set of blackboard mutations and interactions depending on which conditions are currently met — for example, a switch that behaves differently the second time it is used, or a trigger whose consequences depend on prior player choices.

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

Invokes every configured `BlackboardAction`; each one independently checks its own requirements against the active save's blackboard and only applies its actions/interactions when they pass.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
