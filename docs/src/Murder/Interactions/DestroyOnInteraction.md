# DestroyOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct DestroyOnInteraction : IInteraction
```

Minimal interaction that destroys the interacted entity when it fires.

**Intent:** Simple, single-purpose destruction of the interacted entity.

**Use-case:** Currently only the `TargetEntity.Self` case is implemented — every other [TargetEntity](../../Murder/Utilities/TargetEntity.html) value is a no-op, so this type is only useful with its default configuration today. Prefer [RemoveEntityOnInteraction](../../Murder/Interactions/RemoveEntityOnInteraction.html) for anything that needs to destroy an entity other than the interacted one (parent, interactor, a named target, etc.).

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public DestroyOnInteraction()
```

### ⭐ Properties

#### Target

```csharp
public readonly TargetEntity Target;
```

Which entity to destroy. Only `TargetEntity.Self` (the default) currently has any effect; other values are silently ignored.

**Returns** \
[TargetEntity](../../Murder/Utilities/TargetEntity.html) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Destroys `interacted` when `Target` is `TargetEntity.Self`. Does nothing for any other `Target` value.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
