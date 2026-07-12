# RemoveFromParentInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct RemoveFromParentInteraction : IInteraction
```

Detaches the interacted entity from its parent without destroying it.

**Intent:** Frees a child entity from its composite so it starts behaving as an independent entity.

**Use-case:** Use to "free" a child entity from a composite — for example, dropping a held item so it stops following its owner, or detaching a piece of a destructible object so it can fall or fly off on its own.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Unparents `interacted`, if it is not null. Has no effect on an entity that has no parent, and does not destroy the entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
