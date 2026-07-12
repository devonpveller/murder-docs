# OnStartMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct OnStartMessage : IMessage
```

A marker message with no payload intended to notify an entity that an interaction (or similar scripted sequence) with it has started.

**Intent:** Provide a generic "start" counterpart to [OnExitMessage](../../Murder/Messages/OnExitMessage.html) so game-specific systems can signal the beginning of an interaction/state without introducing a bespoke message type. Compare with `InteractMessage`, which is the message actually used by the built-in interaction systems (`InteractSystem`, `InteractOnStartSystem`, `InteractOnStartOnEndSystem`) to report an interaction starting.

**Use-case:** No built-in engine system currently sends or listens for this message (it has no callers under `src/Murder`); it exists as a ready-made message type for game-specific code that needs a distinct "started" signal separate from `InteractMessage`, for example to drive a custom state machine or scripted sequence.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
