# BlackboardActionInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct BlackboardActionInteraction : IInteraction
```

Applies a single unconditional [DialogAction](../../Murder/Core/Dialogs/DialogAction.html) to the active save's blackboard when the interaction fires.

**Intent:** Mutates a blackboard variable in response to an in-world interaction.

**Use-case:** The simplest way to record a game-state change triggered by interaction, such as setting a flag when the player picks up an item or flips a switch. For a version that first checks conditions and can apply several different actions/interactions depending on save state, see [AdvancedBlackboardInteraction](../../Murder/Interactions/AdvancedBlackboardInteraction.html).

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public BlackboardActionInteraction()
```

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Applies the configured dialog action directly to the active save's blackboard tracker, ignoring `world`, `interactor`, and `interacted`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
