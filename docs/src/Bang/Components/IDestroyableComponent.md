# IDestroyableComponent

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public interface IDestroyableComponent
```

Marks a component that needs to run custom cleanup logic when it stops being attached to an
entity, either because the component was replaced with a different value or removed altogether.
`Entity.ReplaceComponent` and `Entity.RemoveComponent` both check whether the *previous* component
instance implements `IDestroyableComponent` and, if so, queue its `OnDestroyed()` for execution via
`World.RegisterToNotifyAfterUpdate(...)`. Because the call is deferred to the end of the current
update rather than invoked inline, it is safe to use `OnDestroyed` to release resources (event
subscriptions, native handles, pooled objects, etc.) without risking interference with systems that
are still iterating over this frame's entities. This is distinct from
[IModifiableComponent](../../Bang/Components/IModifiableComponent.html), which is about the
component's *value* changing in place; `IDestroyableComponent` is specifically about the component
instance going away.

The most notable implementer in Bang itself is `StateMachineComponent<T>`
(`bang\src\Bang\StateMachines\StateMachineComponent.cs`), whose `OnDestroyed()` forwards to the
underlying `StateMachine`'s own `OnDestroyed()` — this is how a state machine gets a chance to run
teardown logic (stopping coroutines, cleaning up subscriptions, etc.) exactly once, at the moment
its component stops being attached to the entity, regardless of whether that happened via a
replace or an outright removal. Implement this interface on a component when it owns something
that must be explicitly released when the component's lifetime on the entity ends.

### ⭐ Methods
#### OnDestroyed()
```csharp
public abstract void OnDestroyed()
```

Called after the entity has replaced or removed this component instance. Use this to unsubscribe
from external events or release any resource that the component was holding on to while it was
active. The call happens after the current world update finishes, not synchronously at the moment
of replace/remove.



⚡