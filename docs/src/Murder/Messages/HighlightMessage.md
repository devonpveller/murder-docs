# HighlightMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct HighlightMessage : IMessage
```

A marker message with no payload sent to request that the receiving entity be visually highlighted.

**Intent:** Signal that an entity should enter a highlighted visual state, such as when the player hovers over or targets it.

**Use-case:** Send this from an input or interaction system when the player's cursor enters an interactive entity. A rendering system listening for this message can then apply an outline or color tint to indicate interactability.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_



⚡