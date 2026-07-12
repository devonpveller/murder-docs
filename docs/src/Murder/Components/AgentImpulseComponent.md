# AgentImpulseComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public readonly struct AgentImpulseComponent : IComponent
```

Carries the desired movement impulse (and optional facing override) that `AgentMoverSystem` reads and converts into `Velocity` for an agent entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Acts as the input channel between "something wants this agent to move" (player input, AI steering, a cutscene, etc.) and the actual physics velocity. `AgentMoverSystem` filters for entities with both `AgentComponent` and `AgentImpulseComponent`, applies friction/speed/acceleration from `AgentComponent`, and writes the resulting `Velocity` component.

**Use-case:** Set (or replace) this component every frame from whatever system decides how the agent should move — for example a player-input system converting stick/keyboard input into a normalized direction, or an AI system steering toward a target. `AgentCleanupSystem` automatically removes this component at the end of the frame once its impulse is no longer needed (i.e. it decays below the agent's speed and friction has fully applied), unless `AgentImpulseFlags.DoNotClear` is set, in which case the caller is responsible for removing it explicitly.

### ⭐ Constructors

```csharp
public AgentImpulseComponent(Vector2 impulse, Direction? direction, AgentImpulseFlags flags)
```

The primary constructor: sets the raw impulse vector, an explicit facing direction override, and behavior flags directly.

**Parameters** \
`impulse` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`direction` [Direction?](../../Murder/Helpers/Direction.html) \
`flags` [AgentImpulseFlags](../../Murder/Components/Agents/AgentImpulseFlags.html) \

```csharp
public AgentImpulseComponent(Vector2 impulse)
```

Creates an impulse with no flags; the facing direction is inferred from the impulse vector via `DirectionHelper.FromVector`.

**Parameters** \
`impulse` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public AgentImpulseComponent(Vector2 impulse, AgentImpulseFlags flags)
```

Creates an impulse with explicit flags; the facing direction is still inferred from the impulse vector.

**Parameters** \
`impulse` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`flags` [AgentImpulseFlags](../../Murder/Components/Agents/AgentImpulseFlags.html) \

```csharp
public AgentImpulseComponent(Vector2 impulse, Direction? direction)
```

Creates an impulse with an explicit facing direction override and no flags.

**Parameters** \
`impulse` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`direction` [Direction?](../../Murder/Helpers/Direction.html) \

```csharp
public AgentImpulseComponent(Direction direction, AgentImpulseFlags flags)
```

Creates an impulse purely from a discrete `Direction` (converted to a unit `Vector2` via `DirectionHelper.ToVector`) — convenient for grid-aligned or 8-way movement input.

**Parameters** \
`direction` [Direction](../../Murder/Helpers/Direction.html) \
`flags` [AgentImpulseFlags](../../Murder/Components/Agents/AgentImpulseFlags.html) \

### ⭐ Properties

#### Impulse

```csharp
public readonly Vector2 Impulse;
```

The raw movement vector for this frame. `AgentMoverSystem` combines its direction/magnitude with `AgentComponent.Speed`, `Acceleration`, and any active `AgentSpeedMultiplierComponent`/`OverrideAgentSpeedComponent` to produce the agent's `Velocity`. A zero vector means "no impulse this frame" and only friction is applied.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

#### Direction

```csharp
public readonly Direction? Direction;
```

Optional explicit facing direction for the agent this frame. When `null`, the engine falls back to deriving direction from `Impulse` itself; when set, it takes precedence (unless `AgentImpulseFlags.IgnoreFacing` is set, in which case `AgentMoverSystem` does not update the entity's `FacingComponent` at all).

**Returns** \
[Direction?](../../Murder/Helpers/Direction.html) \

#### Flags

```csharp
public readonly AgentImpulseFlags Flags;
```

Behavior modifiers for how this impulse is consumed by `AgentMoverSystem` — see `AgentImpulseFlags.DoNotClear` and `AgentImpulseFlags.IgnoreFacing`.

**Returns** \
[AgentImpulseFlags](../../Murder/Components/Agents/AgentImpulseFlags.html) \

⚡
