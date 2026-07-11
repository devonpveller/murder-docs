# InteractorMessage

**Namespace:** Bang.Interactions \
**Assembly:** Bang.dll

```csharp
public sealed struct InteractorMessage : IMessage
```

A payload immediately fired once an event happens. This is an intentionally empty [IMessage](../../Bang/Components/IMessage.html): it
exists as a bare marker/template that shows how "an interaction happened" can be modeled as a message sent
to an entity, so that any system tagged with `[Messager(typeof(InteractorMessage))]` reacts to it via
[IMessagerSystem](../../Bang/Systems/IMessagerSystem.html). It carries no data because, by the time a message is dispatched, the code that
sent it already has direct access to the [World](../../Bang/World.html), the interactor entity and the interacted entity, and can
act on them immediately — the message itself is only the trigger, not a data carrier.

Games built on top of Bang typically define their own richer message type instead of using this one
directly — for example, the Murder engine defines `InteractMessage`, a struct implementing `IMessage` that
carries an `Entity? Interactor` field, and systems dispatch a target entity's `IInteractiveComponent.Interact`
in response to it. Treat `InteractorMessage` as a minimal reference example rather than something to send
in production game code as-is.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_



⚡
