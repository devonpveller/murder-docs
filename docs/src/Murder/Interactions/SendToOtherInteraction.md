# SendToOtherInteraction

**Namespace:** Murder.Interactions \
**Assembly:** Murder.dll

```csharp
public sealed struct SendToOtherInteraction : IInteraction
```

Sends a Bang `IMessage` to one or more entities referenced explicitly in `_targets`, rather than to the interactor, the interacted entity, or its parent.

**Intent:** Dispatches a message to explicitly named target entities rather than the direct interactor or parent.

**Use-case:** Use to trigger behaviour on distant or unrelated entities from a single interaction point, such as opening a gate elsewhere in the level, or notifying several machines at once, when a lever is pulled.

**Implements:** _[IInteraction](../../Bang/Interactions/IInteraction.html)_

### ⭐ Constructors

```csharp
public SendToOtherInteraction()
```

### ⭐ Properties

#### \_targets

```csharp
public readonly ImmutableArray<T> _targets;
```

The entity instances (authored in the level editor via the instance picker, hence `[InstanceId]`) to send `Message` to. For each entry, resolution first tries the interacted entity's single `IdTargetComponent` target; if that is not set, it falls back to looking the entry up by name in the interacted entity's `IdTargetCollectionComponent`.

**Returns** \
[ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### Message

```csharp
public readonly IMessage Message;
```

The message to send to each resolved target entity. Nothing is sent if this is `null`.

**Returns** \
[IMessage](../../Bang/Components/IMessage.html) \

### ⭐ Methods

#### Interact(World, Entity, Entity)

```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

For each entry in `_targets`, resolves the corresponding entity and dispatches `Message` to it. Does nothing if `interacted` is `null` or `Message` is unset.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \

⚡
