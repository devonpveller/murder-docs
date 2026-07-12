# TargetedInteractionCollection

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct TargetedInteractionCollection : IInteraction
```

Fans a single interaction out to several distinct, individually named target entities resolved from the interacted entity's [IdTargetCollectionComponent](../../Murder/Components/IdTargetCollectionComponent.html), running a different set of interactions against each one.

**Intent:** Dispatches different interactions to different named target entities from a single interaction event.

**Use-case:** Use when a single trigger needs to affect multiple distinct entities differently — for example, a master switch that opens one door, plays a sound at another entity, and sends a message to a third, all from one interaction.

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

The list of target-specific interaction bundles evaluated when this collection fires. Every item is evaluated, regardless of whether earlier items resolved their target.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Requires `interacted` to carry an `IdTargetCollectionComponent`. For each item in `Interactives`, resolves its named target from that collection and runs its `InteractionCollection` against the resolved entity — or against `null` if the name does not resolve. Logs an error and does nothing if `interacted` is `null` or lacks the target collection.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
