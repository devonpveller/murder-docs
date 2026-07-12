# OnExitMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct OnExitMessage : IMessage
```

A marker message with no payload sent to notify an entity that an ongoing interaction with it has ended.

**Intent:** Signal to a previously-interacted entity that the interacting entity has finished or exited its interaction, complementing the "start" signal carried by `InteractMessage`.

**Use-case:** `InteractOnStartOnEndSystem.Exit` sends this (`e.SendOnExitMessage()`) — immediately followed by an `InteractMessage` — to every entity with an `InteractOnStartOnEndComponent` when the system itself exits (e.g. the scene/world is tearing down), so interaction-driven state can be closed out cleanly. `PlayEventInteraction` checks for its presence with `interactor.HasOnExitMessage()` to decide whether a sound tied to the interaction should be stopped (fading out) instead of started. Send/check this alongside `InteractMessage` whenever an interaction needs an explicit "this has ended" signal rather than just "this happened".

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
