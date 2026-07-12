# NextDialogMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct NextDialogMessage : IMessage
```

A marker message with no payload sent to advance the current dialogue to its next line or node.

**Intent:** Trigger progression to the next step in a running dialogue sequence.

**Use-case:** `DialogStateMachine.Talk()` publishes the current dialogue line as a `LineComponent` and then suspends itself with `Wait.ForMessage<NextDialogMessage>()` whenever the line is a text line. Send this message to the dialogue entity (e.g. from a UI/input system when the player presses the "advance" button) to resume the state machine and move on to the character's next line. It has no payload — its mere arrival is the entire signal.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
