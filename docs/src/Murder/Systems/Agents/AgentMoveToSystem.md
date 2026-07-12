# AgentMoveToSystem

**Namespace:** Murder.Systems.Agents \
**Assembly:** Murder.dll

```csharp
public class AgentMoveToSystem : IUpdateSystem, ISystem
```

Steers agent entities toward a destination declared with `MoveToComponent` (a fixed world position) or `MoveToTargetComponent` (another entity, optionally with an offset).

**Intent:** Turns a declarative "go to this point/entity" component into per-frame `AgentImpulseComponent` steering impulses, decelerating as the entity approaches its goal and clearing the move component once it arrives.

**Use-case:** Add `MoveToComponent` (with a target `Vector2`) or `MoveToTargetComponent` (with a target entity id) to any entity with a `PositionComponent`, and this system drives it there every frame. It does not itself move the entity or resolve collisions - the impulse it produces is consumed by the agent mover system and ultimately turned into velocity handled by the physics systems (e.g. [SATPhysicsSystem](../Physics/SATPhysicsSystem.html)). Entities tagged `AgentPauseComponent` or `AgentPauseRuntimeComponent` are skipped, as are entities configured to not move while off-camera.

**Implements:** _[IUpdateSystem](../../../Bang/Systems/IUpdateSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public AgentMoveToSystem()
```

### ⭐ Methods

#### Update(Context)

```csharp
public virtual void Update(Context context)
```

Advances every entity with a pending `MoveToComponent` or `MoveToTargetComponent` one frame closer to its destination. If a `MoveToMaxTimeComponent` timeout is present and has elapsed, the move is aborted and both components are removed. Otherwise the remaining distance to the target determines the behavior: within `MinDistance` the move completes and the component is removed; within `SlowDownDistance` the impulse ramps down (using `Calculator.Remap`) to avoid overshooting; beyond that, a full-strength impulse is applied toward the target. For `MoveToTargetComponent`, if the target entity no longer exists in the world, the move is cancelled and the component removed.

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
