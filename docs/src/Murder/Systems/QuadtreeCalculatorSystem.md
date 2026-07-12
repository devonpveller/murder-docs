# QuadtreeCalculatorSystem

**Namespace:** Murder.Systems \
**Assembly:** Murder.dll

```csharp
public class QuadtreeCalculatorSystem : IReactiveSystem, IStartupSystem, ISystem
```

Filtered and watched on `PositionComponent`/`ColliderComponent`. Maintains the world's spatial `Quadtree` by batching up which entities need to be inserted/updated/removed as their position or collider changes, then applying the whole batch at once in `OnAfterTrigger`.

**Intent:** Keeps the world's spatial index (used for broad-phase collision queries, physics, and "what's near this point" gameplay queries) accurate and up to date, without doing a quadtree update per individual entity event — all of a trigger step's changes are coalesced into two hash sets and flushed once per frame, which is much cheaper than re-indexing entities one at a time.

**Use-case:** Must be present in any world that uses collision detection or spatial queries; systems like the physics/trigger systems and `PushAwayComponent` handling read from `Quadtree.GetOrCreateUnique(world)`, which this system is responsible for populating and keeping current.

**Implements:** _[IReactiveSystem](../../Bang/Systems/IReactiveSystem.html), [IStartupSystem](../../Bang/Systems/IStartupSystem.html), [ISystem](../../Bang/Systems/ISystem.html)_

### ⭐ Constructors

```csharp
public QuadtreeCalculatorSystem()
```

### ⭐ Methods

#### Start(Context)

```csharp
public virtual void Start(Context context)
```

Queues every entity already present in the filter (has both `PositionComponent` and `ColliderComponent`) for insertion, so the quadtree is fully populated before the first frame runs. The actual insertion happens afterwards in `OnAfterTrigger`.

**Parameters** \
`context` [Context](../../Bang/Contexts/Context.html) \

#### OnActivated(World, ImmutableArray<T>)

```csharp
public virtual void OnActivated(World world, ImmutableArray<T> entities)
```

Queues reactivated entities to be (re-)inserted into the spatial quadtree.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnAdded(World, ImmutableArray<T>)

```csharp
public virtual void OnAdded(World world, ImmutableArray<T> entities)
```

Queues newly added entities to be inserted into the spatial quadtree.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnDeactivated(World, ImmutableArray<T>)

```csharp
public virtual void OnDeactivated(World world, ImmutableArray<T> entities)
```

Queues deactivated entities for removal from the quadtree so they are excluded from spatial queries.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnModified(World, ImmutableArray<T>)

```csharp
public virtual void OnModified(World world, ImmutableArray<T> entities)
```

Queues each entity whose position or collider changed for a bounding-box update in the quadtree.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnRemoved(World, ImmutableArray<T>)

```csharp
public virtual void OnRemoved(World world, ImmutableArray<T> entities)
```

Queues destroyed (or no-longer-matching) entities for removal from the quadtree.

**Parameters** \
`world` [World](../../Bang/World.html) \
`entities` [ImmutableArray\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Immutable.ImmutableArray-1?view=net-7.0) \

#### OnAfterTrigger(World)

```csharp
public virtual void OnAfterTrigger(World world)
```

Flushes the batched changes queued by this frame's `OnAdded`/`OnModified`/`OnActivated`/`OnRemoved`/`OnDeactivated`/`Start` calls into the world's `Quadtree`: entities queued for removal are dropped from the collision quadtree; entities queued for update are re-validated (still active, still has a `ColliderComponent`) and have their collision bounding box (and, if present, their `PushAwayComponent` bounds) refreshed in the tree. Does nothing if no changes were queued.

**Parameters** \
`world` [World](../../Bang/World.html) \

⚡
