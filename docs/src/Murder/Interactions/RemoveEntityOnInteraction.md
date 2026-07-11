# RemoveEntityOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct RemoveEntityOnInteraction : IInteraction
```

Destroys a specified entity (interacted, interactor, parent, child, or target) when the interaction fires.

**Intent:** Removes an entity from the world as a consequence of an interaction.

**Use-case:** Use to despawn consumables, destroy obstacles, remove the interactor after it uses an item, or clean up one-shot objects when the player activates them.

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
Components to add to the target entity immediately before it is destroyed, useful for triggering reactive systems on the way out.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
#### DestroyWho
```csharp
public readonly DestroyWho DestroyWho;
```
Determines which entity is destroyed when the interaction fires.

**Returns** \
[DestroyWho](../../Murder/Interactions/DestroyWho.html) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Determines the target entity based on `DestroyWho`, optionally adds pre-removal components, then destroys the target.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡