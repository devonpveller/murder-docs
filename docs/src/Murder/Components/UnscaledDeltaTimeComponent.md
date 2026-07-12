# UnscaledDeltaTimeComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct UnscaledDeltaTimeComponent : IComponent
```

Used when calculating time for [StateMachine](../../Bang/StateMachines/StateMachine.html).

**Intent:** Signal that a state machine on this entity should be ticked with real (unscaled) delta time rather than the normal, pause/time-scale-affected delta time.

**Use-case:** Attach to entities whose state machine logic must keep advancing at real-world speed even while the game is paused or slowed down — for example UI controllers, menus, or cutscene/dialogue drivers that should still respond during a pause screen. `StateMachineSystem` checks for this marker component and, when present, ticks the entity's `StateMachine` with `Game.UnscaledDeltaTime` instead of `Game.DeltaTime`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡
