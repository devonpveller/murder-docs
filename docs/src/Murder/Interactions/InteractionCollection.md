# InteractionCollection

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractionCollection : IInteraction
```

This triggers a list of different interactions within this entity.

**Intent:** Groups multiple `IInteraction` implementations so they all execute in sequence when the entity is interacted with.

**Use-case:** Use as the primary interaction component when an entity needs to perform several independent actions simultaneously, such as playing a sound, modifying a blackboard variable, and spawning a particle effect all at once.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public InteractionCollection()
```

```csharp
public InteractionCollection(ImmutableArray<T> interactives)
```

**Parameters** \
`interactives` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Properties
#### Interactives
```csharp
public readonly ImmutableArray<T> Interactives;
```
The ordered list of interactions that will be invoked when this collection is triggered.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### WithInteraction(IInteractiveComponent)
```csharp
public InteractionCollection WithInteraction(IInteractiveComponent interactive)
```
Returns a new `InteractionCollection` with the given interaction appended.

**Parameters** \
`interactive` [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) \

**Returns** \
[InteractionCollection](../../Murder/Interactions/InteractionCollection.html) \

#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Invokes every interaction in `Interactives` in order.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡