# UnscaledDeltaTimeComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct UnscaledDeltaTimeComponent : IComponent
```

Used when calculating time for [StateMachine](../../Bang/StateMachines/StateMachine.html).

**Intent:** Signal that a state machine on this entity should use real (unscaled) delta time rather than game-scaled time.

**Use-case:** Attach to entities whose state machines must advance at real-world speed even when the game is paused or slowed (e.g. UI elements or cutscene controllers).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_



⚡