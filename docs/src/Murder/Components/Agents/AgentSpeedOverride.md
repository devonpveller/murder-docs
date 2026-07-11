# AgentSpeedOverride

**Namespace:** Murder.Components.Agents \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentSpeedOverride : IComponent
```

Temporarily overrides an agent's maximum speed and acceleration for the current frame or until removed.

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Allows runtime systems to impose a hard cap on agent movement parameters, ignoring the base `AgentComponent` values.

**Use-case:** Attach to an entity to slow it down during a scripted event (e.g., wading through mud), then remove it when the condition ends.

### ⭐ Constructors
```csharp
public AgentSpeedOverride()
```

```csharp
public AgentSpeedOverride(float maxSpeed, float acceleration)
```

Creates an override with the specified speed cap and acceleration.

**Parameters** \
`maxSpeed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`acceleration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Acceleration
```csharp
public readonly float Acceleration;
```

Overriding acceleration value to apply instead of the agent's default.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### MaxSpeed
```csharp
public readonly float MaxSpeed;
```

The maximum speed cap that replaces the agent's base `Speed` value while this component is present.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡