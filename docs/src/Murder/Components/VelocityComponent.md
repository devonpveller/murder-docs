# VelocityComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct VelocityComponent : IComponent
```

Stores the per-frame velocity vector applied to an entity's position by the movement system.

**Intent:** Represent the current translational velocity of an entity in world space.

**Use-case:** Attach to any entity that moves via the velocity-driven movement pipeline; set `Velocity` to the desired speed vector each frame or via impulse.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public VelocityComponent(float x, float y)
```

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public VelocityComponent(Vector2 velocity)
```

**Parameters** \
`velocity` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties
#### Velocity
```csharp
public readonly Vector2 Velocity;
```

Current velocity of the entity in pixels per second.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \


⚡