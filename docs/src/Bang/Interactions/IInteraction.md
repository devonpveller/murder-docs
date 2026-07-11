# IInteraction

**Namespace:** Bang.Interactions \
**Assembly:** Bang.dll

```csharp
public abstract IInteraction
```

An interaction is any logic which will be immediately sent to another entity. It is the lightweight,
data-only counterpart to [IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html): implementations are typically
declared as small `readonly struct`s (e.g. "send a message", "destroy the target", "play a sound") that
describe *what* should happen, without themselves being components on an entity.

Because a plain `IInteraction` is not a component, it cannot be added to an entity on its own. To attach
one, wrap it in [InteractiveComponent&lt;T&gt;](../../Bang/Interactions/InteractiveComponent-1.html), which adapts any `IInteraction` into an
[IInteractiveComponent](../../Bang/Interactions/IInteractiveComponent.html) that can live on an [Entity](../../Bang/Entities/Entity.html). Interactions can also be composed: it is a
common pattern for a game to define its own `IInteraction` that simply holds a collection of other
interactions and forwards `Interact` to each of them, letting a single interact event trigger several
effects in sequence (send a message, play a sound, deactivate the entity, and so on).

### ⭐ Methods
#### Interact(World, Entity, Entity)
```csharp
public abstract void Interact(World world, Entity interactor, Entity interacted)
```

Contract immediately performed once <paramref name="interactor" /> interacts with <paramref name="interacted" />.
This is called synchronously, on the spot, by whatever triggered the interaction — for example a system
reacting to a collision message or an explicit "interact" message — there is no queueing or delay involved.
An autonomous agent implementing a new interaction should treat this method as the single place where the
interaction's side effects happen; it should not assume it will be called again or that any state persists
between calls unless it explicitly stores that state on one of the entities involved.

`world` is the world the interaction is taking place in, `interactor` is the entity that initiated the
interaction (e.g. the player), and `interacted` is the entity being interacted with, if any — it may be
`null` when the interaction does not have a specific target entity to act on.

**Parameters** \
`world` [World](../../Bang/World.html) \
`interactor` [Entity](../../Bang/Entities/Entity.html) \
`interacted` [Entity](../../Bang/Entities/Entity.html) \



⚡
