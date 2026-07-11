# InteractiveComponent\<T\>

**Namespace:** Bang.Interactions \
**Assembly:** Bang.dll

```csharp
public sealed struct InteractiveComponent<T> : IInteractiveComponent, IComponent
```

Implements an interaction component which will be passed on to the entity. This is the generic adapter
that turns any `T` (a plain [IInteraction](../../Bang/Interactions/IInteraction.html) struct, such as "send a message" or "destroy the
target") into a real [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) that can be added to an [Entity](../../Bang/Entities/Entity.html) and picked up
by systems that filter on `IInteractiveComponent`.

This is the type editor tooling and content authors reach for when wiring up "when interacted with, do X"
behavior on an entity, instead of writing a bespoke component for every interaction. For example, in the
Murder engine `SendMessageInteraction : IInteraction` is attached to an entity as
`InteractiveComponent<SendMessageInteraction>`, and a system such as `InteractSystem` — filtered on
`IInteractiveComponent` and reacting to an interact message — fetches the component off the entity and
calls `Interact(world, interactor, entity)` on it, which forwards straight through to the wrapped
`SendMessageInteraction.Interact`. Interactions can also be grouped: a collection-style `IInteraction` (or
`IInteractiveComponent`) can hold several inner interactions and call `Interact` on each of them in turn,
letting one interact event trigger multiple effects.

**Implements:** _[IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html), [IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public InteractiveComponent<T>()
```

Default constructor, initializes a brand new interaction.

```csharp
public InteractiveComponent<T>(T interaction)
```

Creates a new [InteractiveComponent&lt;T&gt;](../../Bang/Interactions/InteractiveComponent-1.html) wrapping the given `interaction` instance.

**Parameters** \
`interaction` [T](../../) \

### ⭐ Methods
#### FetchInteraction()
```csharp
public T FetchInteraction()
```

Gets the wrapped `T` interaction instance. Useful when code — such as editor tooling or another system —
needs to inspect or reuse the underlying interaction data directly, rather than only invoking [Interact(World, Entity, Entity)](../../Bang/Interactions/InteractiveComponent-1.html).

**Returns** \
[T](../../) \

#### Interact(World, Entity, Entity)
```csharp
public virtual void Interact(World world, Entity interactor, Entity interacted)
```

Calls the inner interaction component. `world` is the world the interaction is taking place in, `interactor`
is the entity that initiated the interaction, and `interacted` is the entity being interacted with, if any.
This simply forwards to the wrapped `T` instance's own `Interact` implementation.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
