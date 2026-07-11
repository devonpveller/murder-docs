# SendInteractMessageInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SendInteractMessageInteraction : IInteraction
```

Sends an `InteractMessage` back to the interacted entity from itself, causing its own interaction listeners to fire again.

**Intent:** Re-broadcasts an interaction event to the interacted entity's own message listeners.

**Use-case:** Use to create a chain reaction where interacting with an entity triggers its own internal interaction pipeline again, useful for relay or forwarding patterns.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Sends an `InteractMessage` to the interacted entity using the interactor as the sender.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡