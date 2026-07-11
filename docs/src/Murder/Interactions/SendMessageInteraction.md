# SendMessageInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SendMessageInteraction : IInteraction
```

Broadcasts a Bang `IMessage` to a target entity (self, parent, interactor, or a referenced target) when the interaction fires.

**Intent:** Sends an arbitrary message to a specific entity in the ECS world as part of an interaction.

**Use-case:** Use to notify systems that observe a particular message type, such as sending a `DamageMessage` or a custom event message to a controller entity when an interactive trigger is activated.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Properties
#### Message
```csharp
public readonly IMessage Message;
```
The message instance to dispatch when the interaction fires.

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Resolves the target entity from `Target` and dispatches `Message` to it.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡