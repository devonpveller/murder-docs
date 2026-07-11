# MoveToTargetComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct MoveToTargetComponent : IComponent
```

Instructs the agent movement system to steer the entity toward another entity identified by its runtime ID.

**Intent:** Drive an agent to follow or pursue a specific target entity, decelerating as it approaches.

**Use-case:** Add at runtime with the target entity's ID; the agent mover reads the target's current position each frame and moves the entity toward it, stopping within `MinDistance`.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public MoveToTargetComponent(int target, float minDistance, float slowDownDistance, Vector2 offset)
```

**Parameters** \
`target` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`minDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`slowDownDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`offset` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

```csharp
public MoveToTargetComponent(int target, float minDistance, float slowDownDistance)
```

**Parameters** \
`target` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \
`minDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`slowDownDistance` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### MinDistance
```csharp
public readonly float MinDistance;
```

Distance threshold (in pixels) at which the entity is considered to have reached the target and movement stops.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Offset
```csharp
public readonly Vector2 Offset;
```

Offset (in pixels) applied to the target entity's position, allowing the pursuer to stop slightly beside rather than directly on the target.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
#### SlowDownDistance
```csharp
public readonly float SlowDownDistance;
```

Distance (in pixels) from the target at which the entity begins decelerating.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### Target
```csharp
public readonly int Target;
```

Runtime entity ID of the entity to move toward.

**Returns** \
[int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \


⚡