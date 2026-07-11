# OnInteractExitMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct OnInteractExitMessage : IMessage
```

Generic struct for notifying that an interaction exit has occurred.

**Intent:** Signal to a previously-interacted entity that the interacting entity has ended its interaction or moved away.

**Use-case:** Send this when the player leaves an interactive trigger or explicitly cancels an ongoing interaction. Listening systems can then reset UI prompts, close menus, or deactivate any state that was active during the interaction.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_



⚡