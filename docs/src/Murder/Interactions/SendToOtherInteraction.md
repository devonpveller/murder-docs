# SendToOtherInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SendToOtherInteraction : IInteraction
```

Sends a Bang `IMessage` to one or more entities referenced by name in the interacted entity's target collection.

**Intent:** Dispatches a message to explicitly named target entities rather than the direct interactor or parent.

**Use-case:** Use to trigger behaviour on distant or unrelated entities from a single interaction point, such as opening a gate elsewhere in the level when a lever is pulled.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public SendToOtherInteraction()
```

### ⭐ Properties
#### _targets
```csharp
public readonly ImmutableArray<T> _targets;
```

Guid of the target entity.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### Message
```csharp
public readonly IMessage Message;
```
The message to send to each resolved target entity.

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Resolves each target entity by name, then sends `Message` to each one found.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡