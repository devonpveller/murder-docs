# PathNotPossibleMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct PathNotPossibleMessage : IMessage
```

A marker message sent to an agent when the pathfinding system cannot compute a valid path to the requested destination.

**Intent:** Notify an agent that its current movement goal is unreachable so it can respond accordingly.

**Use-case:** Listen for this in agent AI systems to handle navigation failures gracefully—for example by stopping movement, selecting an alternative waypoint, or triggering an idle state when the target is blocked.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_



⚡