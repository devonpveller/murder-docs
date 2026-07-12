# VerticalPhysicsSystem

**Namespace:** Murder.Systems.Physics \
**Assembly:** Murder.dll

```csharp
public class VerticalPhysicsSystem : IFixedUpdateSystem, ISystem
```

Simulates a fake third (height/"Z") axis for entities in an otherwise 2D top-down world.

**Intent:** Used for things like jump arcs, thrown/knocked-back objects and bouncing projectiles. Any entity carrying a `VerticalPositionComponent` has its `Z` height and `ZVelocity` advanced by a constant downward acceleration every fixed tick.

**Use-case:** Add `VerticalPositionComponent` to an entity to give it a height above the ground that decays back to zero under gravity, bouncing on impact. Per-entity `BounceAmountComponent` overrides the default bounciness/gravity scale, and `GravityMultiplierComponent` scales gravity (and, indirectly, bounciness) further - useful for lighter/heavier variants of the same projectile. Agents landing with a high downward velocity have their bounce halved so they don't keep bouncing indefinitely. Once the entity reaches the ground (`Z == 0`) a `TouchedGroundMessage` is sent every tick it stays grounded, and the component is removed entirely once vertical velocity has also settled to zero, returning the entity to plain 2D behavior. This system only integrates the height value itself; it does not affect the entity's X/Y position or collision (see [SATPhysicsSystem](SATPhysicsSystem.html) for that), though render systems commonly read `Z` to offset the sprite's draw position and simulate a jump.

**Implements:** _[IFixedUpdateSystem](../../../Bang/Systems/IFixedUpdateSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public VerticalPhysicsSystem()
```

### ⭐ Methods

#### FixedUpdate(Context)

```csharp
public virtual void FixedUpdate(Context context)
```

Advances the height (`Z`) and vertical velocity of every filtered entity by one fixed tick of gravity, applying any `BounceAmountComponent` or `GravityMultiplierComponent` overrides, sending `TouchedGroundMessage` when grounded, and removing the component once the entity comes to rest on the ground.

**Parameters** \
`context` [Context](../../../Bang/Contexts/Context.html) \

⚡
