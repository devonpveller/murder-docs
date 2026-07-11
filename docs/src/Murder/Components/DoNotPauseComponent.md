# DoNotPauseComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DoNotPauseComponent : IComponent
```

Marker component that exempts an entity's systems from being suspended when the game is paused.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Keeps selected entities (e.g., UI, pause-menu animations, state machines) ticking even when the rest of the world is frozen.

**Use-case:** Attach to any entity that must remain active during a pause state, such as menu screens, countdown timers, or audio state machines.



⚡