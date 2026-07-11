# AgentComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentComponent : IComponent
```

Stores the movement parameters (speed, acceleration, friction) that drive an autonomous agent entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Defines how fast an agent can move and how quickly it ramps up or slows down.

**Use-case:** Attach to any entity that should be controlled by `AgentMoverSystem`. Tune `Speed`, `Acceleration`, and `Friction` to match the desired movement feel for that entity.

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

Deceleration factor applied each frame when the agent has no input, bringing it to a stop.

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