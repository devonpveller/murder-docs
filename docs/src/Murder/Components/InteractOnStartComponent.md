# InteractOnStartComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct InteractOnStartComponent : IComponent
```

Triggers the entity's interactive components once when the entity is first added to the world.

**Intent:** Run an interaction at world-load time, such as applying initial state changes or starting a cutscene, without requiring any player input or external trigger.

**Use-case:** Add to entities that should execute an interaction immediately on spawn (e.g. a level intro sequence, an auto-opening door, or a one-time spawn effect).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡