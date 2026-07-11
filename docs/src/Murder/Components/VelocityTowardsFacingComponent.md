# VelocityTowardsFacingComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct VelocityTowardsFacingComponent : IComponent
```

Causes an entity to move at a constant speed in the direction it is currently facing.

**Intent:** Drive forward movement automatically from the entity's facing angle.

**Use-case:** Attach to projectiles, homing objects, or characters that always move forward; set `Velocity` to the desired forward speed in pixels per second.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors
```csharp
public VelocityTowardsFacingComponent()
```

### ⭐ Properties
#### Velocity
```csharp
public readonly float Velocity;
```

Forward speed in pixels per second; the movement system resolves the actual direction from the entity's facing angle.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡