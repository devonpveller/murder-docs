# FacingTurnCompleteMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct FacingTurnCompleteMessage : IMessage
```

A marker message with no payload sent when an entity finishes smoothly turning to face a new direction.

**Intent:** Notify systems that a `FacingTurnComponent`-driven turn animation/interpolation has finished, so they can trigger follow-up logic that depends on the entity now facing its target direction.

**Use-case:** `FacingTurnSystem` interpolates an entity's facing direction over time while it has a `FacingTurnComponent` (lerping from `From` to `To` based on `StartTurnTime`/`EndTurnTime`), and once the interpolation reaches its end (`delta >= 1`) it removes the component and sends this message (`e.SendFacingTurnCompleteMessage()`). Listen for it with `[Messager(typeof(FacingTurnCompleteMessage))]` to run logic that should only happen once the entity is fully facing its new direction, such as resuming movement or triggering an attack that was queued during the turn.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
