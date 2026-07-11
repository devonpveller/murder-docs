# TargetedInteractionCollection

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct TargetedInteractionCollection : IInteraction
```

Runs a set of interactions against specific named target entities resolved from the interacted entity's `IdTargetCollection`.

**Intent:** Dispatches different interactions to different named target entities from a single interaction event.

**Use-case:** Use when a single trigger needs to interact with multiple distinct entities in the world — for example, opening several doors at once or activating a group of machines by name.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public TargetedInteractionCollection()
```

### ⭐ Properties
#### Interactives
```csharp
public readonly ImmutableArray<T> Interactives;
```
The list of target-specific interaction bundles to evaluate when this collection fires.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Resolves each item's named target from the `IdTargetCollection` and fires its interactions against that entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡