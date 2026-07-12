# SendInteractMessageInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SendInteractMessageInteraction : IInteraction
```

Re-sends an `InteractMessage` to the interacted entity itself, carrying the original interactor as the message's sender.

**Intent:** Re-broadcasts an interaction event to the interacted entity's own message listeners.

**Use-case:** Use to relay or forward an interaction — any other interaction or reactive system already listening for `InteractMessage` on the interacted entity fires again, as if it had been interacted with directly. This is handy for proxy/relay entities, or for triggering an entity's normal interact pipeline from code paths that don't go through the usual interact-button flow (e.g. `InteractOnStartSystem`, `InteractOnCollisionSystem`).

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Sends an `InteractMessage` to `interacted`, carrying `interactor` as the message's sender. Does nothing if `interacted` is `null`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
