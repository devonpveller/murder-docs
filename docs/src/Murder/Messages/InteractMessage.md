# InteractMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractMessage : IMessage
```

Generic struct for interacting with an entity.

**Intent:** Notify an entity that another entity has interacted with it, passing along the interactor's identity.

**Use-case:** Send this from player input or proximity trigger systems when the player activates an interactable object. The receiving entity's interaction handlers can inspect `Interactor` to apply context-specific logic, such as granting items only to the player entity.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors
```csharp
public InteractMessage(Entity interactor)
```

**Parameters** \
`interactor` [Entity](../../Bang/Entities/Entity.html) \

### ⭐ Properties
#### Interactor
```csharp
public readonly Entity Interactor;
```

The entity that initiated the interaction.

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \


⚡