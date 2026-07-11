# MuteEventsComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct MuteEventsComponent : IComponent
```

This will block any [EventListenerComponent](../../Murder/Components/EventListenerComponent.html) from being sent.

**Intent:** Prevent the entity from emitting sound events so that its animations or actions play silently.

**Use-case:** Add to an entity during scripted sequences or cutscenes where sound effects should be suppressed; remove the component to restore normal event broadcasting.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡