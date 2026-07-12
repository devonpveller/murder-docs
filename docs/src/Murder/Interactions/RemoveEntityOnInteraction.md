# RemoveEntityOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct RemoveEntityOnInteraction : IInteraction
```

Destroys an entity — chosen relative to the interaction — when the interaction fires.

**Intent:** Removes an entity from the world as a consequence of an interaction, without requiring a bespoke system.

**Use-case:** Use to despawn consumables and pickups, destroy a one-shot trigger after it fires, remove the interactor after it consumes an item, or clean up a scripted obstacle once the player has dealt with it. Pair with `AddComponentsBeforeRemoving` when a reactive system needs one extra frame to observe the entity before it disappears.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public RemoveEntityOnInteraction()
```

### ⭐ Properties

#### AddComponentsBeforeRemoving

```csharp
public readonly ImmutableArray<T> AddComponentsBeforeRemoving;
```

Components to add to the target entity immediately before it is destroyed. Useful to filter out reactive systems: tagging the entity with a marker component lets an "on death"/"on removed" reactive system pick it up for one last frame before it is gone.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### DestroyWho

```csharp
public readonly DestroyWho DestroyWho;
```

Determines which entity is destroyed when the interaction fires: the interacted entity, the interactor, the interacted entity's parent or first child, an explicitly named target, or none at all.

**Returns** \
[DestroyWho](../../Murder/Interactions/DestroyWho.html) \

#### Target

```csharp
public readonly string? Target;
```

Optional name of the entity to destroy when `DestroyWho` is `Target`. When left unset, the interacted entity's single `IdTargetComponent` target is used instead; if that is also absent, every entity registered in the interacted entity's `IdTargetCollectionComponent` is destroyed.

**Returns** \
[string](https://learn.microsoft.com/en-us/dotnet/api/System.String?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Resolves the entity selected by `DestroyWho` (and `Target`, when applicable), applies every component in `AddComponentsBeforeRemoving` to it, then destroys it. Does nothing if no entity resolves for the selected option.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
