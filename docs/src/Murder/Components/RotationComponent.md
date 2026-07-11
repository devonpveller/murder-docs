# RotationComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct RotationComponent : IComponent
```

Stores the rotation of an entity as an angle in radians.

**Intent:** Track a free-rotation angle that is independent of the entity's facing direction.

**Use-case:** Attach to projectiles, particles, or objects that spin freely; read `Rotation` each frame to apply the angle to the sprite or collider transform.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public RotationComponent()
```

```csharp
public RotationComponent(float rotation)
```

**Parameters** \
`rotation` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Rotation
```csharp
public readonly float Rotation;
```

In radians.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡