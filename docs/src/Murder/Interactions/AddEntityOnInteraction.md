# AddEntityOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct AddEntityOnInteraction : IInteraction
```

This will trigger an effect by placing [AddEntityOnInteraction._prefab](../../Murder/Interactions/AddEntityOnInteraction.html#_prefab) in the world.

**Intent:** Spawns a prefab entity into the world when the interaction fires.

**Use-case:** Use to create projectiles, particle effects, loot pickups, or other prefab instances at runtime as a consequence of interacting with an entity.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public AddEntityOnInteraction()
```

```csharp
public AddEntityOnInteraction(Guid prefab)
```

**Parameters** \
`prefab` [Guid](https://learn.microsoft.com/en-us/dotnet/api/System.Guid?view=net-7.0) \

### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Creates the configured prefab entity in the world, applies any custom components, and optionally positions it at the interactor or interacted entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡