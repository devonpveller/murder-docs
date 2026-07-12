# SendMessageInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SendMessageInteraction : IInteraction
```

Broadcasts a Bang `IMessage` to a target entity (self, parent, interactor, a referenced target, or every child) when the interaction fires.

**Intent:** Sends an arbitrary message to one or more entities in the ECS world as part of an interaction, without needing a bespoke `IInteraction` for every message type.

**Use-case:** Use to notify systems that observe a particular message type, such as sending a custom "activated" message to a controller entity, forwarding a message to every child of a container, or messaging the entity referenced by an `IdTarget`/`IdTargetCollection` when an interactive trigger is activated.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public SendMessageInteraction()
```

```csharp
public SendMessageInteraction(IMessage message, TargetEntity target)
```

Creates an interaction that sends `message` to the entity selected by `target`.

**Parameters** \
`message` [IMessage](../../Bang/Components/IMessage.html) \
`target` [TargetEntity](../../Murder/Utilities/TargetEntity.html) \

### ⭐ Properties

#### Message

```csharp
public readonly IMessage Message;
```

The message instance to dispatch when the interaction fires. Nothing is sent if this is left `null`.

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \

#### Target

```csharp
public readonly TargetEntity Target;
```

Which entity (relative to the interaction) receives `Message`. Defaults to `TargetEntity.Self`, i.e. the interacted entity. `TargetEntity.Target` resolves the interacted entity's `IdTarget`/`IdTargetCollection`, and `TargetEntity.Child` sends the message to every child of the interacted entity.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Resolves the entity (or entities) selected by `Target` and dispatches `Message` to each of them. Does nothing if `interacted` is `null` or `Message` is unset.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
