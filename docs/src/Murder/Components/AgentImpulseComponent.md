# AgentImpulseComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct AgentImpulseComponent : IComponent
```

Carries a one-frame velocity impulse and optional facing direction for an agent entity.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Delivers a movement impulse to the `AgentMoverSystem` for a single simulation step, then is cleared automatically.

**Use-case:** Attach (or replace) this component each frame to drive agent movement — for example from a player input system that converts stick input into a velocity vector.

### ⭐ Constructors
```csharp
public AgentImpulseComponent(Vector2 impulse, T? direction)
```

Creates an impulse with an explicit desired facing direction.

**Parameters** \
`impulse` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \
`direction` [T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

```csharp
public AgentImpulseComponent(Vector2 impulse)
```

Creates an impulse; the facing direction is inferred from the impulse vector.

**Parameters** \
`impulse` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties
#### Direction
```csharp
public readonly T? Direction;
```

The desired facing direction for the agent this frame; `null` means direction is derived from the impulse vector.

**Returns** \
[T?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \
#### Impulse
```csharp
public readonly Vector2 Impulse;
```

The velocity impulse to apply to the agent this frame.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \


⚡