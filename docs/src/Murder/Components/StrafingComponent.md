# StrafingComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct StrafingComponent : IComponent
```

Marker component that enables lateral (strafing) movement for an agent, allowing it to move sideways while keeping its facing direction.

**Intent:** Opt an agent out of `AgentMoverSystem`'s default behavior of auto-facing the entity toward its movement impulse, so a movement system (or gameplay code) that has already set an explicit facing (e.g. always facing a target) can keep it while the agent still moves freely.

**Use-case:** Attach to enemy or player entities that should be able to side-step or circle around a target without turning to face their direction of travel. `AgentMoverSystem` checks `!e.HasStrafing()` (alongside `!e.HasFacingTurn()` and `AgentImpulseComponent.Flags`'s `IgnoreFacing` flag) before calling `Entity.SetFacing(impulse.Impulse.Angle())`; as long as `StrafingComponent` is present, the entity's facing is left untouched by movement and must be driven by something else (e.g. code that faces the entity toward its target every frame).

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

⚡
