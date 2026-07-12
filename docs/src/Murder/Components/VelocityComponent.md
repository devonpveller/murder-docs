# VelocityComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct VelocityComponent : IComponent
```

Stores the current per-frame translational velocity of an entity.

**Intent:** Represent the current translational velocity of an entity in world space so physics/movement systems can integrate it into position, rather than the entity's position being set directly every frame.

**Use-case:** Attach to any entity that should move under a velocity-driven simulation. `SATPhysicsSystem` integrates `Velocity * Game.FixedDeltaTime` into the entity's position every fixed tick and resolves collisions along the way; friction, tethering, and facing-based movement systems (e.g. [VelocityTowardsFacingComponent](../../Murder/Components/VelocityTowardsFacingComponent.html)) read or write this component to influence that motion.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public VelocityComponent(float x, float y)
```

Creates a component with the given velocity components.

**Parameters** \
`x` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`y` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public VelocityComponent(Vector2 velocity)
```

Creates a component with the given velocity vector.

**Parameters** \
`velocity` [Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

### ⭐ Properties

#### Velocity

```csharp
public readonly Vector2 Velocity;
```

Current velocity of the entity, in pixels per second.

**Returns** \
[Vector2](https://learn.microsoft.com/en-us/dotnet/api/System.Numerics.Vector2?view=net-7.0) \

⚡
