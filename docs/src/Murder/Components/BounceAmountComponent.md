# BounceAmountComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct BounceAmountComponent : IComponent
```

Defines the bounciness and gravity modifier for an entity that should rebound off surfaces.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

**Intent:** Overrides `VerticalPhysicsSystem`'s default bounce/gravity values (`0.6` bounciness, `1.0` gravity) for a specific entity, letting different objects fall and bounce with different feel along the Z (vertical/height) axis.

**Use-case:** Attach alongside a [VerticalPositionComponent](../../Murder/Components/VerticalPositionComponent.html) to any entity that needs custom vertical physics — for example a ball that should bounce higher (`Bounciness` closer to `1.0`) or a heavy crate that should barely bounce at all (`Bounciness` near `0`). `GravityMod` is also multiplied into `Bounciness` by `VerticalPhysicsSystem`, so raising it makes the object both fall and bounce more energetically. Without this component, `VerticalPhysicsSystem` uses its built-in defaults for any entity with a `VerticalPositionComponent`.

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
