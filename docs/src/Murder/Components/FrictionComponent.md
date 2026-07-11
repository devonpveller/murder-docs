# FrictionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FrictionComponent : IComponent
```

Applies a friction coefficient to an agent's velocity each frame, decelerating it to a stop.

**Intent:** Simulate ground and air friction so that agents naturally slow down when no movement input is applied.

**Use-case:** Add to any entity with an `AgentComponent` and set `Amount` between 0 (no friction) and values close to 1 (stops very quickly); optionally provide `AirFriction` for separate in-air deceleration.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public FrictionComponent(float amount)
```

**Parameters** \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Amount
```csharp
public readonly float Amount;
```

Friction coefficient applied while the agent is grounded. Higher values (closer to 1) cause the agent to stop faster; 0 applies no friction.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡