# RevertMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct RevertMessage : IMessage
```

A marker message with no payload intended to signal that a previously applied action or state change on an entity should be undone.

**Intent:** Provide a generic "undo" counterpart message so game-specific systems that apply a temporary effect (a buff, a status, a scripted transformation) have a standard message type to listen for when that effect needs to be reverted, instead of each system inventing its own revert message.

**Use-case:** No built-in engine system currently sends or listens for this message (it has no callers under `src/Murder`); it exists as a ready-made message type for game-specific systems to send when an action previously taken on an entity (for example by a `RevertMessage`-aware interaction or effect system) needs to be undone.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
