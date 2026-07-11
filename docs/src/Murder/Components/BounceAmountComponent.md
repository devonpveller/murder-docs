# BounceAmountComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct BounceAmountComponent : IComponent
```

Defines the bounciness and gravity modifier for an entity that should rebound off surfaces.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Parameterizes the bounce physics applied to a projectile or physics object when it collides with a surface.

**Use-case:** Attach to a projectile or thrown object; the physics system reads `Bounciness` to scale the reflected velocity and `GravityMod` to adjust how quickly gravity pulls it back down.

### ⭐ Constructors
```csharp
public BounceAmountComponent(float bounciness, float gravity)
```

**Parameters** \
`bounciness` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`gravity` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties
#### Bounciness
```csharp
public readonly float Bounciness;
```

Fraction of velocity retained after bouncing; `1.0` is a perfect bounce, `0.0` means no rebound.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
#### GravityMod
```csharp
public readonly float GravityMod;
```

Multiplier applied to the global gravity constant for this entity; `1.0` is normal gravity.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \


⚡