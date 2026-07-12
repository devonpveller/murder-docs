# Quadtree

**Namespace:** Murder.Core.Physics \
**Assembly:** Murder.dll

```csharp
public class Quadtree
```

The engine's primary broad-phase spatial acceleration structure. Maintains three separate `QTNode<T>` trees — `Collision`, `PushAway` and `StaticRender` — so unrelated queries (physical collision, soft push-away separation, and render culling) don't contend with each other or carry payload data they don't need.

**Intent:** There is one `Quadtree` per world, stored on a unique `QuadtreeComponent` and retrieved via `GetOrCreateUnique`; physics systems (`QuadtreeCalculatorSystem`, `SATPhysicsSystem`, etc.) keep it up to date every frame.

**Use-case:** Retrieved via `Quadtree.GetOrCreateUnique(world)` in physics systems; add entities with `AddToCollisionQuadTree` / `AddToStaticRenderQuadTree` and query with `GetCollisionEntitiesAt` to find potential collision candidates.

### ⭐ Constructors

```csharp
public Quadtree(Rectangle mapBounds)
```

Creates a `Quadtree` whose three partitions all cover the given world-space `mapBounds` rectangle.

**Parameters** \
`mapBounds` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \

### ⭐ Properties

#### Collision

```csharp
public readonly QTNode<T> Collision;
```

Quadtree partition indexing every entity with a collider, keyed by `Entity`. Queried by `GetCollisionEntitiesAt` and the physics systems that resolve collisions.

**Returns** \
[QTNode\<T\>](../../../Murder/Core/Physics/QTNode-1.html) \

#### PushAway

```csharp
public readonly QTNode<T> PushAway;
```

Quadtree partition indexing entities with a `PushAwayComponent`, used to softly separate overlapping actors (their position, push-away settings and velocity are cached alongside the entity to avoid extra lookups).

**Returns** \
[QTNode\<T\>](../../../Murder/Core/Physics/QTNode-1.html) \

#### StaticRender

```csharp
public readonly QTNode<T> StaticRender;
```

Quadtree partition indexing static, sprite-rendered entities (their sprite and render position are cached alongside the entity), used to cull off-screen entities during rendering.

**Returns** \
[QTNode\<T\>](../../../Murder/Core/Physics/QTNode-1.html) \

### ⭐ Methods

#### GetOrCreateUnique(World)

```csharp
public Quadtree GetOrCreateUnique(World world)
```

Retrieves the world's unique `Quadtree`, creating and registering a new `QuadtreeComponent` for it if one doesn't exist yet. The size for a freshly-created quadtree is derived from the unique map's dimensions, or a fallback 2000x2000 area with a warning if no map exists yet. This is the standard way for physics/AI systems to get hold of the world's quadtree.

**Parameters** \
`world` [World](../../../Bang/World.html) \

**Returns** \
[Quadtree](../../../Murder/Core/Physics/Quadtree.html) \

#### AddToCollisionQuadTree(Entity)

```csharp
public void AddToCollisionQuadTree(Entity entity)
```

Inserts a single active `entity` into the `Collision` partition (if it has a collider) and, if it also has a `PushAwayComponent`, into the `PushAway` partition as well.

**Parameters** \
`entity` [Entity](../../../Bang/Entities/Entity.html) \

#### AddToCollisionQuadTree(IEnumerable<Entity>)

```csharp
public void AddToCollisionQuadTree(IEnumerable<T> entities)
```

Inserts every active entity in `entities` into the collision/push-away quadtrees, skipping inactive ones. Convenience batch overload of `AddToCollisionQuadTree(Entity)`.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### AddToStaticRenderQuadTree(IEnumerable<Entity>)

```csharp
public void AddToStaticRenderQuadTree(IEnumerable<T> entities)
```

Inserts every active, sprite-rendered entity in `entities` into the `StaticRender` partition, computing a rotation-safe (greedy, always-square) bounding box from the entity's `SpriteAsset` so render-culling stays correct even if the sprite is later rotated. Entities without a resolvable sprite asset are skipped.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### GetCollisionEntitiesAt(Rectangle, List<NodeInfo<Entity>>)

```csharp
public void GetCollisionEntitiesAt(Rectangle boundingBox, List<NodeInfo<T>> list)
```

Populates `list` with every entry in the `Collision` partition whose bounding box overlaps `boundingBox`. This is the main broad-phase query used by physics systems to narrow down which entities to run precise collision checks against.

**Parameters** \
`boundingBox` [Rectangle](../../../Murder/Core/Geometry/Rectangle.html) \
`list` [List\<NodeInfo\<T\>\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.List-1?view=net-7.0) \

#### RemoveFromCollisionQuadTree(int)

```csharp
public void RemoveFromCollisionQuadTree(int entityId)
```

Removes an entity from the collision/push-away quadtrees, swallowing the "not found" case (which commonly happens when the entity was already removed by a previous operation). Use `TryRemoveFromCollisionQuadTree` instead if you need to know whether it actually removed anything.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

#### TryRemoveFromCollisionQuadTree(int)

```csharp
public bool TryRemoveFromCollisionQuadTree(int entityId)
```

Removes an entity with the given id from both the `Collision` and `PushAway` partitions.

**Parameters** \
`entityId` [int](https://learn.microsoft.com/en-us/dotnet/api/System.Int32?view=net-7.0) \

**Returns** \
[bool](https://learn.microsoft.com/en-us/dotnet/api/System.Boolean?view=net-7.0) \

#### RemoveFromCollisionQuadTree(IEnumerable<Entity>)

```csharp
public void RemoveFromCollisionQuadTree(IEnumerable<T> entities)
```

Removes every given entity from the collision/push-away quadtrees. Batch overload of `RemoveFromCollisionQuadTree(int)`.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### RemoveFromStaticRenderQuadTree(IEnumerable<Entity>)

```csharp
public void RemoveFromStaticRenderQuadTree(IEnumerable<T> entities)
```

Removes every given entity from the `StaticRender` partition.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

#### UpdateQuadTree(IEnumerable<Entity>)

```csharp
public void UpdateQuadTree(IEnumerable<T> entities)
```

Completely clears and rebuilds the `Collision` and `PushAway` quadtrees from scratch using the given list of entities. This is O(n) and discards the existing tree structure entirely, so prefer incremental `AddToCollisionQuadTree(Entity)`/`RemoveFromCollisionQuadTree(int)` calls where possible — we should avoid this if possible.

**Parameters** \
`entities` [IEnumerable\<T\>](https://learn.microsoft.com/en-us/dotnet/api/System.Collections.Generic.IEnumerable-1?view=net-7.0) \

⚡
