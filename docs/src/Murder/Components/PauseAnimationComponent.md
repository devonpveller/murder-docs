# PauseAnimationComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct PauseAnimationComponent : IComponent
```

Struct to describe an entity that will not never have its animation paused.

**Intent:** Mark an entity whose animation should be frozen at its current frame, preventing it from advancing.

**Use-case:** Add to an entity when you need to freeze its animation (e.g. during a cutscene or a freeze effect); remove the component to resume normal playback.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡