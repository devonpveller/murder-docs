# SendToParentInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SendToParentInteraction : IInteraction
```

Sends a message to the parent entity of the interacted entity when the interaction fires.

**Intent:** Propagates an interaction event up to the parent entity in the entity hierarchy.

**Use-case:** Use when a child component (such as a trigger collider or a sub-object) needs to notify its parent that it has been interacted with, for example a button child informing its parent machine.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Properties
#### CustomMessage
```csharp
public readonly IMessage CustomMessage;
```
An optional custom message to send; if `null`, a default `InteractMessage` is sent with the interacted entity as sender.

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Sends `CustomMessage` (or a default `InteractMessage`) to the parent of the interacted entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡