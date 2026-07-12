# DoNotPauseComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct DoNotPauseComponent : IComponent
```

Marker component that exempts an entity's systems from being suspended when the game is paused.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Keeps selected entities ticking even when the rest of the world is frozen by a pause. On its own this component does nothing — it only has an effect when a system explicitly filters for it in combination with `[OnPause]`, so that system's `Update` keeps being called while the world is paused.

**Use-case:** `StateMachineOnPauseSystem` filters for entities that have both `IStateMachineComponent` and `DoNotPauseComponent`; state machines on such entities keep ticking with unscaled delta time even while the world is paused. Attach this to any entity whose state machine (or other `[OnPause]`-aware logic) must keep running during a pause menu, such as UI routines or background audio state machines. Note the type itself also carries `[DoNotPersistOnSave]`, so the marker is not written into save files.

⚡
