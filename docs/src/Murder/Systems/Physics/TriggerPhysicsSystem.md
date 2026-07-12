# TriggerPhysicsSystem

**Namespace:** Murder.Systems.Physics \
**Assembly:** Murder.dll

```csharp
public class TriggerPhysicsSystem : IReactiveSystem, IMessagerSystem, ISystem
```

Detects overlaps between trigger-layer colliders and actor/hitbox colliders and reports them as `OnCollisionMessage` enter/exit events.

**Intent:** Unlike [SATPhysicsSystem](SATPhysicsSystem.html), this system never moves anything - it only figures out which pairs of entities are currently overlapping and notifies both sides via messages. Only two pairings are considered valid: an `ACTOR`/`HITBOX` collider overlapping a `TRIGGER` collider (trigger-vs-trigger and actor-vs-actor pairs are ignored).

**Use-case:** Add `ColliderComponent` with the `TRIGGER` layer to area entities (pickup zones, area events, cutscene triggers) and this system automatically sends `OnCollisionMessage` with `CollisionDirection.Enter`/`Exit` to both the trigger and the actor/hitbox that entered or left it. It depends on `QuadtreeCalculatorSystem` having already rebuilt the quadtree for the frame. Every entity whose `PositionComponent` is watched (added/modified/removed/(de)activated) is queued and re-checked once per frame, diffing the result against each entity's `CollisionCacheComponent`. Deactivated, destroyed or removed entities are treated as an implicit "exit" for everything they were previously colliding with. The system also listens for `OnBeforeReplaceMessage` so that, right before a component replace wipes out the collision cache, exit messages are still sent for every entity it was colliding with.

**Implements:** _[IReactiveSystem](../../../Bang/Systems/IReactiveSystem.html), [IMessagerSystem](../../../Bang/Systems/IMessagerSystem.html), [ISystem](../../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public TriggerPhysicsSystem()
```

### ⭐ Methods

#### OnActivated(World, ImmutableArray<T>)

```csharp
public virtual void OnActivated(World world, ImmutableArray<T> entities)
```

Queues reactivated entities to be re-checked for trigger overlaps at the end of the frame.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Queues newly added entities to be checked for trigger overlaps at the end of the frame.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnAfterTrigger(World)

```csharp
public virtual void OnAfterTrigger(World world)
```

Runs once per frame, after all of this frame's `OnAdded`/`OnRemoved`/`OnModified`/`OnActivated`/`OnDeactivated` notifications, and performs the actual (expensive) trigger-overlap checks for every entity queued during the frame. Inactive or destroyed entities are cleared out of the collision cache with exit messages; active entities are re-checked against the quadtree. The watch list is cleared afterwards so the same entity is only checked once even if it changed multiple times this frame.

**Parameters** \
`world` [World](../../../Bang/World.html) \

#### OnDeactivated(World, ImmutableArray<T>)

```csharp
public virtual void OnDeactivated(World world, ImmutableArray<T> entities)
```

Queues deactivated entities to be re-checked at the end of the frame, where they are treated as having exited every trigger they were previously overlapping.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnMessage(World, Entity, IMessage)

```csharp
public virtual void OnMessage(World world, Entity entity, IMessage message)
```

Handles `OnBeforeReplaceMessage`: right before the entity's components are wiped out by a replace, sends an exit collision message for every entity currently in its collision cache so listeners don't miss the exit just because the cache is about to disappear.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entity` [Entity](../../../Bang/Entities/Entity.html) \
`message` [IMessage](../../../Bang/Components/IMessage.html) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Queues entities whose `PositionComponent` moved to be re-checked for trigger overlaps at the end of the frame.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Queues removed entities to be re-checked at the end of the frame; if the entity was already destroyed, exit messages are sent immediately instead of waiting for the batch.

**Parameters** \
`world` [World](../../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

⚡
