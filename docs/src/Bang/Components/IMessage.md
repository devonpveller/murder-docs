# IMessage

**Namespace:** Bang.Components \
**Assembly:** Bang.dll

```csharp
public abstract IMessage
```

A special type of component that will disappear within the next frame.

`IMessage` is Bang's mechanism for one-shot, fire-and-forget notifications between systems and
entities, as opposed to [IComponent](../../Bang/Components/IComponent.html), which models
persistent entity state. Sending a message is done with `Entity.SendMessage<T>(...)`, which stores
the message alongside the entity's components (indexed separately, see `ComponentsLookup`) and
raises `Entity.OnMessage`; any [ISystem](../../Bang/Systems/ISystem.html) implementing
`IMessagerSystem` and tagged with a `[Messager(typeof(T))]` attribute for that message type will
have its `OnMessage(World, Entity, IMessage)` called for it during that update. Unlike a regular
component, a message is automatically removed from the entity right after the frame it was sent
in — systems should treat receiving one as an instantaneous event, not as a durable flag to poll
for on subsequent frames.

Like `IComponent`, `IMessage` is a plain marker interface with no members, and Bang follows the
same convention of implementing it on small `readonly struct` types. Some messages carry no data
at all and simply signal that something happened, e.g. `public struct InteractorMessage :
IMessage { }` in `bang\src\Bang\Interactions\InteractorMessage.cs`; others carry a small payload,
e.g. `InteractMessage` in `src\Murder\Messages\InteractMessage.cs`, which wraps the interacting
`Entity`. Game code should implement `IMessage` on any new struct meant to represent a transient
event (an interaction, a collision, an animation completing, a dialog line finishing, etc.) that
one or more systems need to react to on the very next update.



⚡