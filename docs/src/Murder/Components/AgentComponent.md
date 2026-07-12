# AgentComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentComponent : IComponent
```

Stores the movement parameters (speed, acceleration, friction) that drive an autonomous agent entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Defines the base movement tuning (top speed, acceleration, and friction/deceleration) that `AgentMoverSystem` uses when it converts an `AgentImpulseComponent` impulse into actual `Velocity` each frame.

**Use-case:** Attach alongside an `AgentImpulseComponent` to any entity that should be moved through the agent-based movement pipeline (player characters, NPCs, patrolling enemies, etc.). `AgentMoverSystem` filters for entities carrying both components; on entities also carrying `OverrideAgentSpeedComponent` or `AgentSpeedMultiplierComponent`, those override or scale this component's `Speed`/`Acceleration` for that frame without needing to mutate `AgentComponent` itself.

### ⭐ Constructors

```csharp
public AgentComponent(float speed, float acceleration, float friction)
```

Creates an `AgentComponent` with explicit speed, acceleration, and friction values.

**Parameters** \
`speed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`acceleration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`friction` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### Acceleration

```csharp
public readonly float Acceleration;
```

Rate at which the agent ramps up to maximum speed, in units per second squared.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Friction

```csharp
public readonly float Friction;
```

Per-axis multiplier applied to the agent's current velocity on any axis where the incoming impulse is zero or points opposite the current motion, gradually bringing that axis to a stop instead of reversing it instantly.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Speed

```csharp
public readonly float Speed;
```

Maximum speed of this agent

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
