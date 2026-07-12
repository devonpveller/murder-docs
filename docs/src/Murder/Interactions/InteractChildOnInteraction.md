# InteractChildOnInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractChildOnInteraction : IInteraction
```

Forwards an [InteractMessage](../../Murder/Messages/InteractMessage.html) from the interactor down to one or more named children of the interacted entity.

**Intent:** Routes an interaction event to specific named child entities.

**Use-case:** Use when the entity being interacted with is a composite built from child entities (see [AddChildOnInteraction](../../Murder/Interactions/AddChildOnInteraction.html)) and the actual interactive behaviour lives on a specific child rather than the parent itself — for example, interacting with an NPC should route to a dialog-handling child, or triggering a machine should forward to a moving part.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public InteractChildOnInteraction()
```

### ⭐ Properties

#### Children

```csharp
public readonly ImmutableArray<string> Children;
```

Names of the child entities (matched the same way as `AddChildOnInteraction` names its children) that will receive the forwarded `InteractMessage`.

**Returns** \
[ImmutableArray\<string\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Looks up each name in `Children` as a child of the interacted entity and, for every one found, sends it an `InteractMessage` carrying the interactor. Children that cannot be found are silently skipped.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
