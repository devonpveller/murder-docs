# HighlightMessage

**Namespace:** Murder.Messages \
**Assembly:** Murder.dll

```csharp
public sealed struct HighlightMessage : IMessage
```

A marker message with no payload, intended to request that the receiving entity be visually highlighted.

**Intent:** Provide a lightweight, payload-free signal that an entity should enter a highlighted visual state, such as when the player hovers over or targets it. This is distinct from the engine's own highlight machinery ([HighlightSpriteComponent](../../Murder/Components/HighlightSpriteComponent.html) / [HighlightOnChildrenComponent](../../Murder/Components/HighlightOnChildrenComponent.html) and `EffectsServices`), which drives sprite outline rendering directly through components rather than this message — no built-in system currently listens for `HighlightMessage`.

**Use-case:** Send this from game-specific input or interaction code when the player's cursor or selection enters an interactive entity, and pair it with a game-specific `[Messager(typeof(HighlightMessage))]` system that reacts by adding/removing the actual highlight component (e.g. `HighlightSpriteComponent`) or otherwise driving a highlight visual.

**Implements:** _[IMessage](../../Bang/Components/IMessage.html)_

⚡
