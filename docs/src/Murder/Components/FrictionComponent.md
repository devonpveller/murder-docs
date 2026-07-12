# FrictionComponent

**Namespace:** Murder.Components \
**Assembly:** Murder.dll

```csharp
public sealed struct FrictionComponent : IComponent
```

Decelerates an entity's velocity every fixed update, applied by `FrictionSystem`. Requires the entity to also have a `VelocityComponent` (the system filters on both).

**Intent:** Simulate ground and, optionally, separate air friction so that agents naturally slow down when no movement input is applied, without every gameplay system needing to manually decay velocity.

**Use-case:** Add to any entity with a `VelocityComponent` (e.g. one with an `AgentComponent`) and set `Amount` between 0 (no friction) and values close to 1 (stops very quickly). `FrictionSystem` also special-cases entities inside an `InsideGravityWellComponent`, applying friction only to the component of velocity perpendicular to (or moving away from) the well so orbiting motion isn't killed. Provide `AirFriction` if the entity should decelerate differently while airborne (its `VerticalPositionComponent.Z` is greater than zero); otherwise `Amount` is used for both grounded and airborne friction.

**Implements:** _[IComponent](../../Bang/Components/IComponent.html)_

### ⭐ Constructors

```csharp
public FrictionComponent(float amount)
```

Creates a friction component that applies the same friction amount whether the entity is grounded or airborne. High friction means stopping fast.

**Parameters** \
`amount` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

```csharp
public FrictionComponent(float ground, float air)
```

Creates a friction component with distinct grounded and airborne friction coefficients.

**Parameters** \
`ground` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \
`air` [float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

### ⭐ Properties

#### AirFriction

```csharp
public readonly float? AirFriction;
```

Optional friction amount applied while the entity is airborne (its `VerticalPositionComponent` has a positive Z). When `null`, `Amount` is used for both grounded and airborne friction; 0 never stops the entity, values close to 1 stop it very fast.

**Returns** \
[float?](https://learn.microsoft.com/en-us/dotnet/api/System.Nullable-1?view=net-7.0) \

#### Amount

```csharp
public readonly float Amount;
```

Friction coefficient applied while the agent is grounded (and used as the airborne fallback when `AirFriction` is not set). Higher values (closer to 1) cause the agent to stop faster; 0 applies no friction.

**Returns** \
[float](https://learn.microsoft.com/en-us/dotnet/api/System.Single?view=net-7.0) \

⚡
