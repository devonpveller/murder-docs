# SendToParentInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SendToParentInteraction : IInteraction
```

Sends a message to the parent entity of the interacted entity when the interaction fires.

**Intent:** Propagates an interaction event up to the parent entity in the entity hierarchy.

**Use-case:** Use when a child component (such as a trigger collider or a sub-object) needs to notify its parent that it has been interacted with, for example a button entity nested under a machine that should react on the machine's behalf.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Properties

#### CustomMessage

```csharp
public readonly IMessage CustomMessage;
```

Optional message to send to the parent instead of the default `InteractMessage`. When `null`, a new `InteractMessage` carrying the interacted entity as sender is sent instead.

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Sends `CustomMessage` (or a default `InteractMessage`) to the parent of `interacted`. Does nothing if `interacted` is `null` or has no parent.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
