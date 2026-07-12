# SATPhysicsSystem

**Namespace:** Murder.Systems.Physics \
**Assembly:** Murder.dll

```csharp
public class SATPhysicsSystem : IFixedUpdateSystem, ISystem
```

Moves every entity that has a `VelocityComponent` and resolves collisions against solid geometry using the Separating Axis Theorem.

**Intent:** This is the core solid-body mover for gameplay entities: it advances each entity toward `Position + Velocity * FixedDeltaTime`, repeatedly applying the minimum translation vector (MTV) returned by collision checks against nearby colliders until no more overlaps are found, sliding the entity along the collision edge (or fully stopping it, if it carries `StopOnCollisionComponent`) rather than passing through solid geometry.

**Use-case:** Add to any world that needs solid physics resolution between entities with `ColliderComponent` on the `ACTOR` layer and tiles/other colliders on the `SOLID`/`HOLE` layers. Large velocities are automatically swept in smaller steps (based on `GameProfile.MinimumVelocityForSweep`) to avoid tunneling through thin colliders at high speed. Entities without a collider, without the `ACTOR` layer, or explicitly marked with `FreeMovementComponent` skip collision checks and move unobstructed (unless `FreeMovementFlags.RespectTiles` is set). On collision, a `CollidedWithMessage` is sent to notify listeners. This system is distinct from [TriggerPhysicsSystem](TriggerPhysicsSystem.html), which only detects overlaps and never moves anything.

**Implements:** _[IFixedUpdateSystem](../../../Bang/Systems/IFixedUpdateSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public SATPhysicsSystem()
```

### ⭐ Methods

#### FixedUpdate(Context)

```csharp
public virtual void FixedUpdate(Context context)
```

Steps every filtered entity's position by its current velocity for this fixed tick, resolving solid collisions via SAT/MTV pushout, sliding along obstacles, and zeroing out velocity that has decayed below a small threshold (rounding the entity's position to avoid long-term jittering).

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
