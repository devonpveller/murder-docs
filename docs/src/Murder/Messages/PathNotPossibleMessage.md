# PathNotPossibleMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct PathNotPossibleMessage : IMessage
```

A marker message sent to an agent when the pathfinding system cannot compute a valid path to the requested destination.

**Intent:** Notify an agent that its current movement goal is unreachable so it can respond accordingly.

**Use-case:** `CalculatePathfindSystem` sends this (`e.SendMessage(new PathNotPossibleMessage())`) whenever `Map.FindPath` returns an empty path for an entity's `PathfindComponent`, right before removing the component and flagging `PathfindStatusFlags.PathNotFound` on it. Listen for this in agent AI or state-machine systems to handle navigation failures gracefully — for example by stopping movement, selecting an alternative waypoint, or falling back to an idle state when the target is unreachable.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
