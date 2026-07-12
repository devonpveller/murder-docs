# AfterMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct AfterMessage : IMessage
```

A marker message with no payload sent once an entity's trigger-collision bookkeeping for the frame has been fully processed.

**Intent:** Give systems a well-defined point in the frame to run logic that must happen strictly after all `OnCollisionMessage` enter/exit events for an entity have already been dispatched, instead of racing with them.

**Use-case:** `TriggerPhysicsSystem.OnAfterTrigger` sends this (`e.SendAfterMessage()`) at the very end of recomputing an entity's collision cache for the frame, after every `OnCollisionMessage` enter/exit for that entity has already been sent. Listen for it with `[Messager(typeof(AfterMessage))]` when a system needs to react only once collision state for the frame has fully settled — for example aggregating or finalizing state that depends on knowing all of this frame's collision enter/exit events have already fired.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
