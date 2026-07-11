# InteractChildOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractChildOnInteraction : IInteraction
```

Sends an [InteractMessage](../../Murder/Messages/InteractMessage.html) to one or more named children of the interacted entity.

**Intent:** Forwards an interaction event down to specific named child entities.

**Use-case:** Use when interacting with a parent entity should trigger behaviour on specific children, such as activating a mechanism that is modelled as a child node.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors
```csharp
public InteractChildOnInteraction()
```

### ⭐ Properties
#### Children
```csharp
public readonly ImmutableArray<T> Children;
```
Names of the child entities that will receive the interact message.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \
### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```
Sends an `InteractMessage` from the interactor to each child listed in `Children`.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡