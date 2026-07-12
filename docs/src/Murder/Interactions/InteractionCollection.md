# InteractionCollection

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractionCollection : IInteraction
```

Bundles several other `IInteractiveComponent` instances and fires all of them, in order, from a single trigger.

**Intent:** Groups multiple `IInteraction` implementations so they all execute in sequence when the entity is interacted with.

**Use-case:** The standard way to make one interactive entity do several unrelated things at once (play a sound, mutate a blackboard variable, spawn a particle effect, etc.) without writing a bespoke composite interaction type for every combination.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public InteractionCollection()
```

```csharp
public InteractionCollection(ImmutableArray<IInteractiveComponent> interactives)
```

Creates a collection that will fire exactly `interactives`, in order.

**Parameters** \
`interactives` [ImmutableArray\<IInteractiveComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties

#### Interactives

```csharp
public readonly ImmutableArray<IInteractiveComponent> Interactives;
```

The ordered list of interactions that will be invoked, one after another, when this collection is triggered.

**Returns** \
[ImmutableArray\<IInteractiveComponent\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### WithInteraction(IInteractiveComponent)

```csharp
public InteractionCollection WithInteraction(IInteractiveComponent interactive)
```

Returns a new `InteractionCollection` with `interactive` appended to the end of `Interactives`. Since the struct is immutable, this does not mutate the original collection — it is intended for building up a collection fluently, e.g. from code that composes interactions at runtime.

**Parameters** \
`interactive` [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) \

**Returns** \
[InteractionCollection](../../Murder/Interactions/InteractionCollection.html) \

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Invokes every interaction in `Interactives`, in order, against the same interactor/interacted pair.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
