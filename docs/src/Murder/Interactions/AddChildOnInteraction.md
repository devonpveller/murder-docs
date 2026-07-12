# AddChildOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct AddChildOnInteraction : IInteraction
```

Instantiates a configured prefab and attaches it as a named child of the interacted entity.

**Intent:** Dynamically composes an entity out of sub-entities at interaction time.

**Use-case:** Use when interacting with an entity should attach a child prefab to it — equipping a held item, spawning a visual sub-entity/attachment, or building up a composite entity out of pieces as gameplay progresses. Combine with [AddChildProperties](../../Murder/Interactions/AddChildProperties.html)'s `SendEventComponentToParent` flag when the spawned child needs its animation/event triggers to be observed by the parent entity's own logic.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public AddChildOnInteraction()
```

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Instantiates the configured prefab and attaches it as a named child of the interacted entity. If configured with the `SendEventComponentToParent` property, the child's `EventListenerComponent` (if any) is merged into the parent's own event listener and removed from the child.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
