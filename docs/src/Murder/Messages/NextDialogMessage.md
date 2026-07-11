# NextDialogMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct NextDialogMessage : IMessage
```

A marker message with no payload sent to advance the current dialogue to its next line or node.

**Intent:** Trigger progression to the next step in a running dialogue sequence.

**Use-case:** Send this from input systems when the player presses the advance button during a cutscene or conversation. The dialogue system listens for it and moves the dialogue state machine forward to display the next line.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_



⚡