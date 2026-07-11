# BlackboardActionInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct BlackboardActionInteraction : IInteraction
```

Applies a single [DialogAction](../../Murder/Core/Dialogs/DialogAction.html) to the active save's blackboard when the interaction fires.

**Intent:** Mutates a blackboard variable in response to an in-world interaction.

**Use-case:** Use to record game-state changes triggered by interaction, such as setting a flag when the player picks up an item or flips a switch.

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
Executes the configured dialog action on the active save's blackboard tracker.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡