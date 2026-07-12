# VelocityTowardsFacingSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class VelocityTowardsFacingSystem : IReactiveSystem, ISystem
```

Converts a `VelocityTowardsFacingComponent` into a world-space velocity vector aligned with the entity's current facing angle, then removes the component.

**Intent:** Translates a magnitude-based impulse into a directional velocity oriented along the entity's facing direction in a single reactive step.

**Use-case:** Use when you want to fire a projectile or dash an agent in the direction they are currently facing without manually computing the angle vector.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public VelocityTowardsFacingSystem()
```

### ⭐ Methods

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

For each entity that gained a `VelocityTowardsFacingComponent`, computes a velocity vector from the component's magnitude and the entity's current `FacingComponent.Angle` (using sine/cosine so `0` faces along the Y axis), applies it via `Entity.SetVelocity`, then immediately removes the `VelocityTowardsFacingComponent` since it is a one-shot instruction rather than persistent state.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

No-op; `OnAdded` always removes the component in the same reactive step it is processed, so `VelocityTowardsFacingComponent` is never expected to be modified while present on an entity.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

No-op; there is nothing left to clean up once `VelocityTowardsFacingComponent` is removed; the resulting `VelocityComponent` this system set in `OnAdded` is left in place for physics/movement systems to consume.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
