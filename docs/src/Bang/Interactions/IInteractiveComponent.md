# IInteractiveComponent

**Namespace:** Bang.Interactions \
**Assembly:** Bang.dll

```csharp
public abstract IInteractiveComponent : IComponent
```

Component that will interact with another entity. Unlike [IInteraction](../../Bang/Interactions/IInteraction.html) (a plain struct describing
behavior), this is a full-fledged [IComponent](../../Bang/Components/IComponent.html), so it can be attached directly to an
[Entity](../../Bang/Entities/Entity.html) and discovered by a [ISystem](../../Bang/Systems/ISystem.html) that filters on `IInteractiveComponent`.

In practice, a system reacting to an "interact" event — for example one tagged
`[Filter(typeof(IInteractiveComponent))]` and `[Messager(typeof(SomeInteractMessage))]` — looks up this
component on the target entity via `entity.TryGetInteractive()` and calls `Interact` on it directly.
Another common pattern is a collision-driven system that iterates every
`IInteractiveComponent` configured on an entity (e.g. "on enter" and "on exit" lists) and invokes
`Interact` on each one in turn.

Most game code does not implement this interface by hand. Instead, implement [IInteraction](../../Bang/Interactions/IInteraction.html) with a
small struct describing the desired behavior, and wrap it with [InteractiveComponent&lt;T&gt;](../../Bang/Interactions/InteractiveComponent-1.html), which
already implements `IInteractiveComponent` and simply forwards to the wrapped interaction. Implementing
`IInteractiveComponent` directly only makes sense when the interaction needs to *be* the component itself
(for instance, to carry additional serialized fields alongside the interaction logic).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public abstract void Interact(World world, Entity interactor, Entity interacted)
```

This is the logic which will be immediately called once the <paramref name="interactor" /> interacts with the
<paramref name="interacted" />. `world` is the world the interaction is taking place in, `interactor` is the
entity that initiated the interaction (e.g. the player), and `interacted` is the entity being interacted
with, if any — this is commonly the entity that owns this very component, but callers are free to pass a
different (or a `null`) target.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
