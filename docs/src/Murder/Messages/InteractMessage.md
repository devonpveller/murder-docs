# InteractMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractMessage : IMessage
```

Generic struct for interacting with an entity. Marked `[RuntimeOnly]`, meaning it is only ever attached to entities during gameplay and is never saved as part of a world/asset in the editor.

**Intent:** Notify an entity with an `IInteractiveComponent` that it has been interacted with, optionally passing along the identity of whichever entity triggered the interaction.

**Use-case:** This is the message every interaction path in `Murder.Interactions`/`Murder.Systems.Interactions` ultimately funnels into. `InteractSystem` listens for it (`[Messager(typeof(InteractMessage))]`) on any entity with an `IInteractiveComponent` and calls `interacted.Interact(world, interactor.Interactor ?? entity, entity)`, falling back to the receiving entity itself when `Interactor` is `null`. It is produced by `InteractOnActivateSystem`, `InteractOnCollisionSystem`, `InteractOnRuleMatchSystem`, `InteractOnStartSystem`/`InteractOnStartOnEndSystem`, and by interactions such as `SendInteractMessageInteraction`, `InteractChildOnInteraction`, `SendToParentInteraction`, and `PropagateInteraction` that forward an interaction to another entity (e.g. a parent or child) — usually via the generated `entity.SendInteractMessage(interactor)` extension. Use `Interactor` to apply interactor-specific logic, such as only letting the player entity trigger a pickup.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

### ⭐ Constructors

```csharp
public InteractMessage(Entity interactor)
```

Creates a message identifying which entity performed the interaction.

**Parameters** \
`interactor` [Entity](../../Bang/Entities/Entity.html) \

### ⭐ Properties

#### Interactor

```csharp
public readonly Entity? Interactor;
```

The entity that initiated the interaction, or `null` when no specific interactor is known (in which case listeners such as `InteractSystem` fall back to treating the receiving entity itself as the interactor).

**Returns** \
[Entity](../../Bang/Entities/Entity.html) \

⚡
