# OverrideAgentSpeedComponent

**Namespace:** Murder.Components.Agents \
**Assembly:** Murder.dll

```csharp
public sealed struct OverrideAgentSpeedComponent : IComponent
```

Temporarily replaces an agent's maximum speed and, optionally, its acceleration while attached, without touching the entity's base [AgentComponent](../../../Murder/Components/AgentComponent.html).

**Implements:** _[IComponent](../../../Bang/Components/IComponent.html)_

**Intent:** Lets gameplay code impose a hard, temporary cap on an agent's movement parameters. `AgentMoverSystem` checks for this component every time it converts an agent's impulse into velocity, and if present, uses `MaxSpeed` (and `Acceleration`, if not left at its sentinel value) in place of the values on `AgentComponent`.

**Use-case:** Attach to an agent entity to slow it down (or change how quickly it ramps up to speed) during a scripted or status-driven situation — e.g. wading through mud, being slowed by a debuff, or a scripted "walk slowly" cutscene beat. Remove the component once the condition ends to restore the agent's original speed and acceleration.

### ⭐ Constructors

```csharp
public OverrideAgentSpeedComponent()
```

Default constructor. `MaxSpeed` is `0` and `Acceleration` is `-1` (meaning "keep the agent's original acceleration"), so adding this via the parameterless constructor effectively freezes the agent's speed to zero — prefer one of the other constructors for a meaningful override.

```csharp
public OverrideAgentSpeedComponent(float maxSpeed)
```

Creates an override that replaces only the agent's maximum speed, leaving its original acceleration untouched.

**Parameters** \
`maxSpeed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — the speed cap to enforce while this component is present. \

```csharp
public OverrideAgentSpeedComponent(float maxSpeed, float acceleration)
```

Creates an override that replaces both the agent's maximum speed and its acceleration.

**Parameters** \
`maxSpeed` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — the speed cap to enforce while this component is present. \
`acceleration` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) — the acceleration to enforce while this component is present. \

### ⭐ Properties

#### Acceleration

```csharp
public readonly float Acceleration;
```

Overriding acceleration value to apply instead of the agent's `AgentComponent.Acceleration`. The default value of `-1` is a sentinel meaning "no override" — `AgentMoverSystem` only substitutes this value when it is not `-1`.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### MaxSpeed

```csharp
public readonly float MaxSpeed;
```

The maximum speed cap that replaces the agent's base `AgentComponent.Speed` while this component is present.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
