# DeactivateChildInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct DeactivateChildInteraction : IInteraction
```

Deactivates (or, optionally, activates) one or more named children found on the interacted entity's root entity (its outermost ancestor, walking up the parent chain).

**Intent:** Toggles named children relative to the top-level composite entity, regardless of which nested child the interaction fired from.

**Use-case:** Looking up from the root means this works correctly even when the interaction fires from a nested child, always resolving named children relative to the top-level composite entity — for example toggling a sibling part of a multi-entity prop from an interaction defined on one of its pieces.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public DeactivateChildInteraction()
```

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Walks up to the interacted entity's root, then for each configured child name activates or deactivates that child depending on the configured mode. Does nothing if `interacted` is null or a named child cannot be found.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
