# MoveToComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct MoveToComponent : IComponent
```

Instructs the agent movement system to steer the entity toward a target world-space position.

**Intent:** Drive an agent to move toward a fixed point in the world, decelerating as it approaches the destination.

**Use-case:** Add at runtime with the desired `Target` position; the agent mover system applies steering velocity each frame and removes the component once the entity is within `MinDistance` of the target.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public MoveToComponent(Vector2& target, float minDistance, float slowDownDistance)
```

**Parameters** \
`target` [Vector2&](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`minDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`slowDownDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public MoveToComponent(Vector2& target)
```

**Parameters** \
`target` [Vector2&](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### MinDistance

```csharp
public readonly float MinDistance;
```

Distance threshold (in pixels) at which the entity is considered to have reached its target and movement stops.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### SlowDownDistance

```csharp
public readonly float SlowDownDistance;
```

Distance (in pixels) from the target at which the agent begins decelerating to avoid overshooting.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

#### Target

```csharp
public readonly Vector2 Target;
```

World-space position the entity should move toward.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
